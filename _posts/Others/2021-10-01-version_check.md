---
title: "Version check of Python libraries "
category:
  - Setting
tags:
  - [Setting]
---
How to check version of Python libraries in convinient way?

## Version check of Python libraries  
Plz, see the example code below.  
```python
from numpy import version
import scipy as sp
import numpy as np
import matplotlib as mpl
import pandas as pd
import sklearn as sk
import h5py
import tensorflow as tf
import torch

print('scipy ' + sp.__version__)
print('numpy ' + np.__version__)
print('matplotlib ' + mpl.__version__)
print('pandas ' + pd.__version__)
print('sklearn ' + sk.__version__)
print('h5py ' + h5py.__version__)
print('tensorflow ' + tf.__version__)
print('torch ' + torch.__version__)
```

The results are represented below.(in my case)
```python
scipy 1.7.1
numpy 1.19.5    
matplotlib 3.4.3
pandas 1.3.2    
sklearn 0.24.2  
h5py 3.1.0      
tensorflow 2.6.0
torch 1.9.0+cpu 
```
