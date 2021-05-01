# AI_Graphics
All of my assignments are listed in here, let me know if there are any issues. Thanks for the interesting course!

## Rendering 
For investigating random fourier features for image encoding I used Tancik's handy ipynb demo [here](https://github.com/tancik/fourier-feature-networks/blob/master/Demo.ipynb)  as a framework. I modified the train and test split to be random which ended up being non-trivial for me, though I am sure there is a simple to do it that I was not aware of. I changed his MLP training function to record RMSE on the 1/3 of random test data. I then plotted sigma for 10 variations and dimension for 4 variations for each image. No embedding is shown as a line on each plot. It looks like optimal sigma-squared hovers around 10-20 depending on image complexity. The cornell box image model benefitted from a lower sigma that the more detailed images. Higher dimension seems to be a benefit for all images but leads to diminishing returns. Exploring past 256 would probably have been useful.

Here is the experiment: https://github.com/jackld2/AI_Graphics/blob/main/2D%20Positional%20Encoding%20Experiment.ipynb

## Image Generation
![IMG](https://github.com/jackld2/AI_Graphics/blob/main/ImageGeneration/morningcow.png?raw=true)
