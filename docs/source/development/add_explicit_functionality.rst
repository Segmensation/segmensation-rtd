Adding new functionality (explicit approach)
========================

To add for example an imaging algorithm like `watershed segmentation <https://docs.opencv.org/4.x/d3/db4/tutorial_py_watershed.html>`_
of an image you need to do following steps:

- Implement interface for frontend
- Implement functionality of watershed in the backend
- Handle the information flow between frontend and backend


Adding frontend interfaces for watershed segmentation
--------------------------

Fist we create a new folder in the correct location where the new application should be located.
This can be in the *analyze*, *Classifier*, *open* or *prepare* section, 
We put the watershed algorithm in the ``segmensation-app/src/script/prepare`` section of the application.


.. image:: https://raw.githubusercontent.com/Segmensation/segmensation-docs/main/source/img/watershed/create_folder.png
    :alt: create frontend folder for watershed

Next you need to create a file called ``comp.vue`` inside the watershed folder. 

.. image:: https://raw.githubusercontent.com/Segmensation/segmensation-docs/main/source/img/watershed/create_comp_file.png
    :alt: create comp.vue file for frontend of watershed


That this newly create component gets found by the vue router, you need to register the directory you created. This needs to correspond to the location you created it in.
We created our frontend file in the *prepare* section so we need to edit the file ``/segmensation-app/src/components/ToolsetPrepare.vue``. 

.. image:: https://raw.githubusercontent.com/Segmensation/segmensation-docs/main/source/img/watershed/register_toolset.png
    :alt: register file in ToolsetPrepare

Now we can create our frontend code for this application. This is all done in the created ``segmensation-app/src/script/prepare/comp.vue`` file.

For the *watershed segmentation* we want the Name of the Algorithm and a button to start is on the chosen image.

The *<template>* section of this vue code determines how the frontend looks like. (`Template Syntax <https://vuejs.org/guide/essentials/template-syntax.html>`_)

.. code-block:: html

    <template>
        <v-list-item>
            <v-list-item-action>
                <v-icon>mdi-call-received</v-icon>
            </v-list-item-action>
            <v-list-item-content>
                <v-card-text>Watershed</v-card-text>
            <v-container class="text-right">
                <v-col>
                    <v-row>
                        <v-btn >Anwenden</v-btn>
                    </v-row>
                </v-col>
            </v-container>
            </v-list-item-content>
        </v-list-item>
    </template>

This creates a new item with an icon (mdi-call-received) in front of it. It has the name "Watershed" and a button called "Anwenden"

You should be able to start the frontend with `yarn electron:serve` and see the newly create section under the *"Vorbereiten"* tab.

.. image:: https://raw.githubusercontent.com/Segmensation/segmensation-docs/main/source/img/watershed/watershed_app1.png
    :alt: watershed_app1

Now we want to create the part that something happens when clicking on the button. we need to edit the template part so it gets connected to the <script> part of vue
(we will get to this in a second)

We add *@click="watershed()* to the button so it will activate the *watershed()* function when clicking. 
.. code-block:: html
    <v-container class="text-right">
        <v-col>
            <v-row>
                <v-btn @click="watershed()>Anwenden</v-btn>
            </v-row>
        </v-col>
    </v-container>


Now lets create the watershed function call.
For this we need the script section of the vue file.

.. code-block:: typescript

    <script lang="ts">
        import Vue from 'vue';
        import api from '@/api/api';
        import { apiImage } from '@/api/types';
        import store from '@/store';

        export default Vue.extend({
            name: 'watershed',

            data: () => ({}),

            methods: {
                async watershed() {
                    const selectImagePart = this.$store.state.imageList.find(
                        (x: apiImage) => x.id === this.$store.state.selectedImageId
                    ).parts[this.$store.state.selectedImageNr];
                },
            },
        });
    </script>

Now we created an function called watershed that is called when the button is clicked.
For now this function just calls the api and retrieves the selected images. 

Lets add an API call to the backend so we can compute the watershed segmentation on the selected image.

For this we add following code to the function:

.. code-block:: typescript

    async watershed() {
        const selectImagePart = this.$store.state.imageList.find(
            (x: apiImage) => x.id === this.$store.state.selectedImageId
        ).parts[this.$store.state.selectedImageNr];
        
        api.requestWatershed(
            this.$store.state.selectedImageId,
            selectImagePart.channel,
            selectImagePart.slice,
        )
        .then(() => store.commit('editImageReload'));
    }

This calls the API function *requestWatershed* and after executing this the displayed image will get reloaded. 


This is expandable in any way you want. You can add some dropdown menus or some text filed or ...
Take a look at other components already created or get inspired from `Vuetify <https://v2.vuetifyjs.com/en/>`_



Creating API call
--------------------------

To link the frontend to the backend we need to create a api call. 

For this we create a function in ``segmensation-app/src/api/api.ts``.
The function must be named ``requestWatershed`` since we did name it like this in the script part of the frontend

.. code-block:: typescript

    requestWatershed: async (fileName: string, channel: number, slice: number) =>
        instance.post(`/image/${fileName}/watershed`, {
            channel,
            slice,
        })

This will post an request via `Axios <https://axios-http.com/>`_ to the backend. 
This will not have an response. If you need one you may ad a part like 
.. code-block:: typescript

    requestWatershed: async (fileName: string, channel: number, slice: number) =>
        instance.post(`/image/${fileName}/watershed`, {
            channel,
            slice,
        }).then(response => {return response}  




Adding backend code for watershed segmentation
--------------------------

First we need to collect that API call in the backend. 
In ``segmensation-api/app.py`` we need to create the corresponding code for the Axios request. 

.. code-block:: typescript
    @app.post('/image/<key>/watershed')

Now we want to create a function that executes the watershed segmentation. 
We call the responding function that we will create afterwards. 

The code in ``app.py`` should look like:

.. code-block:: typescript
    @app.post('/image/<key>/watershed')
    def manipulation_watershed(key):
        file, channel, slice_nr = load_request_image(key)
        result = manipulation.watershed(file.load_image_file(channel, slice_nr))
        file.save_image_file(channel, slice_nr, result)

        return Response(status=200)

This will call *manipulation_watershed* and will save the response as an image and returns to the frontend that the code was successful.

Now we create a python file called ``watershed.py`` in ``segmensation-api/manipulation/``

In this file we can now create the function where we actually calculate the watershed segmentation. 

.. code-block:: python 
    import cv2 as cv
    import numpy as np


    def watershed(image: np.ndarray):
        """
        Calculates the watershed segmentation of the corresponding image
        :param image: image file to process as 2-dimensional numpy array
        :return: processed image array
        """

        # image to grayscale
        if len(image.shape) == 3:
            image_gray = cv.cvtColor(image,cv.COLOR_BGR2GRAY)

        # Thesholding of image
        ret, bin_img = cv.threshold(image_gray,0,255,cv.THRESH_BINARY_INV+cv.THRESH_OTSU)

        # Noise removal
        kernel = cv.getStructuringElement(cv.MORPH_RECT, (3, 3)) 
        bin_img = cv.morphologyEx(bin_img,  
                                cv.MORPH_OPEN, 
                                kernel, 
                                iterations=2) 
        
        # sure background area 
        sure_bg = cv.dilate(bin_img, kernel, iterations=3) 
        
        # distance transform
        dist = cv.distanceTransform(bin_img, cv.DIST_L2, 5) 
        
        # foreground area
        ret, sure_fg = cv.threshold(dist, 0.5 * dist.max(), 255, cv.THRESH_BINARY) 
        sure_fg = sure_fg.astype(np.uint8)
        sure_bg = sure_bg.astype(np.uint8)
        #unknown area
        unknown = cv.subtract(sure_bg, sure_fg) 

        # sure foreground
        ret, markers = cv.connectedComponents(sure_fg) 

        # Add one to all labels so that background is not 0, but 1 
        markers += 1
        # mark the region of unknown with zero 
        markers[unknown == 255] = 0

        # apply watershed Algorithm 
        markers = cv.watershed(image, markers) 
        
        labels = np.unique(markers) 
        unique_sections = [] 

        for label in labels[2:]:  
            # Create a binary image in which only the area of the label is in the foreground  
            #and the rest of the image is in the background    
            target = np.where(markers == label, 255, 0).astype(np.uint8) 
            
            # Perform contour extraction on the created binary image 
            contours, hierarchy = cv.findContours( 
                target, cv.RETR_EXTERNAL, cv.CHAIN_APPROX_SIMPLE 
            ) 
            unique_sections.append(contours[0]) 
        
        # Draw the outline 
        watershed_img = cv.drawContours(image, unique_sections, -1, color=(255, 0, 0), thickness=2) 


        return watershed_img
    

The only thing we now need to do is to register this function in ``segmensation-api/manipulation/__init__.py`` so we can find it in ``segmensation-api/app.py``.
For this we simply add 

.. code-block:: python 
    from .watershed import watershed

to the ``segmensation-api/manipulation/__init__.py`` file.


Start the frontend and backend and you should be able to execute the created watershed segmentation. 


.. image:: https://raw.githubusercontent.com/Segmensation/segmensation-docs/main/source/img/watershed/watershed_app2.png
    :alt: watershed_app2



!!CONGRATULATIONS!!

you build your first component in segmensation