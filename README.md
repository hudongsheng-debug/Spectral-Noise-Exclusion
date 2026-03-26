# Spectral Noise Removal

We are committed to leveraging the capabilities of mobile platforms such as macOS, iPhone, and iPad for scientific data analysis. In January 2026, we released two applications on the Apple App Store for FITS file visualization and distortion correction.
However, we believe this is only the beginning. From an early stage, we have aimed to introduce AI-based methods into spectral analysis, with the goal of improving the reliability of noise identification and spectral extraction.

## What is this?
This project demonstrates a method for **pixel-level noise exclusion** in fiber spectral images.
Instead of applying traditional denoising, the method:
- Identifies **noise-contaminated pixels**
- Excludes them from spectral extraction
- Preserves the integrity of valid spectral signals

## Key Idea
**Noise-contaminated pixels should be excluded rather than corrected.**

By removing unreliable pixels, the method avoids introducing artificial distortions and improves the stability of spectral extraction.


## How it works
The method follows a simple but effective workflow:
1. **Noise Identification**  
   Noise-contaminated pixels are identified using a pretrained classification model (SpectraX).
2. **Mask Generation**  
   A corresponding noise mask is generated to mark unreliable pixels.
3. **Pixel Exclusion**  
   Instead of correcting noisy pixels, the method excludes them from spectral extraction.
4. **Spectral Extraction**  
   The final one-dimensional spectrum is computed using only reliable pixels.
This approach avoids introducing artificial signals and improves the reliability of spectral analysis.

## Sample Data and Model

A small subset of spectral data is provided in this repository for demonstration purposes.

The noise-contaminated pixel masks are generated using a pretrained classification model (Spectra X). The annotation process follows a standard labeling workflow, where regions of noise are manually annotated using tools such as LabelMe, and then converted into COCO-style format for model training.

Example annotation files (JSON format) and corresponding visualization images are included to illustrate the labeling structure and noise region definition.

To simplify usage, precomputed masks are provided in this repository, and the full training pipeline is not included.

This setup allows users to focus on the core idea of pixel-level noise exclusion without requiring additional model training.


