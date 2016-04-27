 

![enter image description here](http://rhodes2.api.algocian.com/client/algocian-logo.png)

<br>
<br>
<br>


edit at: 
https://stackedit.io/editor#





# Artemis1 SDK Documentation 

### v1.12 - March 2015

![enter image description here](http://alg11.api.algocian.com/Artemis1_logo1s.png) 


## Table of contents

[TOC]


## Introduction

The Artemis 1 SDK enables the integration of advanced machine learning algorithms in x86 and embedded systems. Included in the SDK is the Artemis 1 person detection solution than enables 

The SDK is targeted at security and surveilance system integrators, smart-home camera manufacturers and OEM camera manufacturers.
 




-------------

#### Versions

The following versions are supported:

| Platform | Architecture | Type | Support |  
| :---: | :---: | :---: | :---: |
| PC | i386 | 32-bit | Limited support |
| PC | amd64 | 64-bit | Fully supported |
| ARM | armv7 | 32-bit | Fully supported |
| ARM| AArch64 | 64-bit | Fully supported |



The current version of the SDK includes specific versions for amd64, armv7 and armv8 systems.

---------------



### Compatibility

Currently the SDK is compatible with Linux systems on armv7, armv8, i386 and amd64 architectures. A standard libc system installation is required. Different versions of the SDK will be provided for each architecture.

In the case of embedded systems, additional system libraries might be required depending on the deployment. If necessary, these libraries can be provided by Algocian.


#### Memory requirements

The memory required  for processing video/image feeds depends on image size and number of  processor cores that will be used.  Under a typical deployment scenario at 640x480, memory requirements will be approximately 30MB.

#### Disk space requirements

Artemis1 does not use any intermediate temporary files. The disk space required for the libartemis1  library and required third-party libraries will be 5-15MB depending on architecture.

#### External library requirements

Processing raw frames with the Algocian API, in a deployment scenario, does not require any external libraries except libstdc++.so.6, libpthread.so.

### Embedded system CPU usage management

libartemis1 provides the means to manage the CPU requirements when on a limited enviroment.  The default running mode is single-threaded.  When running on 2 or more cores, artemis1 will provide 

#### Running as a separate process

libartemis1 is not tied to any particular means of video input / output. Running artemis1 as a standalone process is an option, where video frames are communicated across a pipe or shared memory. You can look at the example process_rgb24 for details on how to communicate video frames across different processes,



 



---------------


### What is inside

The following directory structure is followed in all our versions of the SDK. In a typical scenario only the .so file will be required to be deployed.

| Location | Description |
| :---     | --- |
| include/artemis1.h | C++ header file that provided access to the SDK |
| lib/libartemis1.so | Library to use at link time |
| support/ | additional libraries that might be required in a deployment system |
| examples/ | showcase of Artemis1 with code examples |
| artemis1-sdk.pdf | Documentation for using the SDK |



------------------

### Examples included


> examples/process_video.sh
> 

Processes a video file and generates a series of output images with results. Metadata will be included in standard output.

> examples/process_rgb24.sh
 
Processes raw RGB24 frames of size 640x480 from standard input. Output jpeg files can be generated or just metadata. The data can be fed from a webcam using the following command:

<b> ffmpeg -s 640x480 -f v4l2 -i /dev/video2 -f rawvideo -pix_fmt bgr24 - | sh examples/process_rgb24.sh 640 480 0 </b>


<br>

------------


## Getting better accuracy out of artemis1





### Models

A 'model` is the type of object that will be detected by Artemis1. For example, if you are using the PERSON_UPRIGHT model, a person entering the frame will be detected but cars, pets and other objects will not.

Currently artemis1 supports the PERSON_UPRIGHT model which detect persons in a image/video frame. Additional models will be included in the future, for example <i>PETS_GENERIC</i> will be able to detect pets and exclude humans.

The PERSON_UPRIGHT_12_GENERIC model currently included in the SDK indicates the following:
* It is a model to detect persons.
* Version number of model is 12.
* It is a generic model, means it was not optimized for any particular camera or situation.

### Generating optimal models for you camera

Given a particular camera and scenario, a targeted model can be generated from our database.




### QuickStart 

```c++

#include <artemis1.h>

using namespace algocian;


void
detectPeople()
{
    Artemis1Detector *detector;

    detector = new Artemis1Detector();
    
    detector->setModel(PERSON_UPRIGHT_12);
    detector->setInputFormat(640, 480, FMT_RGB24);


    while(1) {

        detectionsList persons;		
		char *image_data;
	
		image_data = grabCameraInputRGB();

        persons = x.detect(image_data);

		if(persons.size() > 0) {  
        
            printf("Alert! Person Detected");
            
            x.saveOutputImage("/tmp/output.jpg");

			alertUser("Person Detected", "/tmp/output.jpg");
        }
		
	}
	



```

    

```c++
#include <artemis1.h>

using namespace algocian;


void
detectPeople()
{
    detector = new Artemis1Detector(PERSON_UPRIGHT_12_GENERIC, 0.1, 0.9, 640, 480, algocian::FMT_RGB24);
    
    Artemis1Detector *detector;


    detector = new Artemis1Detector();

    // Select the default person detection model
    
    detector.setModel(PERSON_UPRIGHT_12);

    // Detect a person from 10% to 90% height of the image
    
    detector.setDetectionHeights(0.1,0.9);

    // Set the input format as RGB 24 bits per pixel
    
    detector.setInputFormat(640,480,algocian::FMT_RGB24);


    // Set the input format as RGB 24 bits per pixel
    
    detector.setSensitivity(10);
   
    
    detector.setInputFormat(640,480,algocian::FMT_YUV24)

    detector.setInputFormat(640,480,algocian::FMT_IPLIMAGE)



    while(1) {

        detectionsList persons;

        persons = x.detect(image_data);

        persons = x.detect(image_data, x1, y1, x2, y2);
        
        
        x.updateBackground(image_data);
        
        
        persons = x.detect(IplImage *input_image);


        if(persons.size() > 0) {
          
            printf("Alert! Person Detected");
          
          
          
            printf("  at location %d %d", );

        }

        x.saveOutputImage("/tmp/output.jpg");

    }

}

```

-------------

### Compilation with Artemis1 SDK

To compile include the sdk directory in your include path:

`-I ./artemis1_sdk/include`

And the artemis1 library in linkage time:

`-L ./artemis1_sdk/lib -L ./artemis1_sdk/support -lartemis1`

In case of compilation problems, we can provide prebuilt static libraries if necessary.


-----

### Additional libraries for platform support


![enter image description here](http://alg11.api.algocian.com/api1.png)

### API Reference 
> <b> detect(char *image_data) </b> (void)

> <b> detect_region(char *image_data, int x1,int y1, int x2, int y2) </b> (void)
> <b> update_background(char *image_data, int x1,int y1, int x2, int y2) </b> (void)

 > <b> save_output_image(char *file_name)  </b> (void)

 > <b> set_detection_heights </b> (float percent_lower_height, float percent_max_height)  </b>   ⇨ (void)



> <b> set_model(int `model_type`) </b> (void)

> Specify which objects the detector will detect. 

The following models are supported currently:

1.  <code>PERSON_UPRIGHT_12_GENERIC</code>: Detect persons using the latest (Feb 2016) model.

Future releases will include additional models and tuning of models to specific cameras. Possible scenarios are PET_GENERIC, CAR_GENERIC etc..

>  <b>set_input_format(int `width`, int `height`, int `format`) </b>  ⇨ void
>
>   Specify input image size in pixels and format of raw input pixels. 

The following are accepted input formats:

-  `IMG_FORMAT_RGB24`: RGB, 3 bytes per pixel, i.e. RGBRGBRGB. 
-  `IMG_FORMAT_YUV24`: YUV 3 bytes per pixel, i.e. YUVYUVYUV.

| Parameter | Description |
| :---      | ---         |
| width  | Width of the image in pixels. |
| height | Height of the image in pixels. |
| format | One of the following: IMG_FORMAT_RGB24, IMG_FORMAT_YUV24, IMG_FORMAT_IPLIMAGE |




## Garbage ##


     sdfsdfds
     fdsfsd
         
```




