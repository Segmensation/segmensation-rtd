Preparing an Image
====================================
To receive good results with object detection methods in images, those 
images usually need some kind of preprocessing. Segmensation currently 
only offers such functions for images where objects are defined by their 
brightness.

Closing
-------
`Closing <https://homepages.inf.ed.ac.uk/rbf/HIPR2/close.htm>`_ is an operator from the field of mathematical morphology that is 
usually used on binary or grayscale images. As the name implies, closing 
is an operator that removes small holes in objects. It also reduces 
general noise in images.

The operator consists of two steps: Dilation and Erosion. 
Dilation expands the area that is assigned to an object, while erosion 
shrinks it. Due to the way these two operations work, the borders of 
objects stay similar, but holes that are filled by dilation can not be 
opened again by erosion.


Parameters:

Number of iterations for Dilation and Erosion.

.. image:: /img/prepare/closing_interface.png
   :alt: image of GUI

.. |pic1| image:: /img/training/example.png
   :alt: expample

.. |pic2| image:: /img/prepare/closing.png
   :alt: image of closing

|pic1|  |pic2|

Shrinking
------------------
Shrinking can be used to manipulate the color histogram of an image. 
With this operation, certain colors can be enhanced by reducing the color 
space to the desired range.
This operation will simply limit the available color space for the selected image 


.. note::
    This operation also automatically maps the color values to a range 
    between 0 and 255, which is required for saving the image as JPG or 
    PNG.

.. image:: /img/prepare/shrinking_interface.png
   :alt: image of GUI

.. |pic3| image:: /img/training/example.png
   :alt: expample

.. |pic4| image:: /img/prepare/shrinking.png
   :alt: image of shrinking

|pic3|  |pic4|


Gausian Blur
------------------
`Gausian Blur <https://shimat.github.io/opencvsharp_docs/html/7b0301d7-322d-a554-8d3f-32fd8ca0ee50.htm>`_ is an image processing technique. It is used to reduce noise and detail in an image.
The purpose of this technique is to create a smoother and softer version of the image by averaging
the pixel values within a specified neighborhood around each pixel

.. note::
    This operation has only one parameter. It controls the size of the used filter.
    It can be set between 1 and 50. This means that in x and y that many pixels are 
    getting used to calculate the blur.
    
.. image::https://raw.githubusercontent.com/Segmensation/segmentation-rtd/main/docs/source/img/gaussianBlur.png
   :alt: image of GUI


.. |pic5| image:: /img/training/example.png
   :alt: expample

.. |pic6| image:: /img/prepare/blur.png   
   :alt: image of gaussian blur

|pic5|  |pic6|


Thresholding
------------------
`Thresholding <https://docs.opencv.org/4.x/d7/d4d/tutorial_py_thresholding.html>`_ is used to segment or separate objects in a image. This will produce
and image that is devided in two classes, either foreground or background.

.. note::
    There are three different types of thresholds that can be chosen
    via the dropdown menu. 
    Adaptive Mean: calculates a local threshold for each pixel based on the mean in a local neighborhood of that pixel
    Adaptive Gaussian: uses the weighted average instead of the average in a local neighborhood
    Otsu: this is a global technique that calculates an optimal threshold. It maximizes the variance between the two classes. 

    For different images different thesholds can be optimal.

.. image:: /img/prepare/thresholding_interface.png   
   :alt: image of GUI

.. |pic7| image:: /img/training/example.png
   :alt: expample

.. |pic8|image:: /img/prepare/adaptive_mean.png   
   :alt: image of mean thresholding


|pic7| - |pic8|


.. |pic9|image:: /img/prepare/adaptive_gauissian.png   
   :alt: image of gaussian thresholding

.. |pic10|image:: /img/prepare/otsu.png
   :alt: image of otsu thresholding

|pic9| - |pic10|

Watershed
------------------

`Watershed <https://docs.opencv.org/4.x/d3/db4/tutorial_py_watershed.html>`_ is an image processing algorithm to segment an image. 
The image is viewed as a topographic surface where high intensity denotes peaks and hills while low intensity denotes valleys. 
Then the valleys get filled. When two or more of these individual valleys get connected with water, a "barrier" gets put in place.
The barriers that got created give the segmentation result.

An example of the watershed algorithm results can be seen here


.. |pic11|image:: ./img/prepare/watershed_interface.png
   :alt:: watershed GUI
      
.. |pic12|image:: ./img/prepare/watershed.png
   :alt: watershed of an example

|pic11| - |pic12|



