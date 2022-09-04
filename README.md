[![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github//wakamenori/txt2imghd-colab/blob/master/txt2imghd.ipynb)


## Introduction
This notebook is basically a Colab version of [txt2imghd](https://github.com/jquesnelle/txt2imghd) and also NSFW disabled.  
I take some codes from the original repo and made it work on Colab. It's easy for people who has no coding background to use it.

`txt2imghd` generates high-resolution images using txt2img and img2img.
> txt2imghd is a port of the GOBIG mode from progrockdiffusion applied to Stable Diffusion, with Real-ESRGAN as the upscaler.  
> It creates detailed, higher-resolution images by first generating an image from a prompt, upscaling it, and then running img2img on smaller pieces of the upscaled image, and blending the result back into the original image.  

(quoted from [original repo](https://github.com/jquesnelle/txt2imghd))

## How it works
1. Generate an image from a prompt using txt2img. Or load a image file.
2. Scale up the image using Real-ESRGAN.
3. Run img2img on smaller pieces of the up-scaled image.
4. Blend the result back into the upscaled image.

### Detailed explanation
#### Step.1 Generate an image from a prompt using txt2img
> Let's say you generate an image in pixel size of 512x512 using txt2img.
![Original image](https://github.com/wakamenori/txt2imghd-colab/blob/master/gallery/Original.png?raw=true)

#### Step.2 Scale up the image using Real-ESRGAN
> Scale up the image to 1024x1024.
![up-scaled](https://github.com/wakamenori/txt2imghd-colab/blob/master/gallery/up-scaled_2x.png?raw=true)

#### Step.3 Run img2img on smaller pieces of the up-scaled image
> Chop up-scaled image into slices in pixel size of original image.  
In this example, up-scaled image will be chopped into 9 images in pixel size of 512x512.  
Then run img2img on every small images with the same prompt for original image.  
This process generates more detailed and cleaner images compared to just up scaling the image
![img2img-1](https://github.com/wakamenori/txt2imghd-colab/blob/master/gallery/slice_img2img.png?raw=true)
![img2img-2](https://github.com/wakamenori/txt2imghd-colab/blob/master/gallery/slice_img2img(2).png?raw=true)

#### Step4. Blend the result back into the upscaled image.
> Finally, blend the slices of images back into the upscaled image.  
![txt2imghd](https://github.com/wakamenori/txt2imghd-colab/blob/master/gallery/up-scaled_2x_img2img.png?raw=true)
![txt2imghd_diff](https://github.com/wakamenori/txt2imghd-colab/blob/master/gallery/diff.png?raw=true)
####  Step.3 and Step.4 again
> If you select `SCALEUP_RATIO` 4x or 8x and checked `SCALEUP_STEP_BY_STEP`, Step.3 and Step.4 runs again.  
up scale 1024x1024 image to 2048x2048, and chop up-scalled image into 36 pieces then run img2img on every 36 images, then blend them back

## `CUDA out of memory` try these
Not to run out memory,
- Smaller size of the image
- Lower `SCALEUP_RATIO`
- Uncheck `FP32`
- Uncheck `GFPGAN`

## Credits
Colab
- [NSFW Disabled: NOP & WAS's Stable Diffusion Colab v0.35 (1.4 Weights)](https://colab.research.google.com/drive/1jUwJ0owjigpG-9m6AI_wEStwimisUE17#scrollTo=Ucr5_i21xSjv)

Reddit
- [txt2imghd: Generate high-res images with Stable Diffusion](https://www.reddit.com/r/StableDiffusion/comments/wxm0cf/txt2imghd_generate_highres_images_with_stable/)

Github
- [txt2imghd](https://github.com/jquesnelle/txt2imghd)
- [Real-ESRGAN](https://github.com/xinntao/Real-ESRGAN)
- [GFPGAN](https://github.com/TencentARC/GFPGAN)

