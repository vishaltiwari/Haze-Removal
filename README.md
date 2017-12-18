## About

Most of the remote sensing data, have a lot of unclear data. This is because of the presence of haze and clouds. Due to the presence of haze, it can’t be directly used for other application or analysis purpose. We know that low wavelength waves get more scattered by atmosphere, due to its interaction with the atmospheric interaction. This can be explained using Mie theory.
A lot of research has been put in the development of such an algorithm. Previous work are mainly of two types. First one is spectral filtering and Spectral Analysis. Some examples of spectral filtering are FFT (Fast fourier Transform) and Wavelet removal. Some examples of spectral Analysis algorithms are Cluster Matching and Tasselled Cap Transform[1,2]. Haze optimization Transform is also a kind of spectral analysis algorithm. 
The data that will be used during this project is LANDSAT data. We will also be using LANDSAT temporal data, for the implementation of histogram matching.

## Haze Optimization Transform

Haze optimization Transform, first makes a scatter plot between two bands, and finds a best fitting line, that passes through those points. This algorithm uses the property that in the non-hazly image the correlation between the bands will be high, and low in hazly images.
After finding the best fitting line, called the Clear Line(CL), a HOT image is calculated using the following[3,4] :

`Hotvalue = DN1sin(theta) - DN2cos(theta)`

Where DN1is the DN value of a pixel in band 1 and DN2is the pixel value in band 2.
Now we use this obtained HOT image to remove the haze from the visible bands. We will plot histograms of DN values vs number of pixel corresponding to that DN value of a band, for some HOT values, that we have calculated from the above step.
After this we make a plot between, HOT value and Min DN value of histograms, and see that, lower the HOT value, clearer the image. Thus we now take the difference in the min_DN values between two HOT values, and subtract that value from corresponding DN values in the input image. We will do that for all the HOT values . After this operation we will get a haze free image.


## Area Selection
A sliding window on the input image calculates the average HOT value of the window and used the window region with the minimal average HOT value. 

## References

[1] R. Richter, “A spatially adaptive fast atmospheric correction algorithm,” International Journal of Remote Sensing, vol. 17, no. 6, pp.1201-1214, Apr, 1996.-R. Richter, “Atmospheric correction of satellite data with haze

[2]removal including a haze/clear transition region,” Computers & Geosciences, vol. 22, no. 6, pp. 675-681, Jul, 1996.

[3] “An Image Transform to Characterize and Compensate for Spatial Variations in Thin Cloud Contamination of Landsat Images”-Y. Zhang1, 2, B. Guindon1 and J. Cihlar1

[4] “A haze removal module for multispectral satellite imagery”-Jianbo Hua,b, Wei Chena, Xiaoyu Lia ,Xingyuan Hea,*

[5] “Unbiased histogram matching quality measure for optimal radiometric normalization”-Zhengwei Yang, Rick Mueller

[6] “Haze detection and removal in high resolution satellite image with wavelet analysis,”-Y. Du, B. Guindon, and J. Cihlar
