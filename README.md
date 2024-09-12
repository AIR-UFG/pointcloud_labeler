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


## Credits

- This Dockerfile is based on [instructions](https://gist.github.com/nerovalerius/80133f409f9ed0573522432244298195) by [Armin Niedermueller](https://github.com/nerovalerius/).
- [Point Cloud Labeling Tool](https://github.com/jbehley/point_labeler) was created by [Jens Behley](https://github.com/jbehley).