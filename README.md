# Structural Complexity with Numpy

This repository contains Python code to calculate the structural complexity of images, as defined in the paper: Bagrov, Andrey A., et al. "Multiscale structural complexity of natural patterns" (10.1073/pnas.2004976117).

## Table of Contents
- [Introduction](#introduction)
- [Installation](#installation)
- [Usage](#usage)
- [Functions](#functions)
  - [importImage](#importimage)
  - [catchErrors](#catcherrors)
  - [structuralComplexity](#structuralcomplexity)
- [Example](#example)

## Introduction
This project provides a set of functions to import images, check for errors, and calculate the structural complexity of the images. The structural complexity is computed based on the methodology described in the referenced paper.

## Installation
To use this code, you need to have Python installed along with the following libraries:
- `numpy`
- `matplotlib`
- `cmasher`

You can install the required libraries using pip:
```bash
pip install numpy matplotlib cmasher
```

## Usage
1. **Import the necessary functions:**
   ```python
   from src import importImage, catchErrors, structuralComplexity
   ```

2. **Import an image:**
   ```python
   image = importImage('path_to_image', 'option')
   ```

3. **Calculate the structural complexity:**
   ```python
   complexity = structuralComplexity(image, kLargerThan, kMax)
   ```

4. **Use the Jupyter Notebook:**
   The repository includes a Jupyter Notebook (`notebook.ipynb`) that demonstrates how to use these functions with an example image. You can run the notebook to see the code in action and visualize the results.

## Functions

### importImage
```python
importImage(path, option)
```
This function imports an image from the specified path and converts it to a normalized array based on the selected color channel or intensity.

- **Parameters:**
  - `path` (str): The path to the image file.
  - `option` (str): The color channel to extract ('red', 'blue', 'green', 'intensity').

- **Returns:**
  - `nArray` (numpy.ndarray): The normalized image array.

### catchErrors
```python
catchErrors(image, kLargerThan, kMax)
```
This function checks for errors in the inputs for the `structuralComplexity` function.

- **Parameters:**
  - `image` (numpy.ndarray): The image array.
  - `kLargerThan` (int): The lower bound for the range of scales.
  - `kMax` (int): The upper bound for the range of scales.

### structuralComplexity
```python
structuralComplexity(image, kLargerThan, kMax)
```
This function calculates the structural complexity of the image.

- **Parameters:**
  - `image` (numpy.ndarray): The image array.
  - `kLargerThan` (int): The lower bound for the range of scales.
  - `kMax` (int): The upper bound for the range of scales.

- **Returns:**
  - `C` (float): The calculated structural complexity.

## Example
You can refer to the `notebook.ipynb` file in the repository for an example implementation, including image visualization:
```python
import numpy as np
import matplotlib.pyplot as plt
import cmasher as cms

from src import structuralComplexity, importImage

# Template for importing a .jpeg image
path = 'images/corsica.jpeg' 
imageArray = importImage(path, 'intensity')

# Plot the imageArray
plt.figure(figsize=[5,5], dpi=100)
plt.imshow(imageArray, cmap=cms.prinsenvlag)
plt.axis("Off")
plt.title("imageArray")
plt.colorbar(shrink=0.5)
plt.clim(-1,1)
plt.show()

# Set the range of value $k$ in equation [4] in the paper
kLargerThan = 0
kMax = int(np.log2(imageArray.shape[0])) - 2  # For the full range maximal value

C = structuralComplexity(imageArray, kLargerThan=0, kMax=kMax)

print(f"Structural complexity of the image is: {C.round(3)}")
```
