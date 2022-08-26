---
title: "Installing software"
teaching: 15
exercises: 0
questions:
- "How to install software to ManeFrame II?"
objectives:
- software, tensorflow, pytorch
keypoints:

---


 ## Installing Tensorflow-GPU
 
Here we use 1 node with P100 GPU to do the installation:

Instruction from login node:

```bash
$ srun -N1 -G1 -c10 -p gpgpu-1 --mem=64G --pty $SHELL
$ module load python/3 gcc-9.2
$ module load cuda/11.4.2-dft6rfn cudnn/8.2.4.15-11.4-tfeuowy
$ conda create --prefix ~/tensorflow_2.9 python=3.8 pip
$ source activate ~/tensorflow_2.9/  
$ pip install tensorflow==2.9.1 --no-cache-dir
$ pip install ipykernel
$ python3 -m ipykernel install --user --name tensorflow_2.9 --display-name TensorflowGPU29
```

Once installation done, check if tensorflow can find any GPU?
  
  ```bash
  $  python
  >>> import tensorflow as tf
  >>> tf.config.list_physical_devices('GPU')
  [PhysicalDevice(name='/physical_device:GPU:0', device_type='GPU')]
  ```
  
  
