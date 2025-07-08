# Post-Flight Analytics

!!! note
    This section is a work in progress.

The following pages explain how to run our [open-goodfire-tools](https://github.com/robotics-88/open-goodfire-tools) package, which provides lidar and video analytics for forest and fire data processing. This tool is independent of our flight stack, and can be used on any lidar and video datasets. However, drones using our flight stack do provide the relevant required inputs.

## LiDAR Overview

Our LiDAR workflow provides the following data products from a .laz pointcloud:

- [X] DEM tif
- [X] Aspect tif
- [X] Slope tif
- [X] Base Canopy Height Model tif
- [X] Tree ID LAS file
- [X] Diameter at Breast Height csv
- [X] Fuel volume tif (when before and after laz both available)

## Video Overview

Our video workflow provides the following data products from a .mp4:

- [X] Gaussian Splats
- [ ] PCD