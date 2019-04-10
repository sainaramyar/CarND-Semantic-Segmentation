
## Semantic Segmntation

The goad of this project is to label the pixels of the road using fully convolutional networks.
The model consists of the the follwowing functions:

In ```load_vgg``` a pre-trained VGG model is loaded into Tensorflow, and results in layers 3,4,7.
In ```layesr``` the architecture of the FCN is created. In this function, first a 1x1 convolution is performd to preserve the spatial information, and then a decoder is used to updample the input by 2. In this function, all the steps are treamlined, so the output of one layer is the input of the next one.
In ```optimze``` the tensorflow loss and optimizer function (Adam Optimizer) are defined.
In ```train_nn``` the network is trained over several epochs.

This network is trained and tested using the "Kitti Road Dataset". In addition, due to the high computational load, the training and testing is done on an AWS instance.

### Hyper Parameters

This project has the following hyper parameters:
Learning rate, batch size, and number of epochs.

In order to investigate the effect of these parameters on the results, the code is tested with different values:

#### Experiment 1
In this experiment: 

learning rate = 0.0009
epochs = 6
batch_size = 16

In the last epoch, the loss value is around 0.641, and the output images only have green noise. This means the model is not properly trained yet.



```python
import matplotlib.pyplot as plt
import matplotlib.image as mpimg
%matplotlib inline
```


```python
img = mpimg.imread('Try_1_1.png')
print('Output of experiment 1')
plt.imshow(img)
```

    Output of experiment 1
    




    <matplotlib.image.AxesImage at 0x9e5bfd0>




![png](output_5_2.png)


#### Experiment 2

Now, in order to test the effetc of number of epochs, the previous experiment is repeated with 15 pochs. It can be seen that while the labeling performance is far from satisfactory, the network is starting to recognize the road from the environment.

learning rate = 0.0009
epochs = 6
batch_size = 16


```python
img = mpimg.imread('Try_2_1.png')
print('Output of experiment 2')
plt.imshow(img)
```

    Output of experiment 2
    




    <matplotlib.image.AxesImage at 0x9d6dac8>




![png](output_7_2.png)


#### Experiment 3

Now that it can be concluded that a higher number of epochs improves the performance, the effect of bactch size is tested. 

learning rate = 0.0009
epochs = 15
batch_size = 8

With a batch size of 8, the results show that the loss decreases and labeling performance is improved.


```python
img = mpimg.imread('Try_3_2.png')
print('Output of experiment 3')
plt.imshow(img)
```

    Output of experiment 3
    




    <matplotlib.image.AxesImage at 0x9dd0b70>




![png](output_9_2.png)


#### Experiment 4

Now, the experiments are repeated with a smaller learning rate and higher number of epochs. It can be seen that the performance is improved.

learning rate = 0.0004
epochs = 25
batch_size = 8


```python
img = mpimg.imread('Try_4_2.png')
print('Output of experiment 4')
plt.imshow(img)
```

    Output of experiment 4
    




    <matplotlib.image.AxesImage at 0xa1b3668>




![png](output_11_2.png)


#### Experiment 5

In the final experiment, the number of epochs is set to 30, and it can be seen that the labeling performance is improved significantly.


```python
img = mpimg.imread('Try_5_2.png')
print('Output of experiment 4')
plt.imshow(img)
```

    Output of experiment 4
    




    <matplotlib.image.AxesImage at 0xa216160>




![png](output_13_2.png)

