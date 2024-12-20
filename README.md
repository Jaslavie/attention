## Measuring brain activity differences between inhibition and selective attention tasks
Extracting patterns of brain activity between visual attention tasks.

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

Sample return values below:
```
<class 'nibabel.nifti1.Nifti1Image'>
data shape (256, 256, 124)
affine:
[[  -0.859375      0.            0.          110.        ]
 [   0.            0.859375      0.         -110.        ]
 [   0.            0.            1.10000002  -68.20000458]
 [   0.            0.            0.            1.        ]]
metadata:
<class 'nibabel.nifti1.Nifti1Header'> object, endian='<'
sizeof_hdr      : 348
data_type       : np.bytes_(b'')
db_name         : np.bytes_(b'')
extents         : 0
...
srow_z          : [  0.         0.         1.1      -68.200005]
intent_name     : np.bytes_(b'')
magic           : np.bytes_(b'n+1')
```
### Preprocessing
Before running searchlight analysis, we need to clean and standardize the data. The following steps are taken to accomplish this:
1. Resample the data to the MNI template
2. Remove the mean signal from the data
3. Normalize the data by dividing each voxel by the standard deviation
4. Remove motion and signal artifacts

All preprocessing steps are implemented in the `preprocessing.ipynb` file.
### Visualizing the data
To display the data, you must extract the data array and affine matrix, then use nilearn's plotting functions.

### Analysis Method
The goal is to isolate attention-specific neural activity. Located in `glm.ipynb`
- Generalized Linear Model (GLM) extracts patterns of brain activity that represent each task condition.
- Contrast Analysis compares inhibition and selective attention conditions
- Design Matrix visualizes relationship between predictors and brain activity
![Analysis Output](output.png)


### Tools
AWS used for remote storage of data
<br/>
The following OpenNeuro datsets were used:
- [ds004836](https://openneuro.org/datasets/ds003500/versions/1.2.0): Visual Attention


<!-- 

Steps
- fit glm (i.e. design the glm) to return the design matrix
- find m for every predictor r(beta for each predictor) for linear model 
- contrast on betas  
- end goal: get a list of voxels and their corresponding betas for each contrast
- 

-->