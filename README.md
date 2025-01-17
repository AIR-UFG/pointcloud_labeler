# Pointcloud Labeler Dockerfile

This Dockerfile sets up an environment for using the Pointcloud Labeler.
- [Point Labeler](https://github.com/jbehley/point_labeler): A tool for manually labeling point clouds.

## Setup

1. **Clone this repository:**
   ```bash
   git clone --recurse-submodules https://github.com/AIR-UFG/pointcloud_labeler.git
   cd pointcloud_labeler
   ```

2. **Build the Docker image:**
   ```bash
   docker build -t pointcloud_labeler Docker
   ```

3. **Run the Docker container:**

   To run the Docker container, utilize the provided run script with the following parameters:

   ```bash
   ./run.sh pointcloud_labeler --rm [--nvidia]
   ```

- `<image-name>`: The name you assigned to the Docker image during the build process.
- `--rm`: Automatically remove the container when it exits.
- `--nvidia`: Run the container with NVIDIA GPU support.

After running the container, a `shared-dir` folder will be created within the repository directory.

This folder is linked to the `/root/shared-dir` directory within the container. You can use this folder to share files between the host and the container, such as point cloud data or labeled data.

## Usage

1. **Prepare Point Cloud Data:**
   
   Place your dataset in the `shared-dir` folder.

2. **Run Point Labeler:**
   - Within the container, navigate to the Point Labeler's bin directory and run the Point Labeler:
     ```bash
     cd /root/point_labeler/bin
     ./labeler
     ```
   - Open the `/root/dataset/sequences/XX/` folder you want to annotate inside the Point Labeler to start labeling the point cloud.

   For more information on how to use the Point Labeler, please refer to the [Tutorial](TUTORIAL.md) we provided or the official [Point Labeler documentation](https://github.com/jbehley/point_labeler/wiki).

## Customizations

- An alias are added to facilitate common commands:
  - `labeler`: Launches the Point Labeler tool.
- The `run.bash` script launches the Docker container with appropriate configurations for GUI display and volume mounts.

## Zoom Issue
While using the tool, it was observed that zooming with the mouse wheel may not function correctly, depending on the specific mouse model and the operating system version. As stated in [Issue with Zooming Using the Mouse Wheel #84](https://github.com/jbehley/point_labeler/issues/84) on the official repository, the author has indicated no current plans to address UX improvements.

With this in mind, our team implemented a workaround by modifying a portion of the code in the function responsible for handling zoom. 

If you are interested in applying the same solution, simply replace the `Viewport.cpp` file located at `/root/point_labeler/src/widget/Viewport.cpp` with the `Viewport.cpp` file provided in the root of this repository.

The modification essentially updates the `wheelEvent` function by normalizing the delta value within the `if` block as follows:
```cpp
if (!numPixels.isNull()) {
   delta = numPixels.y() / 120.f; // solution
} else if (!numDegrees.isNull()) {
   delta = numDegrees.y() / 15.f; 
}
```
It is important to note that this change may alter the intended behavior of the tool. Use it only if you are experiencing issues with zoom functionality.


## Credits

- This Dockerfile is based on [instructions](https://gist.github.com/nerovalerius/80133f409f9ed0573522432244298195) by [Armin Niedermueller](https://github.com/nerovalerius/).
- [Point Cloud Labeling Tool](https://github.com/jbehley/point_labeler) was created by [Jens Behley](https://github.com/jbehley).