---
title: "CANDELS: CNN Redshifts"
description: "Searching the HST CANDELS survey"
pubDate: "Apr 15 2026"
category: "physics"
heroImage: "/projects/physics/candels-image.png"
---
### Introduction

Having <a href="/projects/physics/borg">searched the BoRG catalogue</a> for high-redshift galaxies, but come across the issue of individual/scientific biases in galaxy redshift prediction, my research year with the University of Melbourne took an unexpected direction: using convolutional neural networks (CNNs) on HST/JWST (i.e., space telescope) imaging to automate galaxy redshift prediction, and reduce human interference. Why use space-based imaging instead of ground-based imaging? Well, ground-based telescopes cannot image in the infrared spectrum, due to atmospheric absorption, but the key features used to measure high redshifts are in the infrared spectrum. This is why space telescopes are commissioned to find high-redshift galaxies! 

What are convolutional neural networks, though? Simply put, they're complex and self-evolving statistical algorithms, which closely model relationships in datasets using images. Once a CNN has developed a model, it can be used on multi-wavelength images of a galaxy to predict its redshift, based on relationships in the data it has found to be useful. Neural networks, in general, need a large dataset of known redshifts to be able to predict redshifts by itself - imagine trying to play a song on guitar without knowing any chord shapes! The CNN learns to predict redshifts without human interference, and can also be upscaled to automatically handle as much data as required - unlike humans which require lots of time (and money) to do so. This is great in today's scientific landscape, where better telescopes produce enormous quantities of data.

Now, the task of predicting high galaxy redshifts using loads of HST/JWST data and an advanced CNN is a very big task - I needed somewhere simpler to start. I started with the HST CANDELS dataset, and a fairly simple (yet effective) CNN to predict a small sample of low galaxy redshifts. From here I could build up towards that monumental goal.

![Galaxies in HST CANDELS](/projects/physics/candels-galaxies.png)

Above we can see three galaxies imaged in the CANDELS survey, at a wavelength of 814 nanometres - in the infrared spectrum. You can clearly see some sub-structure in the galaxy, and the redshifts (z) are below 1.5.

Some key problems I encountered during this project were:

1) Matching the positions of galaxies with known redshifts, to the image data.
2) Making sure that each galaxy was imaged in each of six wavelengths: 606nm, 814nm, 850nm, 1050nm, 1250nm, and 1600nm.
3) Handling variable image resolutions across different images.
4) Artificially removing secondary (background) galaxies from each galaxy image.
5) Expanding the very small dataset to improve CNN performance.


### Finding "Good" Galaxies
First I dealt with problems 1) and 2). I downloaded a catalogue of all galaxies imaged in the CANDELS survey, that had confirmed spectroscopic redshifts (very accurate measurements). Most of the patches of the survey were not imaged in all six wavelengths, aside from the "Goods-South 33" patch - so I removed all galaxies that weren't in this patch. Then I used Source Extractor to extract the positions of all galaxies in each image, so that I could extract my own images later. However, the catalogue and Source Extractor positions rarely matched - in the end I had a total of 77 galaxies with confirmed redshifts + imaging in all wavelengths.


### Image Processing
Despite the small dataset, I pushed on and developed my own complex image processing pipeline. For each galaxy, in each wavelength, I:

 - Extracted a small portion of the image containing the galaxy - a "postage stamp", using the _astropy.io.fits_ Python package.
 - Created a "mask" of all pixels in the image that were in the top 10% of brightness, and which were in groups of 20 or more. This used the _skimage.measure_ Python package.
 - Identified the central galaxy in the image, and the pixels involved in background galaxies. Then I could re-centre the image on the central galaxy.
 - Replaced the background galaxies with image noise sampled from the rest of the image.
 - Scaled the image to a standard resolution.

This set of actions solved problems 3) and 4): you can see the difference in the image below!

!["Cleaned" image of a galaxy](/projects/physics/candels-cleaned-stamp.png) 


### CNN Pipeline
The CNN would need a much larger dataset than 77 galaxies to meaningfully learn any relationships in the data - see problem 5). I chose to artificially expand the dataset by rotating each image three times, so that my resulting dataset was 4x larger! I could have tried other things, like adding fake noise to images, or creating my own fake galaxy images (which I ended up doing later in the year), but this was an exploratory project. I developed the CNN using the _tensorflow_ and _keras_ frameworks in Python, with the former being a pretty accessible way to make neural networks.

I could list the full CNN architecture here, but I don't think that's a good use of anyone's time. The important technical details are that I had three convolutuional layers with ReLU activation function, two MaxPooling layers and a 25% dropout layer. I used the _adam_ optimiser, and a loss metric of mean squared error. 

That latter point is important - the MSE loss function. This means that the CNN is encouraged to learn relationships that result in a loss in MSE. MSE is the squared difference between the true and predicted redshifts, which gets smaller as this difference is minimised. So I was telling the CNN "Reduce the (squared) difference between your predicted redshifts and the true redshifts as much as possible". This resulted in the following graph:

![CNN loss graph](/projects/physics/candels-cnn.png)

The important thing to focus on here is the orange line - the "validation loss". The validation group is a fraction of the original dataset, that is not used to train the CNN, but rather to test it. The CNN evaluates its performance on this dataset, then determines which learned relationships were good or bad. We can see the validation loss (MSE) converge to a value of ~0.12 over time. The fact that this value is less than 10% of the maximum true redshift (z=1.5) means that the CNN is a pretty alright predictor of low galaxy redshifts!

