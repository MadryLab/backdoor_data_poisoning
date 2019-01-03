# Backdoor Attacks on CIFAR10

This is a simple Resnet for CIFAR implementation supporting the detection of
backdoor attacks with spectral signatures.


- `train.py` trains
- `eval.py` evals once (`--loop` flag for infinite loop)
- `config.json` has all the options
- `compute_corr` performs the spectral signature detection


The simplest usage is to change the "data" section of the config.json file.
Method supports 'pixel', 'ell', and 'pattern'.
An eps number of clean label images are marked according to the position and
color values and mislabelled as the target label.
Percentile indicates how many images will be kept after the scores are computed.
The compute corr file will load the latest checkpoint from the given output 
directory in the config file and perform the spectral signature detection.
The code will print (to stdout) the top singular values with and without
the corrupted inputs, as well as the number of corrupted images removed as
having a high score.
The model directory is then updated with a numpy file containing the indices
of the top scores, so that if the train file was run again, the model would 
be trained without training inputs corresponding to the removed indices.
