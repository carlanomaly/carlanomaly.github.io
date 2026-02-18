---
title: Dataset
date: 2025-01-01
type: landing

design:
  spacing: '3rem'

sections:
  - block: markdown
    content:
      title: Dataset Overview
      text: |
        <!-- Placeholder: insert composition, modalities, and annotation schema -->

  - block: markdown
    content:
      title: ''
      text: |
        ### Sensor Setup

        For data collection, we attached an array of sensors to the simulated vehicle. 

        <div style="max-width: 500px; margin: auto;">

        ![Sensor Setup](/img/carla-setup.png)

        </div>

  - block: markdown
    content:
      title: ''
      text: |
        ### Directory Structure

        {{< tree >}}
        carlanomaly/
        ├── train/
        │   ├── scenario-1/
        │   └── ...
        ├── val/
        │   ├── scenario-1/
        │   └── ...
        └── test/
            ├── normal/
            │   ├── scenario-1/
            │   └── ...
            └── anomalous/
                ├── scenario-1/
                └── ...
        {{< /tree >}}

  - block: markdown
    content:
      title: ''
      text: |
        ### Cameras

        The dataset contains pixel- and instance wise segmentation masks for each object in the scene. Each object has a unique ID. Since these annotations where generated in a simulation, the annotations are perfect.

        {{< tree >}}
        scenario/
        ├── rgb-front/
        │   ├── 000000.jpg
        │   └── ...
        ├── segmentation-front/
        │   ├── 000000.png
        │   └── ...
        └── depth-front/
            ├── 000000.png
            └── ...
        {{< /tree >}}

        ```python
        img = Image.open("segmentation-front/000099.png")

        # instance ids are encoded in the G and B channel
        id_fields = np.array(img)[:,:,1:3]
        instance_ids = np.zeros(shape=(id_fields.shape[0], id_fields.shape[1]), dtype=np.int32)
        instance_ids += id_fields[:,:,0]
        instance_ids += id_fields[:,:,1].astype(np.int32) << 8

        # per-pixel classes are encoded in the R channel
        segmentation_mask = np.array(img)[:,:,0]
        ```

        <div class="image-gallery">
          <figure>
            <img src="/img/000003.jpg" alt="Camera Image">
            <figcaption>Camera Image</figcaption>
          </figure>
          <figure>
            <img src="/img/000003.png" alt="Instance Segmentation Mask">
            <figcaption>Instance Segmentation Mask</figcaption>
          </figure>
          <figure>
            <img src="/img/000003.png" alt="Depth Map">
            <figcaption>Depth Map</figcaption>
          </figure>
        </div>

        <div class="image-gallery">
          <figure>
            <img src="/img/000080.jpg" alt="Camera Image">
            <figcaption>Camera Image</figcaption>
          </figure>
          <figure>
            <img src="/img/000080.png" alt="Instance Segmentation Mask">
            <figcaption>Instance Segmentation Mask</figcaption>
          </figure>
          <figure>
            <img src="/img/000080.png" alt="Depth Map">
            <figcaption>Depth Map</figcaption>
          </figure>
        </div>

  - block: markdown
    content:
      title: ''
      text: |
        ### Semantic LIDAR Point Clouds

        Pixel-Anotated LIDAR Pointclouds for each frame with realistic settings.

        {{< tree >}}
        scenario/
        └── pointclouds/
            ├── 000000.feather
            └── ...
        {{< /tree >}}

        These files can be loaded with pandas:

        ```python
        import pandas as pd
        # Columns: x, y, z, angle, object_id, class_id
        data = pd.read_feather("000000.feather")
        ```

        <div class="image-gallery">
          <figure>
            <img src="/img/pcl-0.jpg" alt="LIDAR Example 1">
            <figcaption>LIDAR Example 1</figcaption>
          </figure>
          <figure>
            <img src="/img/pcl-1.jpg" alt="LIDAR Example 2">
            <figcaption>LIDAR Example 2</figcaption>
          </figure>
        </div>

        #### KITTI Annotations

        Kitti annotations contain 3D bounding boxes and connect them to the camera.

        {{< tree >}}
        scenario/
        └── kitti-front/
            ├── complete_data/
            │   ├── 000000_extended.json
            │   └── ...
            ├── label_2/
            │   ├── 000000.txt
            │   └── ...
            └── calib/
                ├── 000000.txt
                └── ...
        {{< /tree >}}

  - block: markdown
    content:
      title: ''
      text: |
        ### Anomaly Annotations

        #### Sample- and Sensor-Level

        For **cameras** the per-pixel anomaly labels are available in a separate directory. Labels are written in a 1-channel PNG where 0 means normal and everything else means anomaly. Sensor-level anomaly labels are given in a CSV with an `anomaly` column.

        {{< tree >}}
        scenario/
        └── anomaly-front/
            ├── 000000.png
            ├── ...
            └── sensor.csv
        {{< /tree >}}

        For **LiDAR** the anomaly labels are similarly available in a separate directory:

        {{< tree >}}
        scenario/
        └── anomaly-pcl/
            ├── 000000.feather
            ├── ...
            └── sensor.csv
        {{< /tree >}}

        The `.feather` files are serialized dataframes with a column for the anomaly label.

        #### Observation-Level

        In CarlAnomaly, an observation is an anomaly when there is an anomaly in any of the sensors. For convenience, these are also stored in feather format:

        {{< tree >}}
        scenario/
        └── anomaly-observation.feather
        {{< /tree >}}

        #### Scenario-Level

        These labels are given by the directory.

  - block: markdown
    content:
      title: ''
      text: |
        ### Additional Data

        The dataset additionally contains sensor readings for the following sensors in CSV format:

        - **IMU**: Measuring acceleration and orientation of the ego vehicle
        - **GNSS**: Measuring position of the vehicle
        - **Weather**: Exact weather conditions
        - **Actions**: Actions executed by the auto-pilot (Note: these are the actions that are executed by CARLAs traffic manager after the last frame)

        {{< tree >}}
        scenario/
        ├── gnss.feather
        ├── imu.fether
        ├── weather.feather
        └── actions.feather
        {{< /tree >}}

        You can simply load these as pandas dataframes:

        ```python
        import pandas as pd
        weather = pd.read_feather("weather.feather")
        ```

        #### Example: IMU

        The per-step IMU readings look as follows:

        <div class="table-wrapper">
          <table class="cool-table">
            <thead>
              <tr>
                <th>index</th>
                <th>acceleration_x</th>
                <th>acceleration_y</th>
                <th>acceleration_z</th>
                <th>compass</th>
                <th>longitude_x</th>
                <th>longitude_y</th>
                <th>longitude_z</th>
              </tr>
            </thead>
            <tbody>
              <tr><td>0</td><td>-1.31</td><td>0.00</td><td>9.73</td><td>3.16</td><td>-0.00</td><td>-0.02</td><td>-0.01</td></tr>
              <tr><td>1</td><td>5.58</td><td>-0.02</td><td>9.82</td><td>3.16</td><td>-0.00</td><td>-0.01</td><td>-0.00</td></tr>
              <tr><td>2</td><td>5.90</td><td>-0.00</td><td>9.82</td><td>3.16</td><td>-0.00</td><td>-0.01</td><td>-0.00</td></tr>
              <tr><td>3</td><td>6.19</td><td>-0.01</td><td>9.82</td><td>3.16</td><td>-0.00</td><td>-0.00</td><td>-0.00</td></tr>
              <tr><td>4</td><td>5.90</td><td>-0.01</td><td>9.81</td><td>3.16</td><td>-0.00</td><td>-0.00</td><td>-0.00</td></tr>
              <tr><td>5</td><td>4.71</td><td>-0.01</td><td>9.81</td><td>3.16</td><td>-0.00</td><td>0.00</td><td>-0.00</td></tr>
              <tr><td>6</td><td>-0.01</td><td>-0.10</td><td>9.82</td><td>3.16</td><td>-0.00</td><td>0.01</td><td>-0.01</td></tr>
            </tbody>
          </table>
        </div>

        #### Example: Global Position (GNSS)

        <div style="max-width: 500px; margin: auto;">

        ![GNSS Coordinates in Matplotlib](/img/gnss.webp)

        </div>
---
