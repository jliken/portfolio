---
title: "2025 Internship"
description: "2025 extragalactic physics internship."
pubDate: "May 28 2026"
heroImage: "/projects/engineering/asi5-pic.png"
blurb: "Spectroscopically measured physical properties of mid-redshift galaxies."
tag: "phys"
---

In the midst of finishing up my [Bachelor's Project](https://jliken.co.uk/projects/bachelors/), I wanted to perform more extragalactic research - focusing on spectroscopy instead of photometry. I was accepted for the University of Edinburgh's Physics & Astronomy Career Development Scholarship 2025, for a project focused on measuring the metallicity (concentration of elements heavier than helium) and primary ionisation sources (AGN and/or star formation) for a range of different galaxies. This exploratory project was conerned with galaxies with redshifts greater than 1, with easily-resolvable spectra. Comparing these metallicities and ionisation sources against those of galaxes in our local universe (redshift, z ~ 0) let me investigate trends in galaxy evolution, and test currently leading models.

I had to use galaxy spectra from the HST CLASSY (z < 0.2), JWST EXCELS (0.2 < z < 7.5) & JWST CEERS (1.7 < z < 12.4) surveys, refining the data for resolved spectra and correcting them for extinction of light by galactic dust. The goal was then to measure temperature in different ionisation zones, and oxygen abundances where possible, and then determine metallicity and primary ionisation sources for each galaxy.

Usage of the *PyNeb* package was crucial for this project. By calculating the ratios of different hydrogen Balmer lines, the "colour excess" E(B-V) was determined for each usable galaxy. The temperature of the high ionisation zone in each galaxy was calculated using emission lines of doubly-excited oxgen. The temperatures of the medium and low ionisation zones could then be inferred with empirical relations, using the high-ionisation temperature. Oxygen abundance, which was later used to calculate metallicity, were calculated using these temperatures and other oxygen emission lines. The primary ionisation source was then determined through empirical relations between emission lines of oxygen and nitrogen. The stellar mass and star formation rate (SFR) of each galaxy was supplied using [BAGPIPES](https://bagpipes.readthedocs.io/en/latest/). The mass-metallicity relation (MZR) and fundamental mass-metallicity-SFR relation (FMR) could then be plotted and compared to local-universe trends.

Temperatures for 70 galaxies were measured, resulting in 49 successful metallicity measurements. Primary ionisation sources could be determined for 35 galaxies, shown below. Star-forming galaxies are below both curves, AGN are above both curves, and composite sources are between the curves.

[INSERT FIG]

The number of stellar mass measurements by BAGPIPES was limited, meaning only a small portion of (star-forming) galaxies could be used to analyse the MZR and FMR in this project. SHown below is the MZR. The low-redshift population of CLASSY galaxies is fitted with a different gradient to the higher-redshift EXCELS population. This implies some deviation from the expected low-redshift MZR of higher redshifts (but this conclusion is questionable given the five high-redshift datapoints). 

[INSERT FIG]

The plot of the FMR of available galaxies is shown below. A fully technical analysis of this plot is beyond the scope of this post, but the conclusion was that this data does not deviate significantly from the expected FMR for solely low-redshift galaxies.

[INSERT FIG]

While the final conclusions of this research internship weren't particularly ground-breaking, the updated catalogue of temperatures and metallicites from this project is valuable. Furthermore, the extra research experience (and exploration of spectroscopic analysis) allowed me to develop my professional skills and interests considerably. This internship went on to serve as the basis for a Master's project the following year.
