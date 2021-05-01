# AI_Graphics
All of my assignments are listed in here, let me know if there are any issues. Thanks for the interesting course!

## Rendering 
For investigating random fourier features for image encoding I used Tancik's handy ipynb demo [here](https://github.com/tancik/fourier-feature-networks/blob/master/Demo.ipynb)  as a framework. I modified the train and test split to be random which ended up being non-trivial for me, though I am sure there is a simple to do it that I was not aware of. I changed his MLP training function to record RMSE on the 1/3 of random test data. I then plotted sigma for 10 variations and dimension for 4 variations for each image. No embedding is shown as a line on each plot. It looks like optimal sigma-squared hovers around 10-20 depending on image complexity. The cornell box image model benefitted from a lower sigma than the more detailed images. Higher dimension seems to be a benefit for all images but leads to diminishing returns. Exploring past 256 would probably have been useful.

Here is the experiment: https://github.com/jackld2/AI_Graphics/blob/main/2D%20Positional%20Encoding%20Experiment.ipynb

## Image Generation
I'm not satisfied with the images that I generated, mainly the cow still looks way out of place. The approach I took was to first use SPADE to get an image without lighting as recommended, and then applied style transfers to each to get the desired lighting. I tried generating a cow with SPADE COCO with bad results, it ended up looking like a cow shaped blob with a cowhide texture. I opted to use the cutout of a real cow and use harmonization to incorporate it into the scene. This was after each style transfer, so I thought that the cow would properly harmonize with each style in terms of lighting. I used [SinGAN](https://github.com/tamarott/SinGAN) to harmonize the cow in each scene by naivley pasting the cow into each image and using a mask around the cow. Unfortunately the results are lackluster, and I am guessing that this is because there is no reference for the cow on my trained model, only landscape. At lower scales it composited the cow as a bush, the results below are at scale 8. As you can see the cow still looks horribly out of place despite harmonization trained on each image. I definitely learned a lot about using open source models in this process though. Since my linux machine bit the dust recently I needed an environment, and I was able to get CUDA working on a Windows 10 subsystem with a lot of effort, which is a newer development for NVIDIA.

### Morning with some fog, sunrise
![IMG](https://github.com/jackld2/AI_Graphics/blob/main/ImageGen/morningcow.png?raw=true)
### Noon on bright day
![IMG](https://github.com/jackld2/AI_Graphics/blob/main/ImageGen/nooncow.png?raw=true)
### Noon on overcast day
![IMG](https://github.com/jackld2/AI_Graphics/blob/main/ImageGen/overcastcow.png?raw=true)
### Sunset with orange/red sky
![IMG](https://github.com/jackld2/AI_Graphics/blob/main/ImageGen/sunsetcow.png?raw=true)

## Shape

## Challenge: Reconstruction of the 2D Shepp Logan Phantom
I relied heavily on [Tancik's CT experiment code](https://github.com/tancik/fourier-feature-networks/blob/master/Experiments/2d_CT.ipynb) to attempt this challenge. He uses 

## Project: Attempt at a learned sampler for a NeRF representation
