In this page, I'll explain how to configure, build and import OpenCV library to your java project with OpenNI and Kinect support on ARM based platform.

I've followed the instructions at
http://docs.opencv.org/doc/tutorials/introduction/desktop_java/java_dev_intro.html
and
http://docs.opencv.org/doc/user_guide/ug_highgui.html

## Notation:
>panda     Refers to the target system (PandaBoard)
>host      Refers to the host system (PC)

## Requirements:
OpenJDK v6-v7 (sudo apt-get install default-jdk)
Ant (sudo apt-get install ant)
Python v2.6+ (sudo apt-get install python or sudo apt-get update python)
Cmake (sudo apt-get install cmake)
Nano (sudo apt-get install nano)
For all of your questions, please do not hesitate to mail me at denizbeker@hotmail.com

## 1 - Install OpenNI and Avin's SensorKinect Drivers

You can refer to the instructions at this post or you can download my libraries compiled for arm-v7+ here. At last, you shall have a file/folder system as below:

/usr/lib/libnimCodecs.so 
/usr/lib/libnimMockNodes.so
/usr/lib/libnimRecorder.so
/usr/lib/libOpenNI.jni.so
/usr/lib/libOpenNI.so  
/usr/lib/libXnDDK.so
/usr/lib/libXnFormats.so
/usr/lib/libXnDeviceFile.so
/usr/lib/libXnCore.so
/usr/lib/libXnDeviceSensorV2KM.so
/usr/bin/XnSensorServer

## 2 - Install OpenCV
>panda Go to your work directory
>panda Download OpenCV and Checkout for 
>git clone git://github.com/Itseez/opencv.git
>cd opencv
>git checkout 2.4
Open CMakeLists.txt file and allow OpenNI.
>sudo nano CMakeLists.txt 
>At OpenCV Cmake Options, find the line containing OpenNI and change OFF value to ON

![alt tag](https://github.com/dBeker/Kinect-Depth/blob/master/Images/OpenNI.PNG)

The trick comes here. As we are using OpenJDK, JAVA_HOME path may be missing eventhough you can type and use "java" command from terminal. That's why we need to set JAVA_HOME path.
export JAVA_HOME=/usr/lib/jvm/java-1.7.0-openjdk-armhf
cmake -DBUILD_SHARED_LIBS=OFF ..
At the end of Cmake, you shall see Java and OpenNI parameters as below:

![alt tag](https://github.com/dBeker/Kinect-Depth/blob/master/Images/output.png)

The rest of the parameters may vary according to your needs.
Now, we can use make to build OpenCV according to our configuration
make -j8 
(-j8 allows make to build parallel. If you don't want parallel build, just write "make". If you enter a too big value, you will suffer highly from performance )

## 3- Copy library output (opencv/build/lib) to /usr/lib
>panda cd opencv/build/lib
>panda cp * /usr/lib

## 4- You can use opencv libraries in java by calling 
>java System.loadLibrary("opencv_java246");
at initialization part of your code.



