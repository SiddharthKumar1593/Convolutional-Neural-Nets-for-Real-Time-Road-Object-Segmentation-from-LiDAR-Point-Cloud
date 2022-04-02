## _SqueezeSeg_: Convolutional Neural Nets with Recurrent CRF for Real-Time Road-Object Segmentation from 3D LiDAR Point Cloud

This repository contains a tensorflow implementation of SqueezeSeg, a convolutional neural network model for LiDAR segmentation. A demonstration of SqueezeSeg can be found below:

<p align="center">
    <img src="https://github.com/SiddharthKumar1593/Convolutional-Neural-Nets-for-Real-Time-Road-Object-Segmentation-from-LiDAR-Point-Cloud/blob/main/readme/pr_0005.gif" width="600" />
</p>


## License
**SqueezeSeg** is released under the BSD license (See [LICENSE](https://github.com/SiddharthKumar1593/Convolutional-Neural-Nets-for-Real-Time-Road-Object-Segmentation-from-LiDAR-Point-Cloud/blob/main/LICENSEE) for details). The **dataset** used for training, evaluation, and demostration of SqueezeSeg is modified from [KITTI](http://www.cvlibs.net/datasets/kitti/) raw dataset. For your convenience, we provide links to download the converted dataset, which is distrubited under the [Creative Commons Attribution-NonCommercial-ShareAlike 3.0 License](https://creativecommons.org/licenses/by-nc-sa/3.0/).

## Installation:

The instructions are tested on Ubuntu 16.04 with python 2.7 and tensorflow 1.0 with GPU support. 
- Clone the SqueezeSeg repository:
    ```Shell
    git clone https://github.com/BichenWuUCB/SqueezeSeg.git
    ```
    We name the root directory as `$SQSG_ROOT`.

- Setup virtual environment:
    1. By default we use Python2.7. Create the virtual environment
        ```Shell
        virtualenv env
        ```

    2. Activate the virtual environment
        ```Shell
        source env/bin/activate
        ```

- Use pip to install required Python packages:
    ```Shell
    pip install -r requirements.txt
    ```

## Demo:
- To run the demo script:
  ```Shell
  cd $SQSG_ROOT/
  python ./src/demo.py
  ```
  If the installation is correct, the detector should write the detection results as well as 2D label maps to `$SQSG_ROOT/data/samples_out`. Here are examples of the output label map overlaped with the projected LiDAR signal. Green masks indicate clusters corresponding to cars and blue masks indicate cyclists.
  <p align="center">
    <img src="hhttps://github.com/SiddharthKumar1593/Convolutional-Neural-Nets-for-Real-Time-Road-Object-Segmentation-from-LiDAR-Point-Cloud/blob/main/readme/0001.gif" width="600" />
  </p>


## Training/Validation
- First, download training and validation data (3.9 GB) from this [link](https://www.dropbox.com/s/pnzgcitvppmwfuf/lidar_2d.tgz?dl=0). This dataset contains LiDAR point-cloud projected to a 2D spherical surface. Refer to our paper for details of the data conversion procedure. This dataset is converted from [KITTI](http://www.cvlibs.net/datasets/kitti/) raw dataset and is distrubited under the [Creative Commons Attribution-NonCommercial-ShareAlike 3.0 License](https://creativecommons.org/licenses/by-nc-sa/3.0/).
    ```Shell
    cd $SQSG_ROOT/data/
    wget https://www.dropbox.com/s/pnzgcitvppmwfuf/lidar_2d.tgz
    tar -xzvf lidar_2d.tgz
    rm lidar_2d.tgz
    ```

- Now we can start training by
    ```Shell
    cd $SQSG_ROOT/
    ./scripts/train.sh -gpu 0 -image_set train -log_dir ./log/
    ```
   Training logs and model checkpoints will be saved in the log directory.
   
- We can launch evaluation script simutaneously with training
    ```Shell
    cd $SQSG_ROOT/
    ./scripts/eval.sh -gpu 1 -image_set val -log_dir ./log/
    ```
    
- We can monitor the training process using tensorboard.
    ```Shell
    tensorboard --logdir=$SQSG_ROOT/log/
    ```
    Tensorboard displays information such as training loss, evaluation accuracy, visualization of detection results in the training process, which are helpful for debugging and tunning models, as shown below:
    ![alt text](https://github.com/SiddharthKumar1593/Convolutional-Neural-Nets-for-Real-Time-Road-Object-Segmentation-from-LiDAR-Point-Cloud/blob/main/readme/Screen%20Shot%202018-02-17%20at%206.13.44%20PM.png)
    ![alt text](https://github.com/SiddharthKumar1593/Convolutional-Neural-Nets-for-Real-Time-Road-Object-Segmentation-from-LiDAR-Point-Cloud/blob/main/readme/Screen%20Shot%202018-02-17%20at%206.14.05%20PM.png)


