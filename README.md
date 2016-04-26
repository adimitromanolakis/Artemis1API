
# Algocian SDK Documentation v1.12
## March 2015


### Introduction

-------------

### Versions

---------------



### Compatibility

The current version of the SDK is compatible with Linux systems on armv7, armv8, i386 and amd64 architectures. A standard GLIBC system installation is required. Different versions of the SDK are provided for each architecture.

Memory requirements: The memory required for the Artemis1 SDK depends on image size and number of cores used, can be as low as 20MB.

Additional libraries required for each particular deployment will be provided by algocian.

---------------


### What is included in the SDK

| Parameter | Description |
| :---     | --- |
| include/artemis1.h | C++ header file that provided access to the SDK |
| lib/libartemis1.so | Library to use at link time |
| support/ | additional libraries that might be required in the deployment system |
| examples/ | showcase of Artemis1 with code examples |
| artemis1-sdk.pdf | Documentation for using the SDK |



------------------

### Examples included

> sdfsdf
> 

------------

### QuickStart 

    

```c++

#include <artemis1.h>

using namespace algocian;

Artemis1Detector *detector;

void
detectPeople() 
{
	
	detector = new Artemis1Detector();
	
	// Select the default person detection model
	detector.setModel(PERSON_UPRIGHT_12); 
	
	// Detect a person from 10% to 90% height of the image
	detector.setDetectionHeights(0.1,0.9); 
	
	// Set the input format as RGB 24 bits per pixel
	detector.setInputFormat(640,480,algocian::FMT_RGB24);


	detector.setInputFormat(640,480,algocian::FMT_YUV24)
	detector.setInputFormat(640,480,algocian::FMT_IPLIMAGE)
	
	
	
	
	while(1) {
	
		detectionsList persons;
		
		persons = x.detect(char *data);
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



 
> <b> setModel(int `model_type`) </b> (void)
>
> Specify which objects the detector will detect. 

The following models are supported currently:

1.  <code>PERSON_UPRIGHT_12_GENERIC</code>: Detect persons using the latest (Feb 2016) model.

Future releases will include additional models and tuning of models to specific cameras. Possible scenarios are PET_GENERIC, CAR_GENERIC etc..

>  <b>setInputFormat(int `width`, int `height`, int `format`) </b>  ⇨ void
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






     sdfsdfds
     fdsfsd
     
$ x*x*x*x \frac{1}{x^2} $
    

```


## GetDetections ##
