<h1 align="center">
  <br>
  PastaIQ-TypeDetection
  <br>
</h1>

<h4 align="center">An Image Classifier that Identifies 20 Different Types of Pasta.</h4>

<p align="center">
  <a href="https://github.com/swamilalit/PastaIQ-TypeDetection">
    <img src="https://img.shields.io/github/last-commit/swamilalit/PastaIQ-TypeDetection">
  </a>
  <a href="https://developer.nvidia.com/cuda-downloads">
    <img src="https://img.shields.io/badge/cuda-12.1-blue.svg">
  </a>
  <a href="https://opensource.org/licenses/MIT">
    <img src="https://img.shields.io/badge/license-MIT-yellow.svg">
  </a>

</p>

<p align="center">
  <a href="#-overview">Overview</a> •
  <a href="#%EF%B8%8F-dataset-preparation">Dataset Preparation</a> •
  <a href="#-training-and-data-cleaning">Training and Data Cleaning</a> •
  <a href="#%EF%B8%8F-build-from-source">Build from Source</a> •
  <a href="#%EF%B8%8F-contact">Contact</a>
</p>

## 📋 Overview

An image classification model that utilizes data collection, augmentation, model training, cleaning, deployment to classify 20 different types of pasta. The types are following:

<table align="center">
    <tr>
        <td>1. Spaghetti</td>
        <td>2. Fettuccine</td>
        <td>3. Penne</td>
        <td>4. Rigatoni</td>
        <td>5. Fusilli</td>
    </tr>
    <tr>
        <td>6. Farfalle</td>
        <td>7. Linguine</td>
        <td>8. Tagliatelle</td>
        <td>9. Lasagna</td>
        <td>10. Ravioli</td>
    </tr>
    <tr>
        <td>11. Tortellini</td>
        <td>12. Orecchiette</td>
        <td>13. Conchiglie</td>
        <td>14. Rotini</td>
        <td>15. Bucatini</td>
    </tr>
    <tr>
        <td>16. Cannelloni</td>
        <td>17. Macaroni</td>
        <td>18. Orzo</td>
        <td>19. Cavatappi</td>
        <td>20. Gemelli</td>
    </tr>
</table>

## 🗂️ Dataset Preparation

- **Data Collection:** The code collects images for each pasta type by searching for them using the DuckDuckGo search engine and downloading the images to corresponding folders in the [data](data/) directory. It then verifies the downloaded images and removes any failed downloads.
- **DataLoader:** The code creates a DataBlock, which defines the structure of the data, including the image and label blocks, data splitting strategy, and image transformations. It then creates a DataLoader (dls) using the DataBlock, specifying the path to the data and the batch size.
- **Data Augmentation:** The code applies data augmentation techniques to the images using RandomResizedCrop, which randomly crops and resizes the images to a specified size (224x224) with a minimum scaling factor of 0.5. Additional augmentation transforms are applied using aug_transforms() to further enhance the variety of the training data.

The final dataset has **7.3K+** images of 20 different pasta types. Details can be found in [data_prep.ipynb](notebooks/data_prep.ipynb)

## 💪 Training and Data Cleaning

- **Training:** The model is trained using a **ResNet34** architecture with a 90-10 train-validation split, and fine-tuned for 5 epochs initially, achieving `~75%` accuracy. After data cleaning, the model is fine-tuned for 2 more epochs, reaching `79.5%` accuracy, and then further fine-tuned for 2 epochs, achieving a satisfactory accuracy of `~85.6%`.
- **Data Cleaning:** The `ImageClassifierCleaner` is used to identify and remove irrelevant data points from the dataset. The data points that need to be relabeled are moved to the correct directories, ensuring the dataset's integrity and improving the model's performance.

Details can be found in [training_and_data_cleaning.ipynb](notebooks/training_and_data_cleaning.ipynb). Multiple models from timm (ResNet50, EfficientNet-B0, MobileNetV3-Large) were fine-tuned as well. Details of it can be found in [this](notebooks/training_and_data_cleaning_[extended].ipynb) notebook. **ResNet34** had the best result and this will be deployed in the next step.

<div align="center">
<img alt="Confusion Matrix" src="notebooks/confusion_matrix.png">
<p>Confusion matrix for the final version of fine-tuned <b>ResNet34</b> model</p>
</div>

## ⚙️ Build from Source

### Clone the repo

```bash
git clone https://github.com/swamilalit/PastaIQ-TypeDetection.git
cd PastaIQ-TypeDetection/
```

### Install CUDA Toolkit

- Go to the NVIDIA CUDA Toolkit download page: https://developer.nvidia.com/cuda-downloads
- Select "Windows" as the operating system and choose the appropriate version and installer type.
- Download and run the installer, following the installation instructions.

### Initialize and activate virtual environment

```bash
virtualenv --no-site-packages venv
source venv/Scripts/activate
```

### Install PyTorch with CUDA support

Run the following command to install PyTorch with CUDA support using `pip3`:

```bash
pip3 install torch torchvision torchaudio --index-url https://download.pytorch.org/whl/cu121
```

_Note: Replace `cu121` with the appropriate CUDA version tag that matches your installed CUDA version (e.g., `cu121` for CUDA `12.1`)._

### Verify the installation

Run the following code to check if PyTorch is using the GPU:

```python
import torch
print(torch.cuda.is_available())
```

If the output is `True`, then PyTorch is successfully set up to use the GPU. `torch.cuda.get_device_name(0)` should also show your GPU config.

### Install Dependencies

```bash
pip3 install fastai fastbook nbdev gradio
```

## ✉️ Contact
[![Linkedin Badge](https://img.shields.io/badge/-LinkedIn-blue?style=flat&logo=Linkedin&logoColor=white&link=https://www.linkedin.com/in/lalit-swami/)](https://www.linkedin.com/in/lalit-swami/) [![Gmail Badge](https://img.shields.io/badge/-Gmail-c14438?style=flat&logo=Gmail&logoColor=white&link=mailto:swamilalit2014@gmail.com)](mailto:swamilalit2014@gmail.com)