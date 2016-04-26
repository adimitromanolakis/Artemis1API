
# <b> Algocian C++ API </b>
## Platforms supported: x86/arm/arm64


![enter image description here](http://blog.cobia.net/cobiacomm/wp-content/uploads/2014/06/api-512x270.png)

![enter image description here](http://alg11.api.algocian.com/api1.png)

 

## ![enter image description here](http://alg11.api.algocian.com/api1.png) </b>

>  <b>setInputFormat(int `width`, int `height`, int `format`) </b>  ⇨
>
>   Specify input image size in pixels and format of raw input pixels. 

The following are accepted input formats:

-  `IMG_FORMAT_RGB24`: RGB, 3 bytes per pixel, i.e. RGBRGBRGB. 
-  `IMG_FORMAT_YUV24`: YUV 3 bytes per pixel, i.e. YUVYUVYUV.

| Parameter | Description |
| :---:     | --- |
| width | Width of the image in pixels. |
| height | Height of the image in pixels. |
| format | One of the following: IMG_FORMAT_RGB24, IMG_FORMAT_YUV24, IMG_FORMAT_IPLIMAGE |


     sdfsdfds
     fdsfsd
     
$ x*x*x*x \frac{1}{x^2} $
    

## QuickStart 

    
> sdfsdf
> 

```c++

#include <artemis1.h>

void
detectPeople() 
{
	
	x = new Artemis1Detector();
	
	x.setModel(algocian::PERSON_UPRIGHT_12)
	
	x.setDetectionHeights(0.1,0.9); // Detect a person from 10% to 90% height of the image
	
	x.setInputFormat(640,480,algocian::FMT_RGB24)
	x.setInputFormat(640,480,algocian::FMT_YUV24)
	x.setInputFormat(640,480,algocian::FMT_IPLIMAGE)
	
	
	
	
	while(1) {
	
	
	
	algocian::detections persons;
	
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


## GetDetections ##
