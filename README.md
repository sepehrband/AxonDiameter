##ActiveAx with ultra-high gradient strength (G<sub>max</sub> = 1.35 T/m)
This link is provided in accordance with the following article:
>**Towards Higher Sensitivity And Stability Of Axon Diameter Estimation With Diffusion-Weighted Magnetic Resonance Imaging**  
>Farshid Sepehrband, Daniel C. Alexander, Nyoman D. Kurniawan, David C. Reutens, and Zhengyi Yang  
>**NMR in Biomedicine 29(3):293-308.** DOI: 10.1002/nbm.3462, [link](http://onlinelibrary.wiley.com/doi/10.1002/nbm.3462/abstract)

## Supplementary material

## Diffusion-weighted MRI data
Two datasets were acquired in this study, which are made available here:
- 3-shell data can be downloaded [here](https://dl.dropboxusercontent.com/u/17531966/ActiveAxD/3-shell.zip).
- 5-shell data can be downloaded [here](https://dl.dropboxusercontent.com/u/17531966/ActiveAxD/5-shell.zip).

For information regarding the acquisition protocol please see the above article. 

## Electron microscopy (EM) data
- Raw electron microscopy images can be find [here](https://dl.dropboxusercontent.com/u/17531966/ADD/EM/Raw.zip).
- Processed images (in MATLAB format) can be find [here](https://dl.dropboxusercontent.com/u/17531966/ADD/EM/MATfiles.zip).

** Please note that some of the images were not processed for axon diameter analysis, because of their low quality. However the raw images are included here, as they may be useful for other purposes. 
 
### MATLAB demo (EM analysis)

```
%% input raw material and show them
I = imread('Path-to-EM-data/Raw/Genu/ccleftb1_5k.tif');
laod('Path-to-EM-data/MATfiles/ccleftb1_5k.mat');
figure(1);subplot(1,2,1);imshow(I,[]);
subplot(1,2,2);imshow(ccleftb1_5k.AllCircles);

%% extract axon diameter distribution and plot it
bwComp = bwconncomp(ccleftb1_5k.AllCircles);
pixelSize = (0.023);
for i = 1:length(bwComp.PixelIdxList)
    temp = bwComp.PixelIdxList(i);
    Volume(i) = length(temp{1}).*(pixelSize^2);
    Dia(i) = 2*sqrt(Volume(i)/pi);
end
figure(2);histogram(Dia)
grid on
xlabel('Axon diameter');ylabel('Frequency')
title('Axon diameter distribution')
```

![alt tag](https://raw.github.com/sepehrband/AxonDiameter/master/EM.tif)  
![alt tag](https://raw.github.com/sepehrband/AxonDiameter/master/ADD.tif)  
