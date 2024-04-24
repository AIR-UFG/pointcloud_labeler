# Pointcloud Labeler Dockerfile

This Dockerfile sets up an environment for using the Pointcloud Labeler with ROS2 (Robot Operating System) and SuMa (Surfels for Mapping) for point cloud processing.

## Features

- [SuMa](https://github.com/jbehley/SuMa): A package for surfel-based mapping and 3D reconstruction.
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

After running the container, a folder structure will be created within the repository directory:

<pre>
pointcloud-files
├── bin-files
└── labels
</pre>

This folder structure is linked to the `/root/dataset/sequences/00/` directory within the container. The `bin-files` directory is used to store the `.bin` files of the point cloud data. The `labels` directory is used to store the labels files generated by the Point Labeler.

## Usage

1. **Prepare Point Cloud Data:**
   
   Place your `.bin` files inside the `bin-files` directory in the repository. This directory is linked to the `/root/dataset/sequences/00/velodyne` directory within the container.

2. **Run SuMa:**
   The SuMa visualizer is used to calculate the poses of the point cloud data.
   - Within the container, navigate to SuMa's bin directory and run SuMa visualizer:
     ```bash
     cd /root/SuMa/bin
     ./visualizer
     ```
   - Open the first `.bin` file of the point cloud in the `/root/dataset/sequences/00/velodyne` folder.
   - Press the play button to calculate poses.
   - Save the `poses.txt` file to `/root/dataset/sequences/00/`.

3. **Run Point Labeler:**
   - Within the container, navigate to the Point Labeler's bin directory and run the Point Labeler:
     ```bash
     cd /root/point_labeler/bin
     ./labeler
     ```
   - Open the `/root/dataset/sequences/00/` folder inside the Point Labeler to start manually labeling the point cloud.

   For more information on how to use the Point Labeler, please refer to the [Point Labeler documentation](https://github.com/jbehley/point_labeler/wiki).

## Customizations

- Aliases are added to facilitate common commands:
  - `visualizer`: Launches the SuMa visualizer.
  - `labeler`: Launches the Point Labeler tool.
- The `run.bash` script launches the Docker container with appropriate configurations for GUI display and volume mounts.


## Credits

- This Dockerfile is based on [instructions](https://gist.github.com/nerovalerius/80133f409f9ed0573522432244298195) by [Armin Niedermueller](https://github.com/nerovalerius/).
- [Point Cloud Labeling Tool](https://github.com/jbehley/point_labeler) and and [SuMa](https://github.com/jbehley/SuMa) were created by [Jens Behley](https://github.com/jbehley).