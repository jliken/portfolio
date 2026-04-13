---
title: "Searching BoRG"
description: "Searching the HST BoRG survey"
pubDate: "Apr 13 2026"
category: "physics"
heroImage: "/projects/physics/borg-image.png"
---

My research year abroad in Melbourne was split into three parts. This is the first.

The HST BoRG survey searched for high-redshift galaxies by imaging in near-infrared wavelengths. By extracting galaxy luminosities from these images, and carefully filtering the galaxies by a set of selection criteria, four high-redshift galaxy candidates were identified from a pool of 2,500 galaxies. The data processing pipeline for this project included:

 - Correcting pixel weight maps to account for errors in the map production.
 - Dual-image photometry using Source Extractor.
 - Correcting galaxy magnitudes for galactid dust extinction and removal of irregular & non-significant sources.
 - Filtering galaxies for high-redshift candidates.
 - Analysis of redshift probability distributions using EAZY.
 - Generation of galaxy postage stamps (small local images) for visual inspection.

Three examples of high-redshift galaxy candidates are shown in the below image, along with their redshift probability distributions. Visual inspection allowed me to exclude candidates that were clearly image artefacts (e.g., part of a PSF spike from a bright source), while looking at the redshift probability distributions allowed me to select candidates that were confidently high-redshift.

![Source Comparison](/projects/physics/borg-candidates.png)

The left cabdidate passed visual inspection, but not redshift inspection. The middle candidate passed redshift inspection but not visual inspection. The right candidate, while tiny, passed visual inspection and redshift inspection.

A comparison of a candidate's magnitudes and signal-to-noise ratios in different photometric filters (wavelengths) is shown in the below table:

![Candidate data](/projects/physics/borg-data.png)

The measured values are in good agreement with literature values, with comparable errors. This inspires confidence in the data processing pipeline and other candidates. 

It's important to identify high-redshift galaxies, because future work can measure their spectra to measure properties such as chemical composition and temperatures in different regions. This allows us to better understand the evolution of ancient galaxies, which we can add to current theories of galaxy evolution over time. Furthermore, high-redshift galaxies are key suspects for the reionisation of the Universe ~380,000 years after the Big Bang. By investigating these galaxies we might understand the evolution of the Universe better.

However, while seemingly robust, there is a large flaw in the pipeline: it is biased! The selection criteria were chosen based on possibly incorrect theories of galaxy evolution, EAZY uses a biased sample of galaxies to generate redshift probability distributions, and visual inspection is not standardised. The remaining two parts of my year abroad were spent investigating a solution for this: the application of convolutional neural networks directly to the images.
