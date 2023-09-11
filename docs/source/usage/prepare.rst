Preparing an Image
==================
To receive good results with object detection methods in images, those 
images usually need some kind of preprocessing. Segmensation currently 
only offers such functions for images where objects are defined by their 
brightness.

Closing
-------
Closing is an operator from the field of mathematical morphology that is 
usually used on binary or grayscale images. As the name implies, closing 
is an operator that removes small holes in objects. It also reduces 
general noise in images.

The operator consists of two steps: Dilation and Erosion. 
Dilation expands the area that is assigned to an object, while erosion 
shrinks it. Due to the way these two operations work, the borders of 
objects stay similar, but holes that are filled by dilation can not be 
opened again by erosion.

.. note::
    For details on how closing works and corresponding examples, see `this 
    page <https://homepages.inf.ed.ac.uk/rbf/HIPR2/close.htm>`_ from HIPR_.

Parameters:

Number of iterations for Dilation and Erosion.

.. image:: https://raw.githubusercontent.com/Segmensation/segmensation-docs/main/source/img/prepare_closing.jpg
   :alt: image of GUI

Shrinking
---------
Shrinking can be used to manipulate the color histogram of an image. 
With this operation, certain colors can be enhanced by reducing the color 
space to the desired range.


.. note::
    This operation also automatically maps the color values to a range 
    between 0 and 255, which is required for saving the image as JPG or 
    PNG.

.. image:: https://raw.githubusercontent.com/Segmensation/segmensation-docs/main/source/img/prepare_shrinking.jpg
   :alt: image of GUI

.. [HIPR] Hypermedia Image Processing Reference - R. Fisher, S. Perkins, 
    A. Walker and E. Wolfart

Gausian Blur
---------
Gausian Blur is an image processing technique. It is used to reduce noise and detail in an image.
The purpose of this technique is to create a smoother and softer version of the image by averaging
the pixel values within a specified neighborhood around each pixel

.. note::
    This operation has only one parameter. It controls the size of the used filter.
    It can be set between 1 and 50. This means that in x and y that many pixels are 
    getting used to calculate the blur.
    
.. image::https://raw.githubusercontent.com/Segmensation/segmentation-rtd/main/docs/source/img/gaussianBlur.png
   :alt: image of GUI

Thresholding
---------
Thresholding is used to segment or separate objects in a image. This will produce
and image that is devided in two classes, either foreground or background.

.. note::
    There are three different types of thresholds that can be chosen
    via the dropdown menu. 
    Adaptive Mean: calculates a local threshold for each pixel based on the mean in a local neighborhood of that pixel
    Adaptive Gaussian: uses the weighted average instead of the average in a local neighborhood
    Otsu: this is a global technique that calculates an optimal threshold. It maximizes the variance between the two classes. 

    For different images different thesholds can be optimal.

.. image:: https://raw.githubusercontent.com/Segmensation/segmentation-rtd/main/docs/source/img/threshold.png
   :alt: image of GUI

   .. image:: https://raw.githubusercontent.com/Segmensation/segmentation-rtd/main/docs/source/img/threshold_dropdown.png
   :alt: image of GUI