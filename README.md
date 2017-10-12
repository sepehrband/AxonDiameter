[![DOI](https://zenodo.org/badge/45438813.svg)](https://zenodo.org/badge/latestdoi/45438813)
[![Open Source Love](https://badges.frapsoft.com/os/v1/open-source.png?v=103)](https://osf.io/yp4qg/)
[![MIT Licence](https://badges.frapsoft.com/os/mit/mit.png?v=103)](https://opensource.org/licenses/mit-license.php)

# Axon diameter mapping of mouse corpus callosum
This link is provided in accordance with the following articles:
>**Towards Higher Sensitivity And Stability Of Axon Diameter Estimation With Diffusion-Weighted Magnetic Resonance Imaging**  
>Farshid Sepehrband, Daniel C. Alexander, Nyoman D. Kurniawan, David C. Reutens, and Zhengyi Yang  
>**NMR in Biomedicine 29(3):293-308.** DOI: 10.1002/nbm.3462, [link](http://onlinelibrary.wiley.com/doi/10.1002/nbm.3462/abstract)

>**Parametric Probability Distribution Functions for Axon Diameters of Corpus Callosum**  
>Farshid Sepehrband, Daniel C. Alexander, Kristi A. Clark, Nyoman D. Kurniawan, Zhengyi Yang and David C. Reutens
>**Frontiers in Neuroanatomy, 10:59.** DOI: 10.3389/fnana.2016.00059 [link](http://journal.frontiersin.org/article/10.3389/fnana.2016.00059/full)

## Supplementary material

## Diffusion-weighted MRI data (ActiveAx with G<sub>max</sub> = 1.35 T/m)
Two datasets were acquired in this study, which are made available here:
- 3-shell data can be downloaded [here](https://www.dropbox.com/s/bqy7buyy0m6cv6s/3-shell.zip?dl=0).
- 5-shell data can be downloaded [here](https://www.dropbox.com/s/wr667f86chisn4u/5-shell.zip?dl=0).
- gradient encoding directions can be found [here](https://www.dropbox.com/s/me79dwdesa4sjeo/encDir.zip?dl=0).

For information regarding the acquisition protocol please see the above article. 

## Electron Microscopy (EM) data
- Raw electron microscopy images can be found [here](https://www.dropbox.com/s/r8wi9ovwc8fq2zy/Raw.zip?dl=0).
- Manually segmented axons (in MATLAB format) can be found [here](https://www.dropbox.com/s/8fh34qiwvow96yi/MATfiles.zip?dl=0).

** Note that some of the images were excluded from axon diameter estimation, due to low image quality. However they are included in the link above (raw EM images), as they may be useful for other purposes. 
 
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
