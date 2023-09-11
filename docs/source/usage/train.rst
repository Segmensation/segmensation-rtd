Training
========

Random Forest Classifier
------------------------
Currently there are two modes of Training for the Random Forest 
Classifier: A fast one with medium accuracy and a slow one with 
higher accuracy. The maximum depths of the tree are 10 and 17 
respectively.

.. image:: https://raw.githubusercontent.com/Segmensation/segmensation-docs/main/source/img/train_rfc.jpg
   :alt: image of GUI

Hough Circle Transformation
---------------------------
Hough Circle Transformation can be used to detect circles in images.

.. note:: 
    Hough Circle Transformation is an operation that does not 
    require training. It is currently listed under "Training" aswell 
    as under "Prediction". During "Training" the Transformation is 
    calculated and the result is shown. "Prediction" only contains a 
    download option for the results.

.. image:: https://raw.githubusercontent.com/Segmensation/segmensation-docs/main/source/img/train_hct.jpg
   :alt: image of GUI


Ellipse Detection
---------------------------
Ellipse Detection can be used to detect circular and elliptical shapes in images.


.. note:: 
   This does not require training. This is a classic detection method.
   First a Canny filter is deployed. On this image all contours are getting found with the algorithm from Suzuki et.al.[TSA]
   Then it fits an ellipse around a set of 2D points. The function calculates the ellipse that fits a set of 2D points created from the contour.


.. image:: https://raw.githubusercontent.com/Segmensation/segmensation-docs/main/source/img/train_hct.jpg
   :alt: image of GUI
.. [TSA] Satoshi Suzuki and others. Topological structural analysis of digitized binary images by border following. Computer Vision, Graphics, and Image Processing, 30(1):32–46, 1985.