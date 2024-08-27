
# Point Cloud Labeler Tutorial

This document aims to outline the annotation process used within our organization. 
It does not cover every detail regarding the tool, only those considered important for our purpose. 
Any information not included here can be found in the [official wiki](https://github.com/jbehley/point_labeler/wiki).

## First Steps
First, you need to follow the instructions in the README to set up the environment. It's worth noting that if the poses of the data have already been calculated, it is not necessary to run SuMa.

After that, with the tool already open, just click on the 'open' icon in the top left corner, navigate to the folder where the data is located, and choose a sequence to start annotating.

![image](https://github.com/user-attachments/assets/e96e1be5-151b-45b8-8dbc-0f274147dc01)

As soon as the point cloud is loaded, the program may become slow due to the large number of points. 
A strategy to alleviate this overload is to adjust the tile size parameter, which is present in the `settings.cfg` file located in `point_labeler/bin`. 

In summary, tiles are the regions where frames are rendered for the annotator. 
The smaller this value, the smaller the rendered region will be, making the program lighter. On the other hand, very low values may make it more difficult to identify objects during annotation.

## Navigation
The main commands for navigation are as follows

|Key|Function|
|:-:|:-:|
| <kbd>W</kbd><br><kbd>A</kbd><kbd>S</kbd><kbd>D</kbd> | Move the camera |
| <kbd>Mouse Wheel</kbd> |  Zoom in and zoom out |
|<kbd>CTRL</kbd> + <kbd>Right Mouse Button</kbd>| Rotate |
