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
   Noise-contaminated pixels are identified using a pretrained classification model (Spectra X+).
2. **Mask Generation**  
   A corresponding noise mask is generated to mark unreliable pixels.
3. **Pixel Exclusion**  
   Instead of correcting noisy pixels, the method excludes them from spectral extraction.
4. **Spectral Extraction**  
   The final one-dimensional spectrum is computed using only reliable pixels.
This approach avoids introducing artificial signals and improves the reliability of spectral analysis.

## Sample Data and Model
This repository provides:

	•	a partial training subset for SpectraX, including example spectral images and corresponding annotations;
   
	•	a partial training subset for YOLO, including example images and labels for noise localization;
   
	•	selected pretrained model weights, intended for demonstration and basic evaluation.

The SpectraX subset is used to illustrate the annotation structure and noise-classification workflow, while the YOLO subset is provided to show how object-detection-based training data are organized.

To simplify usage, only representative samples and partial pretrained models are included in this repository. The full training datasets, complete model weights, and the full training pipeline are not part of this release.

This setup is intended to present the data structure, labeling format, and core idea of pixel-level noise exclusion without disclosing the entire project resources.


## Data Organization

This repository includes two types of data folders:

### annotations (YOLO)

This folder contains **YOLO-style annotation data** for noise localization.

- Images: spectral image patches  
- Labels: corresponding YOLO-format annotation files (bounding boxes of noise regions)  
- Overlay: visualization images showing annotated noise regions  

These data are used for **object detection tasks**, where the goal is to locate noise regions in spectral images.


### Datasets (CNN)

This folder contains data used for training the **Spectra X+ classification model**.

- Noisy samples: patches containing noise  
- Clean samples: noise-free patches  

These data are used for **classification tasks**, where the model determines whether a given patch is noisy or not.

**Note:** This folder provides only a **representative subset of the dataset**, rather than the full training data.


## Model 1

### Spectra X+ (CNN)

Spectra X+ is a convolutional neural network designed for **noise classification** in spectral images.

Given an input spectral patch, the model predicts whether the patch is **noise-contaminated** or **noise-free**. This classification result is further used to generate noise masks for pixel-level noise exclusion.

A pretrained model is provided in the `models_CNN` folder for demonstration and inference purposes.
Example result for a clean spectral patch:

<img width="890" height="91" alt="Screenshot 2026-03-26 at 7 22 56 PM" src="https://github.com/user-attachments/assets/0d55941e-3537-4264-b318-e82cb166908d" />

**Note:** The model weights included here represent a **partial pretrained version**. The full training configuration and complete model weights are not part of this repository.

## Model 2
### YOLO (Detection / Segmentation)

YOLO is used for **noise localization** in spectral images.

Given an input spectral image, the model identifies noise regions and produces segmentation masks. The results can be represented in multiple forms:

- **Binary mask**: pixel-level segmentation of noise regions  
- **Overlay visualization**: noise regions highlighted on the original spectral image  
- **Coordinate outputs**: exported pixel coordinates of detected noise regions (CSV format)  

Example results are provided to illustrate the segmentation performance, including predicted masks and overlay visualizations.

**Note:** The model and outputs provided here represent a **partial demonstration**. The full training pipeline and complete datasets are not included in this repository.
#### Example Segmentation Results

The figure shows representative segmentation results of noise regions predicted by the YOLO model.

The left image presents the **binary mask**, where white pixels indicate the detected noise regions and black pixels represent background.

The right image shows the **overlay visualization**, where the detected noise regions are highlighted on the original spectral image, enabling intuitive inspection of the localization accuracy.

These results demonstrate that the model can accurately identify sparse and irregular noise artifacts while preserving the underlying spectral structure.

<img width="128" height="128" alt="pred_mask_all" src="https://github.com/user-attachments/assets/d667826c-183d-4bd0-b83d-477936a7e13f" />
<img width="128" height="128" alt="pred_overlay_solid" src="https://github.com/user-attachments/assets/ecb1495d-12f1-4db5-a82d-9dcb94946ca1" />

## Deployment in Apple Xcode Projects
We are actively integrating the Spectra X model into our Apple Xcode-based applications. The model is continuously updated and maintained as part of our ongoing development.

For more information, please visit our GitHub repository:

## Open-Source and Project Integration

The proposed method has been integrated into a practical application and is under continuous development and optimization.

Due to its integration with real-world projects, certain components — including the full training datasets, complete model weights, and the full training pipeline — are not publicly released. The materials provided in this repository, including the methodology, sample data, and partial pretrained models, are intended to support understanding and reproducibility of the core approach.

The models are actively maintained and further applied to real spectral data analysis tasks.






