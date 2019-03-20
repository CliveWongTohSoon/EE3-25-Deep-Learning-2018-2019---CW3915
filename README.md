# Introduction
This is a repository for Imperial College London Deep Learning coursework (2018-2019). The dataset is N-HPatches (Noisy HPatches) which can be found [here](https://github.com/MatchLab-Imperial/deep-learning-course). Utility functions are also used, which is provided [here](https://github.com/MatchLab-Imperial/keras_triplet_descriptor). 

# Instruction to execute the source code
The source code is attached in this repository, which you can download from this repository or view it on <a href="https://colab.research.google.com/github/CliveWongTohSoon/EE3-25-Deep-Learning-2018-2019-CW3915/blob/master/cw3915_DL.ipynb" target="_blank">Google Collab </a>. You will need Jupyter Notebook with Python 3 and above to execute the code. 

## 1. Set up Google Drive
You will need a Google Drive to execute the code, as this code is intended to run on Google Collab environment and data will be persisted on Google Drive. 
## 2. Temporary fix for broken keras implementation of ResNet and InceptionV2. 
At the time of working on this courserwork, the implementation of ResNet and InceptionV2 in keras is broken. Reference can be found [here](https://github.com/keras-team/keras/issues/11927). Therefore, a temporary fix is needed, which is to run the following patches:
```
!pip install -U --force-reinstall --no-dependencies git+https://github.com/datumbox/keras@fork/keras2.2.4
!pip install -U --force-reinstall --no-dependencies git+https://github.com/datumbox/keras@bugfix/trainable_bn
```
## 3. Clone dataset and utilities functions
As mentioned in the introduciton, the dataset and utility function is provided by Imperial College London, running the following lines:
```
# Clone repo
!cd /content/gdrive/My\ Drive; git clone https://github.com/MatchLab-Imperial/keras_triplet_descriptor
# change directory
%cd /content/gdrive/My\ Drive/keras_triplet_descriptor 
# Initial set up
!wget -O hpatches_data.zip https://imperialcollegelondon.box.com/shared/static/ah40eq7cxpwq4a6l4f62efzdyt8rm3ha.zip
# Extract data
!unzip -q ./hpatches_data.zip
!rm ./hpatches_data.zip
```

## 4. Training
You can create your own Keras model. For denoise model, it is straight forward: build your model, compile them, fit data into the model and train. Example can be found in Section 3.1. 

For descriptor model, I have written a wrapper function `load_descriptor_model` which takes in your descriptor model, and an optional `pretrained_model`, which will generate tuple of `descriptor_model_trip` and `descriptor_model` using triplet loss as the loss function. `descriptor_model_trip` will be used for training, and `descriptor_model` will be used for verification, matching and retrieval (VMR) tasks later on. 

## 5. Evaluation
A wrapper function `run_vmr` is also written, which takes input of `path_dir`, `descriptor_model` and `denoise_model`. `path_dir` is the path the utility function provided will generate the output for executing (VMR). `descriptor_model` and `denoise_model` are self-explanotary, which takes your defined descriptor model and denoise model respectively. 

