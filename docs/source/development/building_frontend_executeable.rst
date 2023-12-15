Building frontend executable
========

To create a executable from the frontend you have to execute:

``yarn electron:build``

in the folder where you have your frontend ``packet.json`` file.

You should find an executable in the newly created ``dist_electron`` directory

.. image:: https://github.com/Segmensation/segmensation-rtd/blob/d3ae55f592593e2fa868a0b3a050fd943f7c9e3b/docs/source/img/build_dir_for_exe.png?raw=true
   :alt: building App
   :align: center

This is not connected to the backend yet (running backend on server and adjusting variables for connection to server is needed),
but you can explore Segmensation already.

Since all data and the execution of the algorithms is done in the backend, non of the algorithms can be actually done when no connection to the backend is established.