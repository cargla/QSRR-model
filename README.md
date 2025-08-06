# QSRR Model

This repository provides a Python implementation of a Quantitative Structure–Retention Relationship (QSRR) model for gas chromatography. The goal is to establish a relationship between molecular structure and Kovats retention index using physicochemical descriptors derived from SMILES. This approach supports retention index prediction and can assist in the identification of unknown compounds in GC-MS analyses.

---

## Repository Structure
<pre> qsrr-model/ 
   ├── data/ # Database (SMILES + RI) 
   ├── notebooks/ # Jupyter notebooks for training, prediction, comparison 
   ├── src/ # Python scripts (model functions, utilities) 
   ├── environment.yml # Conda environment file 
   ├── README.md # Project documentation 
   ├── LICENSE # Project license (MIT) 
   └── .gitignore # Files/folders ignored by Git </pre>


---

## How to Use This Repository

This project provides a QSRR-based model to predict Kovats retention indices (RI) from molecular structures, with an integrated workflow for GC-MS data processing and RI normalization using alkane standards.

---

### 1. Set Up the Environment

We recommend using **Conda** to ensure compatibility with RDKit:

```bash
# Create a dedicated environment
conda create -n qsrr_env python=3.8
conda activate qsrr_env

# Install RDKit and required libraries
conda install -c conda-forge rdkit
conda install numpy pandas scikit-learn jupyter
```

Then launch Jupyter Notebook:

```bash
jupyter notebook
```

Make sure your environment is active before launching.

---

### 2. RI Calibration and Data Processing
Retention indices were calibrated using a reference mixture of n-alkanes. Retention times were extracted and processed externally (e.g. in MZmine) to compute Kovats indices for all analytes. This process generated the `DTB.csv` file, which contains both the experimental RI values and the corresponding SMILES structures used to build and evaluate the QSRR model. 

### 3. Predict RI from Molecular Structure

1. Go to [NIST](https://webbook.nist.gov/chemistry/) or [PubChem](https://pubchem.ncbi.nlm.nih.gov/).
2. Retrieve the **SMILES** structure of the compound of interest (via InChIKey → Names and Identifiers).
3. Paste the SMILES string into the notebook `QSRR-model.ipynb`.
4. Run all cells to obtain the **predicted RI**.

Make sure to execute all preprocessing steps in the notebook (descriptor calculation, filtering, scaling, etc.).

---

### 4. (Optional) Compare Prediction Models

If the dataset is updated or new descriptors are tested:

1. Open `model-comparaison.ipynb`
2. Run all cells to compare:
   - Cross-validated R²
   - Mean Absolute Error (MAE)
   - Relative prediction error (%)

You can modify the model or descriptor count in the main prediction function within `QSRR-model.ipynb`:

```python
results = prediction(smiles_list, df, n_iterations=300, k=90, model_type="Ridge")
```

Supported models: `"LinearRegression"`, `"Ridge"`, `"PLS"`, `"RandomForest"`

---

## Installation via environment.yml

You can also recreate the environment directly from the provided file:

```bash
conda env create -f environment.yml
conda activate qsrr_env
```

---

## 📄 License

This project is licensed under the MIT License – see the [LICENSE](LICENSE) file for details.

---




