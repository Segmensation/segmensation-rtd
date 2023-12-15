Training
========

Random Forest Classifier
------------------------

The `Random Forest Classifier <https://web.archive.org/web/20160417030218/http://ect.bell-labs.com/who/tkh/publications/papers/odt.pdf>`_  is 
a meta estimator that fits a number of decision tree classifiers on various sub-samples of the dataset and uses averaging to improve the predictive accuracy and control over-fitting.
The implementation follows closely the implementation of `sklearn <https://scikit-learn.org/stable/modules/generated/sklearn.ensemble.RandomForestClassifier.html>`_

Currently there are two modes of Training for the Random Forest Classifier: A fast one with medium accuracy and a slow one with 
higher accuracy. The maximum depths of the tree are 10 and 17 respectively.

.. image:: https://raw.githubusercontent.com/Segmensation/segmensation-docs/main/source/img/train_rfc.jpg
   :alt: image of GUI


The Training part doesn't yeld results. You need to execute the prediction after training to see results. 

Hough Circle Transformation
---------------------------
`Hough Circle Transformation <https://en.wikipedia.org/wiki/Circle_Hough_Transform>`_ can be used to detect circles in images.
In this training config only one Slice of an image can be chosen. 
After  a successful Hough Transformation the image with its annotations is getting displayed. 

This step is for trying on only one image before using on a whole stack of slices. 

A tutorial about the implementation of the Hough Circle Transformation can be found `here <https://docs.opencv.org/3.4/d4/d70/tutorial_hough_circle.html>`_ 

.. note:: 
    Hough Circle Transformation is an operation that does not 
    require training. It is currently listed under "Training" aswell 
    as under "Prediction". During "Training" the Transformation is 
    calculated and the result is shown. "Prediction" only contains a 
    download option for the results.

.. image:: https://raw.githubusercontent.com/Segmensation/segmentation-rtd/main/docs/source/img/train_hct.jpg
   :alt: image of GUI

|pic1|  |pic2|

.. |pic1| image:: /img/hough_circle_transformation_input.png
   :width: 45%

.. |pic2| image:: /img/hough_circle_transformation_result.png
   :width: 45%


Ellipse Detection
---------------------------
Ellipse Detection can be used to detect circular and elliptical shapes in images.

The calculated image annotations can be downloaded. 

This follows the approach by `OpenCV <https://docs.opencv.org/3.4/de/d62/tutorial_bounding_rotated_ellipses.html>`_

.. note:: 
   This does not require training. This is a classic detection method.
   First a Canny filter is deployed. On this image all contours are getting found with the algorithm from Suzuki et.al. called `Topological structural analysis <https://www.nevis.columbia.edu/~vgenty/public/suzuki_et_al.pdf>`_
   Then it fits an ellipse around a set of 2D points. The function calculates the ellipse that fits a set of 2D points created from the contour.


.. image:: https://raw.githubusercontent.com/Segmensation/segmentation-rtd/main/docs/source/img/ellipse_detection.png
   :alt: image of GUI

|pic3|  |pic4|

.. |pic3| image:: /img/ellipse_detection_input.png
   :width: 45%

.. |pic4| image:: /img/ellipse_detection_result.png
   :width: 45%
