# Lung Nodule Dataset Guide

This repository provides tools and code to access and process data from the Lung Nodule Database. The dataset contains 3D nodule images, along with metadata to identify high-quality samples for analysis.

---

## Dataset Overview

The dataset consists of:
- **3D nodule images** stored as `.npy` files in the `cubes_selected/` directory.
- **Metadata** provided in an Excel file (`infoNodul681.xlsx`) to filter and identify high-quality nodule samples.

You can explore the dataset at [Google Drive repository](https://drive.google.com/drive/folders/1hKr88xRUFkZA641HPnG72sk3kWF0KvDS?usp=sharing).

---

## Getting Started

### Prerequisites
Ensure you have the following Python libraries installed:
- `pandas`
- `numpy`

### Directory Structure
Place your data in the following structure:
```
datadirectory/
├── infoNodul681.xlsx          # Metadata file
└── cubes_selected/            # Directory containing .npy files for each nodule
```

---

## Steps to Access the Data

### 1. Load Metadata
First, read the metadata file to access information about the nodules:
```python
import pandas as pd

# Load the metadata file
datadirectory = "path_to_data/"
df = pd.read_excel(datadirectory + 'infoNodul681.xlsx')

# Filter for high-quality nodules (well-centered and low noise)
dfl = df[df.lois.eq(True)]
print(dfl.shape)  # Check the number of selected nodules
nrows, ncols = dfl.shape
```

---

### 2. Read Nodule Images
Use the filtered metadata to load the 3D nodule images:
```python
import numpy as np

# Initialize a list to store the 3D nodule images
nodImag = list()

# Loop through the filtered metadata to load each nodule
for i in range(nrows):
    fname = dfl["idop"].iloc[i]  # Get the file ID
    print(f"> ======= Reading image: {fname}")
    cube = np.load(datadirectory + 'cubes_selected/' + fname + '.npy')  # Load the .npy file
    nodImag.append(cube)  # Add the 3D cube to the list

print("> Images read:", len(nodImag))  # Check the total number of images read
print(nodImag[0].shape)  # Check the dimensions of the first nodule image
```
The output should confirm:
```
328
(32, 32, 32)
```

---

### 3. Extract a Flattened 2D View
To work with a flattened 2D slice of the 3D data, extract the slice corresponding to a fixed plane (e.g., the 16th plane):
```python
# Initialize a list
opImages = list()

# Loop through the 3D images to extract a 2D slice and flatten
for i in range(nrows):
    lcube = nodImag[i]
    opCube = lcube[16, :, :]  # Extract the 16th slice (Longitudinal Plane)
    opCube = opCube[0:32, 0:32]  # Ensure the slice is square (32x32)
    opCube = np.reshape(opCube, 1024)  # Flatten the 2D slice into a 1D vector of size 1024
    opImages.append(opCube)

# Combine the list of flattened slices into a 2D NumPy array
sampleImg = np.array(opImages, dtype="uint8")
print(sampleImg.shape)  # Should output: (number_of_images, 1024)
```

Output:
```
(328, 1024)
```

---

## Notes
- Each 3D nodule image is stored as a `.npy` file with dimensions `(32, 32, 32)`.
- Filtering the dataset based on the `lois` column in the metadata ensures that only high-quality nodules are processed.
- The 16th slice of each nodule is used for 2D analysis, flattened into a vector of size `1024`.

---

## Example Applications
- **3D Analysis**: Use the full 3D cubes (`nodImag`) for volumetric studies.
- **2D Analysis**: Use the 2D slices (`sampleImg`) for simpler models.

---


