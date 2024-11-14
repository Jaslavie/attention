## SearchLight Analysis with fMRI data to measure attention levels in candidate brain regions

### Running the application
1. Install dependencies
```
pip install -r requirements.txt
```

2. Run the application
```
python main.ipynb
```

### Data Representation
fMRI data is represented in the following format (NIFTI files):
- Header: metadata about the image including dimensions, voxel size, etc.
- Data: array of integers representing image density of each voxel
- Affine matrix: 4x4 matrix that maps the 2D voxel coordinates to 3D spatial coordinates

### Visualizing the data
To display the data, you must extract the data array and affine matrix, then use nilearn's plotting functions.

### Tools
AWS used for remote storage of data