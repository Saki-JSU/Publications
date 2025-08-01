# STransfer
# **STransfer: A Transfer Learning-Enhanced Graph Convolutional Network for Clustering Spatial Transcriptomics Data**


## **Table of Contents**
1. [Requirements]
2. [Data process]
3. [Model Initialization]
4. [Visualization]
5. [File Description]
6. [Example Workflow]

---

## Requirements

### ○ Required Python Packages

○ torch (2.4.0+cu118)  
○ scanpy  
○ pandas  
○ numpy  
○ scikit-learn  
○ scipy  
○ matplotlib  

---

## Data process

Due to upload size restrictions, we only provide pre-trained model parameters for each dataset.  
As an example, we briefly introduce the usage of the **DLPFC** dataset below.

During data preprocessing, both the **source** and **target** domain datasets must be processed simultaneously, which involves selecting highly variable genes and constructing graph-based networks:

```python
adata_s, data_s, labels_s, graph_dict_s = preprocess_slice_DLPFC(slicename_s, data_dir, device, label_mapping, n_top_genes)
adata_t, data_t, labels_t, graph_dict_t = preprocess_slice_DLPFC(slicename_t, data_dir, device, label_mapping, n_top_genes)
```

## Model Initialization
We then initialize the source domain encoder and classifier:

```python
src_encoder = STransferEncoder(input_dim=n_top_genes).to(device)
src_classifier = STransferClassifier(input_dim=64).to(device)
```
And initialize the target domain encoder along with the domain discriminator (critic):

```python
tgt_encoder = STransferEncoder(input_dim=n_top_genes).to(device)
critic = Discriminator().to(device)
```
Model Training
Next, we train the model.
If pre-trained parameters are available, they will be loaded automatically; otherwise, the model will be trained from scratch.

## Visualization
Finally, we will visualizate the results.

## File Description
- `ADDA.py`  
  Implements the Adversarial Domain Adaptation (ADDA) framework used for training on source and target domains,Here, we give the DLPFC as an example.
- `HPR.py`  
  Contains data handling and processing methods for the MERFISH dataset for the mouse hypothalamic preoptic region.
- ` mPFC.py`  
  Contains code for handling and processing the STARmap dataset mPFC.
- `modules.py`  
  Defines core neural network modules, including encoders, classifiers, and discriminators used in the model.
- `params.py`  
  Stores all hyperparameter configurations and command-line argument parsing.
- `utils.py`  
  Includes utility functions such as metrics computation, graph construction etc.
- `train.py`  
  Core training script that integrates data loading, model training, and evaluation loops.

## Example Workflow

<img width="800" height="600" alt="flow17" src="https://github.com/user-attachments/assets/9b87446a-08c8-41ca-be57-ca15c81f1569" />


