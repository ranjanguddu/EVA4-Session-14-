# S14: Creation of A Very Large Dataset

This Repo explains how you can, not just use available datasets in your journey of DNN but efficiently create them yourself.

## Description  
We have used approximately 100 background images and 100 foreground objects to create a massive dataset with more than 400,000 images.  
Also, corresponding masks for each resultant as well as foreground objects have been created.  
We ultimately create depth maps of all images in our dataset.  
A special focus has been laid on handling such massive sized data efficiently with limited resources.

## Starting with..
### Background  
Background contains pictures of empty roads of all sorts, ranging from city roads to flyovers. 

<b>Statistics</b>  
* Image dimensions: 224\*224 pixels  
* Image format: jpg - We take a special care to avoid png format here in order to save space.  
* Number of Images: 100 
* Folder size: 2.1 MB
* Background mean: [0.4066298566301917, 0.4002413496649073, 0.39249680184578123]
* Background std: [0.2516888771733121, 0.25270893840650427, 0.2627707634116584]

<p float="left">
  <img src="/background/S_50.jpg" width="150" />
  <img src="/background/S_3.jpg" width="150" /> 
  <img src="/background/S_73.jpg" width="150" />
  <img src="/background/S_102.jpg" width="150" />
  <img src="/background/S_57.jpg" width="150" />
</p>

### Foreground  
Foreground contains object as car on a transparent background in all possible orientations.  

<b>Statistics</b>  
* Image dimensions: varies from 94px to 120px (aspect ratio maintained to fit background)
* No.of channels: 4
* Image format: png - preserves the alpha channel(transparency)
* Number of Images: 100
* Folder Size: 1.2 MB
* Foreground mean:[0.20949517588176447, 0.19539478564017485, 0.19461715970327936]
* Foreground std: [0.28369063174894876, 0.2668295825763676, 0.26662684995218183]

<p float="left">
  <img src="/foreground/Car_0.png" width="100" />
  <img src="/foreground/Car_73.png" width="100" /> 
  <img src="/foreground/Car_23.png" width="100" />
  <img src="/foreground/Car_186.png" width="100" />
  <img src="/foreground/Car_75.png" width="100" />
  <img src="/foreground/Car_19.png" width="100" />
  <img src="/foreground/Car_70.png" width="100" />
  <img src="/foreground/Car_83.png" width="100" />
</p>  

### Foreground Mask
Foreground masks have been created using the alpha channel of the png images  
<b>Statistics</b>
* Image format: jpg
* Number of channels: 1
* Number of Images: 100
* Folder size: 135 KB 
* Fg_Mask Mean : 0.4901193707128269
* Fg_Mask Std: 0.4889552830051992

<p float="left">
  <img src="/fg_mask/Car_0_mask.jpg" width="100" />
  <img src="/fg_mask/Car_73_mask.jpg" width="100" />
  <img src="/fg_mask/Car_23_mask.jpg" width="100" />
  <img src="/fg_mask/Car_186_mask.jpg" width="100" />
  <img src="/fg_mask/Car_75_mask.jpg" width="100" />
  <img src="/fg_mask/Car_19_mask.jpg" width="100" />
  <img src="/fg_mask/Car_70_mask.jpg" width="100" />
  <img src="/fg_mask/Car_83_mask.jpg" width="100" />
</p>  

### Fg_Bg Together: OverLayed Images  
Foreground objects are overlayed on each background image at 20 random positions.  
This gives a total of 100\*200\*20 = 4,60,000 images.  
<b>Statistics</b>  
* Image dimensions: 224\*224\*3
* No.of channels: 3
* Image format: jpg - saves space as we don't need the transparency(alpha) channel here.
* Number of Images: 4,00,000
* Folder Size: 1.92 GB
* Dataset Mean: [0.406589950038055, 0.3974733626335778, 0.3922238309037007]
* Dataset Std: [0.2537575580108365, 0.2544099256403426, 0.26358312983854404]


Here's a peek into few of our images:  

<p float="left">
  <img src="/fg_bg/P_1.jpg" width="150" />
  <img src="/fg_bg/P_206074.jpg" width="150" />
  <img src="/fg_bg/P_100071.jpg" width="150" />
  <img src="/fg_bg/P_148576.jpg" width="150" />
  <img src="/fg_bg/P_156303.jpg" width="150" />
</p>

### Fg_Bg Masks  
These masks are created by overlaying the foreground masks on a black patch with size equal to background image's size.  
<b>Statistics</b>  
* Image dimensions: 224\*224\*1
* No.of channels: 1
* Image format: jpg - saves space as we don't need the transparency(alpha) channel here.
* Number of Images: 4,00,000
* Folder Size: 723MB
* Dataset Mask Mean: 0.06884130386902756
* Dataset Mask Std: 0.25071680302352883

The corresponding masks are:  

<p float="left">
  <img src="/fg_bg_mask/mask_1.jpg" width="150" />
  <img src="/fg_bg_mask/mask_206074.jpg" width="150" />
  <img src="/fg_bg_mask/mask_100071.jpg" width="150" />
  <img src="/fg_bg_mask/mask_148576.jpg" width="150" />
  <img src="/fg_bg_mask/mask_156303.jpg" width="150" />
</p>

### Fg_Bg Depth Maps  
Our Monocular Depth Estimation Maps have been produced using a pre-trained DenseNet-201 model, cloned from [this](https://github.com/ialhashim/DenseDepth) repo with minor modifications. Our modifications mainly include scaling up of each image during processing to get a better view and hence a better prediction of depth for each object. The images are loaded at size 224x224, scaled up to 480x480 during processing, and then scaled down back to 224x224 before saving.  
Lack of a Depth camera or a LIDAR camera leads us to rely on pretrained DenseNet-201 model to create depth maps.  

<b>Statistics</b>  
* Image dimensions: 224\*224\*1
* No.of channels: 1
* Image format: jpg - saves space as we don't need the transparency(alpha) channel here.
* Number of Images: 400,000
* Folder Size: 1.02 GB
* Depth Map Mean: 0.38157365288360556
* Depth Map Std: 0.25473305512119443  

Here's a glimpse of the depth maps generated:

<p float="left">
  <img src="/Depth maps/depth_P_1.jpg" width="150" />
  <img src="/Depth maps/depth_206074.jpg" width="150" />
  <img src="/Depth maps/depth_P_100071.jpg" width="150" />
  <img src="/Depth maps/depth_100792.jpg" width="150" />
  <img src="/Depth maps/depth_156303.jpg" width="150" />
</p>  

