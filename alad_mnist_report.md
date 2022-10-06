# ALAD MNIST Report
In this report, I explained how change the base code to add MNIST dataset to the ALAD model training and inference phase. To run current code, I used the libraries below:
```
tensorflow-gpu==1.15
keras==2.8.0
numpy==1.21.6
urllib3==1.24.3
matplotlib==3.2.2
seaborn==0.11.2
scikit-learn==1.0.2
opencv-python==4.6.0.66
gensim==3.6.0
pillow==7.1.2
regex==2022.6.2
```

# Modifications
For modification of this base project, I've used some files from another repo of `houssamzenati` in [this link](https://github.com/houssamzenati/Efficient-GAN-Anomaly-Detection/). In this repo, they have implemented a prior work of ALAD and used MNIST dataset to test it. the structure of the current code is the same as another repo, so I used some of files in the another repo to add supporting MNIST dataset for ALAD model.

## Adding Dataset Loader
- `data/mnist.npz`
- `data/mnist.py`
- ‍‍‍‍`utils/adapt_data.py`

## Modification to force using GPU
- `alad/run.py`

## Adding ALAD model adapted with MNIST
- `alad/mnist_utilities.py`

## Add to CLI Interface
- `main.py`

# Model Outputs
## Train Phase
### Model Specification
- Batch size:  `32`
- Starting learning rate:  `0.0002`
- EMA Decay:  `0.999`
- Degree for L norms:  `1`
- Anomalous label:  `0`
- Score method:  `fm`
- Discriminator zz enabled:  `False`
- Spectral Norm enabled:  `False`

### Epoch-Loss
|Epoch|Time|Gen Loss|Enc Loss|Dis Loss|Dis(xz) Loss|Dis(xx) Loss|
|---|---|---|---|---|---|---|
| 0 | 143s | 6.8177 | 6.9313 | 1.3852 | 0.3451 | 1.0401 | 
|1 | 139s | 6.5120 | 6.6248 | 1.4836 | 0.3856 | 1.0980 | 
|2 | 139s | 6.2576 | 6.5781 | 1.5159 | 0.4188 | 1.0970 | 
|3 | 139s | 6.4489 | 6.5697 | 1.4994 | 0.4101 | 1.0893 | 
|4 | 139s | 6.2339 | 6.3903 | 1.5470 | 0.4338 | 1.1132 | 
|5 | 138s | 6.2133 | 6.3076 | 1.5629 | 0.4261 | 1.1368 | 
|6 | 138s | 6.1597 | 6.3843 | 1.5720 | 0.4192 | 1.1528 | 
|7 | 139s | 6.2620 | 6.4314 | 1.5641 | 0.4062 | 1.1579 | 
|8 | 139s | 6.3937 | 6.5163 | 1.5561 | 0.3973 | 1.1588 | 
|9 | 139s | 6.3507 | 6.4825 | 1.5934 | 0.4107 | 1.1827 | 


## Test Phase
|Testing Step|Method|Precision|Recall|F1 score|
|---|:-:|---|---|---|
|Testing at step 17346| ch | 0.3400 | 0.8653 | 0.4881|
|Testing at step 17346| l1 | 0.3929 | 1.0000 | 0.5641|
|Testing at step 17346| l2 | 0.3929 | 1.0000 | 0.5641|
|Testing at step 17346| fm | 0.3928 | 0.9997 | 0.5640|
