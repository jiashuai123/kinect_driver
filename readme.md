#Kinect driver for Ubuntu 14.04 and ROS indigo

*This tutorial introduces the procedures of installing kinect driver on Ubuntu 14.04 and ROS indigo.*

##Prerequisites
Install dependencies below:  
```
sudo apt-get install g++  
sudo apt-get install cmake cmake-gui  
sudo apt-get install doxygen  
sudo apt-get install mpi-default-dev openmpi-bin openmpi-common  
sudo apt-get install libflann1 libflann-dev  
sudo apt-get install libeigen3-dev  
sudo apt-get install libboost-all-dev  
sudo apt-get install libvtk5.8-qt4 libvtk5.8 libvtk5-dev  
sudo apt-get install libqhull*  
sudo apt-get install libusb-dev  
sudo apt-get install libgtest-dev  
sudo apt-get install git-core freeglut3-dev pkg-config  
sudo apt-get install build-essential libxmu-dev libxi-dev  
sudo apt-get install libusb-1.0-0-dev graphviz mono-complete  
sudo apt-get install qt-sdk openjdk-7-jdk openjdk-7-jre
```

##Install Kinect driver on Ubuntu

Install 3 drivers  below:  

* OpenNI  
* Kinect Sener Module  
* NITE  

These files can be downloaded from this git repo.  

###Install OpenNI
```
cd ${YOURDOWNLOADPATH}/kinect_driver/OpenNI
cd Platform/Linux/CreateRedist
chmod +x RedistMaker
./RedistMaker
cd ../Redist/OpenNI-Bin-Dev-Linux-x64-v1.5.7.10
sudo ./install.sh
```

###Install Kinect Sensor Module
```
cd ${YOURDOWNLOADPATH}/kinect_driver/SensorKinect
cd Platform/Linux/CreateRedist
chmod +x RedistMaker
./RedistMaker
cd ../Redist/Sensor-Bin-Linux-x64-v5.1.2.1
chmod +x install.sh
sudo ./install.sh
```

###Install NITE
```
cd ${YOURDOWNLOADPATH}/kinect_driver/NITE
sudo ./install.sh
```  
###Test Kinect driver
Then power on the kinect, plugin the USB wire and enter commands below in the terminal:
```
cd ${YOURDOWNLOADPATH}/kinect_driver/OpenNI/Platform/Linux/Bin/x64-Release
./NiViewer 
```
If error: **Open failed: Failed to set USB interface!**, use this trick: 
```
sudo modprobe -r gspca_kinect 
sudo modprobe -r gspca_main
```
If the problem is not solved, check your USB port, USB hub is NOT supported, you should plug USB into PC directly. And USB2.0 is better(I didn't test that).

if error: **Open failed: Xiron OS failed to wait on event!**, do this:
```
sudo chmod +x /usr/bin/XnSensorServer
```

Both RGB image and depth image should be shown on screen if you setup correctly.

##Install driver for ROS
From ROS Wiki page(*http://wiki.ros.org/openni_kinect*)
>The functionality for this stack has been split into two different stacks: openni_camera and openni_launch. This stack has been deprecated, reference those new stacks for updated documentation. 
```
sudo apt-get install ros-indigo-openni-camera ros-indigo-openni-launch
```

Use command below to launch kinect.
```
roslaunch openni_launch openni.launch
```


##Reference  

http://www.cnblogs.com/hitcm/p/5118318.html

http://wiki.frankiezafe.org/index.php?title=OpenNI_and_NITE_on_linux  

http://answers.ros.org/question/72022/primesense-failed-to-set-usb-interface-error/  

http://www.cnblogs.com/zxouxuewei/p/5271939.html

http://www.cnblogs.com/zxouxuewei/p/5272875.html

http://wiki.ros.org/openni_kinect