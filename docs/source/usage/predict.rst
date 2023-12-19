Predicting Classes
==================

Random Forest Classifier
------------------------
The `Random Forest Classifier <https://web.archive.org/web/20160417030218/http://ect.bell-labs.com/who/tkh/publications/papers/odt.pdf>`_ that was created during Training can 
be used to predict the contents of other images.
For this, select another image from the upload section and run the 
Prediction.

.. image:: https://raw.githubusercontent.com/Segmensation/segmensation-docs/main/source/img/predict_rfc.jpg
   :alt: image of GUI

Resulting probability maps can be saved as images and pixel 
probabilities can be saved as CSV.

Here is an example of the input, the marking of two classes and the prediction output of this component.

.. |pic1| image:: /img/train/example.png
   :width: 30%

.. |pic2| image:: /img/train/randomForest/class_marking.png
   :width: 30%
   
.. |pic3| image:: /img/train/randomForest/prediction.png
   :width: 30%

|pic1|  |pic2| |pic3|


Hough Circle Transformation
---------------------------
`Hough Circle Transformation <https://en.wikipedia.org/wiki/Circle_Hough_Transform>`_ can be used to detect circles in images.

Here a whole batch ( the complete stack of slices of an image) can be computed here. 

The results can be downloaded and visualized. 

.. note::
   note that the LAST used parameters in the training step are getting used. 

.. image:: https://raw.githubusercontent.com/Segmensation/segmentation-rtd/main/docs/source/img/predict_hct.jpg
   :alt: image of GUI

After predicting the images can be visualized in 3D. 
Here you can see all selected slices in a image and the resulting calculated fitted objects.

This was developed to see a 3d mesh of tube like structures. If the tube like structure is seen on adjacent slices, 
they get connected. 

.. note::
   you can specify the radius when the tube like structures are still connected. This is measured in absolute px
   in x,y and radius of the centerpoints.   

.. image:: https://raw.githubusercontent.com/Segmensation/segmentation-rtd/main/docs/source/img/predict_hct.jpg
   :alt: image of GUI

.. image:: https://raw.githubusercontent.com/Segmensation/segmentation-rtd/main/docs/source/img/hough_circle_transformation_visu.png


The visualized 3d mesh is displayed in a browser. You can disable each slice and each connection between the slices.
The 3D-Mesh can ge rotated freely. 

.. image:: https://raw.githubusercontent.com/Segmensation/segmentation-rtd/main/docs/source/img/visu_pred_hct.png
   :alt: image of GUI