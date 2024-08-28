
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

## Annotation Tools
All the tools we need to perform the annotations are in the `Points` tab located in the bottom left corner.

![image](https://github.com/user-attachments/assets/39850124-bf48-4d2f-961d-f2c3af46b599)

The `Labels` section contains the classes available in the tool. The assigned colors are the same as those in Semantic KITTI, and you can see the name of each class by hovering the mouse pointer over the color for a few moments. It is also possible to select a specific category from the dropdown menu above.

![image](https://github.com/user-attachments/assets/22394a89-8f66-46da-a4bc-745c3b1cd77d)

In this next section, we have following tools.

| Icon | Function |
|:-:|-|
| ![image](https://github.com/user-attachments/assets/385106bd-13f8-481f-b88a-a1b6d6af7179) | When selected along with a label, the `brush tool` can label regions using the left mouse button |
| ![image](https://github.com/user-attachments/assets/a6f65721-19a8-4ff2-9843-309894f8b242) | When selected along with a label, the `polygon tool` can label points inside a given polygon. The polygon is defined by selecting corner points with the left mouse button. The polygon is completed by pressing the right mouse button|
| ![image](https://github.com/user-attachments/assets/7f23b35f-6b6b-4140-9bb2-b24e9236aefb) | When enabled, the `overwrite labels tool` allows you to overwrite points that already have labels.|
| ![image](https://github.com/user-attachments/assets/8ae08d47-4354-4d22-ae4d-7d1a01482e85) | When enabled, the `filter labels tool` allows you to hide points that already have labels. To do this, with the tool enabled, simply return to the previously displayed label palette and hold down <kbd>Ctrl</kbd> while clicking on the label with the left mouse button.|

The `remove ground tool` is very useful for annotating objects that are above the ground. By setting a threshold, points that are close to the ground are gradually hidden.

![image](https://github.com/user-attachments/assets/1b215711-d987-47d4-a95a-820b69fe4241)

Similar to the previous tool, the `remove with plane` performs the same process but in reverse. By setting a threshold, points above the plane are gradually hidden. It is recommended to have the `show plane` option unchecked to facilitate visualization. It is also possible to adjust the theta and phi angles to change the rotation of the plane if necessary

![image](https://github.com/user-attachments/assets/9e027899-79f2-4daf-8247-b15ce2a18487)



