---
layout: post
title: OpenCV haar training to .xml file
description: "one of the object detection methods in computer vision"
modified: 2014-04-23
tags: [Computer Vision]
---

- References:    
    - [opencv-haar-classifier-training](http://coding-robin.de/2013/07/22/train-your-own-opencv-haar-classifier.html) -> [github](https://github.com/mrnugget/opencv-haar-classifier-training) -> [Usage](https://docs.google.com/document/pub?id=14r34Pd51lKZNlfJIQVRS_3kbow1OcJBKV7wTRRAW5Vg)    
    - [Tutorial: OpenCV haartraining](http://note.sonots.com/SciSoftware/haartraining.html) -> [example (Window OS)](http://nayakamitarup.blogspot.com/2011/07/how-to-make-your-own-haar-trained-xml.html)              
- $ `git clone https://github.com/mrnugget/opencv-haar-classifier-training`    
- Put target images into `./positive_images`  
    - $ `find ./positive_images -iname "*.tif" > positives.txt`       
- Put background images into `./negative_images`    
    - $ `find ./negative_images -iname "*.tif" > negatives.txt`       
- Get *.vec files (maxidev refers to max\_intensity\_deviation)    

{% highlight css %}
    $ perl bin/createsamples.pl positives.txt negatives.txt\ 
    samples 1154 "opencv_createsamples -bgcolor 0 -bgthresh 0\ 
    -maxxangle 1.1 -maxyangle 1.1 maxzangle 0.5 -maxidev 255 -w 183 -h 212" 
{% endhighlight %}

- Download opencv-2.4.8 source code from [here](https://github.com/Itseez/opencv/releases)        
    - $ `cp src/mergevec.cpp ../opencv-2.4.8/apps/haartraining/`    
    - $ `cd ../opencv-2.4.8/apps/haartraining/`    

{% highlight css %}
    g++ `pkg-config --libs --cflags opencv` -I. -o mergevec mergevec.cpp\ 
    cvboost.cpp cvcommon.cpp cvsamples.cpp cvhaarclassifier.cpp\ 
    cvhaartraining.cpp -lopencv_core -lopencv_calib3d\ 
    -lopencv_imgproc -lopencv_highgui -lopencv_objdetect    
{% endhighlight %}

- Put executable mergevec ([my mergevec file](https://drive.google.com/file/d/0B-OcoMYLimAlR2diaERuT1hiTVU/edit?usp=sharing)) in opencv-haar-classifier-training  
    - $ `cp mergevec ../../../opencv-haar-classifier-training/`  
    - $ `cd ../../../opencv-haar-classifier-training/`    
    - $ `find ./samples -name '*.vec' > samples.txt`    
    - $ `./mergevec samples.txt samples.vec`    
- Train the classifier ([It takes a couple of days](http://coding-robin.de/2013/07/22/train-your-own-opencv-haar-classifier.html) (O_o))    

{% highlight css %}
$ opencv_traincascade -data classifier -vec samples.vec -bg negatives.txt\ 
    -numStages 12 -minHitRate 0.999 -maxFalseAlarmRate 0.5 -numPos 1154 -numNeg 15\ 
    -w 183 -h 212 -mode ALL -precalcValBufSize 1024 -precalcIdxBufSize 1024
{% endhighlight %}



