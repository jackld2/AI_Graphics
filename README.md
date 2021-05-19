# AI_Graphics
All of my assignments are listed in here, let me know if there are any issues. Thanks for the interesting teachings!

## Rendering 
For investigating random fourier features for image encoding I used Tancik's handy ipynb demo [here](https://github.com/tancik/fourier-feature-networks/blob/master/Demo.ipynb)  as a framework. I modified the train and test split to be random which ended up being non-trivial for me, though I am sure there is a function to do it that I was not aware of. I changed his MLP training function to record RMSE on the 1/3 of random test data. I then plotted sigma for 10 variations and dimension for 4 variations for each image. No embedding is shown as a line on each plot. It looks like optimal sigma-squared hovers around 10-20 depending on image complexity. The cornell box image model benefitted from a lower sigma than the more detailed images. Higher dimension seems to be a benefit for all images but leads to diminishing returns. Exploring past 256 would probably have been useful. I feel like this paper has already added a tool to my belt, incredible results.

Here is the experiment: https://github.com/jackld2/AI_Graphics/blob/main/2D%20Positional%20Encoding%20Experiment.ipynb
It should open right up via the link, but for some reason you may need to reload it a few times.

## Image Generation
I'm not satisfied with the images that I generated, mainly the cow still looks way out of place. The approach I took was to first use SPADE to get an image without lighting as recommended, and then applied style transfers to each to get the desired lighting without the cow. I tried generating a cow with SPADE COCO with bad results, it ended up looking like a cow shaped blob with a cowhide texture. I opted to use the cutout of a real cow and use harmonization to incorporate it into the scene. This was after each style transfer, so my logic was that the cow would properly harmonize with each style in terms of lighting. I used [SinGAN](https://github.com/tamarott/SinGAN) to harmonize the cow in each scene by naivley pasting the cow into each image and using a mask around the cow. Unfortunately the results are lackluster, and I am guessing that this is because of the simplicity of the scene of the trained model. At lower scales it composited the cow as a bush, the results below are at scale 8, which I believe confirms this. As you can see the cow still looks horribly out of place despite harmonization trained on each image (partly my fault due to a bad pasting job). I definitely learned a lot about using open source models in this process though. Since my linux machine bit the dust recently I needed an environment to work in, and I was able to get CUDA working on a Windows 10 subsystem with a lot of effort but suprisingly little problems, I believe this is a new development from Microsoft and Nvidia.

### Morning with some fog, sunrise
![IMG](https://github.com/jackld2/AI_Graphics/blob/main/ImageGen/morningcow.png?raw=true)
### Noon on bright day
![IMG](https://github.com/jackld2/AI_Graphics/blob/main/ImageGen/nooncow.png?raw=true)
### Noon on overcast day
![IMG](https://github.com/jackld2/AI_Graphics/blob/main/ImageGen/overcastcow.png?raw=true)
### Sunset with orange/red sky
![IMG](https://github.com/jackld2/AI_Graphics/blob/main/ImageGen/sunsetcow.png?raw=true)

## Shape
I looked around at a bunch of proofs and material that involved seperating hyperplane theorem and or convex cones, but in lecture you said that it was quite easy, so I just ran at it with proof by contradiction. Perhaps I should be more formal with my definitions and elaborate more, it seems too simplistic. Nevertheless, it's here: https://github.com/jackld2/AI_Graphics/blob/main/proof.pdf

## Motion
The paper “Contact and Human Dynamics from Monocular Video” shows an excellent way to improve current human pose estimation for monocular video by adding physics-based optimizations. However, the paper and video demonstration show that low quality input motions still lead to a bad output. I believe this is because of noisy input that the model is not trained for. The example was given in lecture of an autonomous car that veers off into a state where it has no reference from its training process, a minor error, where it then makes an even graver mistake. I believe that one could argue this is a similar situation, and imitation learning might be applicable. 

There are certain inputs for which Rempe et al.’s model do not perform well. The visual example given was a quick motion high kick. Though the model assumes a stationary camera, I would wager that changing/awkward perspectives such as a top view would lead to the same issues. Without the feet visible, the model has nothing to go on, and would likely lead to some strange results. If these situations could be supplemented with imitation learning where bad solutions could be eliminated from the model, it might be able to perform a lot better in these noisy situations. For example, imitation learning could be used for the high kick shown in the video, or without the feet in view. It could not work perfectly but it may be worth exploring.

The reason I think this could be useful is that motion capture gear tends to be expensive and cumbersome. Quality monocular video tracking would likely have a lot of benefits in motion tracking applications, I have in mind actors. You can see from Rempe et al.’s model that the added physics optimizations take the capture to the next level in terms of usability, but complex motion is unusable.If an actor could do complex movements with a capable tracking system for imitation learning, it might be possible to switch to monocular tracking and perform those movements without issue.

[Contact and Human Dynamics from Monocular Video](https://geometry.stanford.edu/projects/human-dynamics-eccv-2020/)

[Immitation Learning Slides](https://katefvision.github.io/katefSlides/immitation_learning_I_katef.pdf)

[Imitation Learning in Robots](https://link.springer.com/referenceworkentry/10.1007%2F978-1-4419-1428-6_758#:~:text=Definition,skills%20performed%20by%20another%20agent.)


## Challenge: Reconstruction of the 2D Shepp Logan Phantom
I was looking at [Tancik's CT experiment code](https://github.com/tancik/fourier-feature-networks/blob/master/Experiments/2d_CT.ipynb) and I noticed that he is able to get a pretty good reconstruction, so I wanted to explore his implementation. I used his method of projection. Challege: https://github.com/jackld2/AI_Graphics/blob/main/CT.ipynb

## Project: Adaptive Sampling
[Sampling Project](https://github.com/jackld2/AI_Graphics/blob/main/Sampling_Project.ipynb)
Again, you might have to click reload a few times for it to embed properly, not sure why this is the case. I recommend opening in Collab if necessary.

