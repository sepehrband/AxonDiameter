##ActiveAx with ultra-high gradient strength (G<sub>max</sub> = 1.35 T/m)
This link is provided in accordance with the following articles:
>**Towards Higher Sensitivity And Stability Of Axon Diameter Estimation With Diffusion-Weighted Magnetic Resonance Imaging**  
>Farshid Sepehrband, Daniel C. Alexander, Nyoman D. Kurniawan, David C. Reutens, and Zhengyi Yang  
>**NMR in Biomedicine 29(3):293-308.** DOI: 10.1002/nbm.3462, [link](http://onlinelibrary.wiley.com/doi/10.1002/nbm.3462/abstract)

>**Parametric Probability Distribution Functions for Axon Diameters of Corpus Callosum**  
>Farshid Sepehrband, Daniel C. Alexander, Kristi A. Clark, Nyoman D. Kurniawan, Zhengyi Yang and David C. Reutens
>**Front. Neuroanat.**, in press.

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
title('Axon Diameter Distribution (ADD) of demo image')
set(gca,'LineWidth',1,'FontSize',12,'FontWeight','Bold','FontName','Arial'); 
xlabel('Axon diameter \fontsize{9}(\mum)','FontSize',12,'FontName','Arial'); 
ylabel('Frequency','FontSize',12,'FontName','Arial'); 
```

![alt tag](https://raw.github.com/sepehrband/AxonDiameter/master/EM.png)   

![alt tag](https://raw.github.com/sepehrband/AxonDiameter/master/ADD2.png)  
