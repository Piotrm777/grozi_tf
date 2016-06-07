## Using TensorFlow for CNN's for recognizing *in situ* groceries

Welcome!

This repository houses all work towards using TensorFlow and other CV tools to recognize *in situ* groceries at a particular store (Mattin's, the store located in Duffield Hall at Cornell). All work here was done during the summer of 2016 under the instruction of Dr. Serge Belongie.

### Notes:
These are all in reverse chronological order to keep track of recent updates more easily.

####6/7/15
Now working on using TF to build a network that recognizes Tide on the shelf, as mentioned in the second current task. To do so, I'm essentially using the code available from TensorFlow's repo using CNN's with the CIFAR-10 dataset, and modifying it to work on images that either do or do not have Tide. To do so, the images in my dataset need to be reshaped to be 32 x 32. Then, they need to each be flattened, and the associated label byte should be added to the front of the flattened image information, as mentioned on this [page](http://stackoverflow.com/questions/35032675/how-to-create-dataset-similar-to-cifar-10/35034287).

####6/1/15
Update to the error from the very beginning - it turns out that the installation page on [Tensorflow](https://www.tensorflow.org/versions/0.6.0/get_started/os_setup.html#pip_install) has an outdated version. I installed the 0.8.0 version of TensorFlow, and now all dependencies are there, and the file that works with MNIST data works as detailed in the tutorials.

####5/29/15
Figured out why the error kept coming up: the input_data Python file, and the associated imports necessary, are all in a different directory in the TensorFlow soure code (i.e. from their Github), and was not installed through pip. I tried working around that by cloning their repo locally, but that won't work unless I move the relevant files into the folder of my local installation of TensorFlow, which brings up the problem of duplicate folder names. 

As a result, if I were to change those, I'd have to go through almost all of their source code and fix up the import statements based on my own changes, so I'm choosing to just skip this for now, at least until it proves to be an impasse. At the moment, everything else works (in the scope of everything that I've tried/ran so far), so I'll just continue working with the framework, and hopefully, this won't pose a problem over the course of the summer.

####5/25/15
The tf_tutorial.py file is not working: when run, the following error occurs:
```
Traceback (most recent call last):
  File "tf_tutorial.py", line 1, in <module>
    import tensorflow.examples.tutorials.mnist.input_data
ImportError: No module named examples.tutorials.mnist.input_data
```
I tried running the input_data.py file to work around that, but that doesn't work as well, giving the following error:
```
Traceback (most recent call last):
  File "input_data.py", line 29, in <module>
    from tensorflow.contrib.learn.python.learn.datasets.mnist import read_data_sets
ImportError: No module named contrib.learn.python.learn.datasets.mnist
```
Currently, I'm working on fixing this.

### Table of Contents

[Current Tasks](https://github.com/dthiagarajan/grozi_tf#current-tasks)

[Completed Tasks](https://github.com/dthiagarajan/grozi_tf#completed-tasks)

[Project Description](https://github.com/dthiagarajan/grozi_tf#project-description)

1. [Introduction](https://github.com/dthiagarajan/grozi_tf#introduction)
2. [Data and Methodology](https://github.com/dthiagarajan/grozi_tf#data-and-methdology)
3. [References](https://github.com/dthiagarajan/grozi_tf#references)


### Current Tasks
1. Become familiar with relevant computer vision tools, find other relevant application studies, and build up related work section of proposal based on this.
2. Pick one product from GroZi-120 (easiest choice would be Tide), and use TF (training and testing) to detect it in 20 shelf images, where half contain Tide, and half don't.
3. Pick a product that isn't as easily distinguished, and use TF to do the same thing again.
4. Collect data from Mattin's for actual training.

### Completed Tasks

### Project Description
#### Introduction
As the need for assistive technology for the visually impaired becomes more prominent and feasible with the use of machine learning, we revisit the problem of using pictures of objects taken in ideal conditions to recognize more common scenes of these same objects. This problem encompasses several possible applications, but in this study, we will specifically look at grocery products sold in Mattin's. In essence, we will revisit the study conducted by Merler, Galleguillos, and Belongie, but with a more modern approach involving the tools contained in TensorFlow. 

The main problem we hope to address by conducting this study is paramount to maintaining the state of assistive technology: ideally, training data and testing data would be obtained from the same distribution of data. However, in real-world application, it is more convenient to obtain training data from more well-kept databases, such as the web or dedicated databases. As a result, using the tools offered in TensorFlow, we intend to design a portable system that can recognize the groceries in Mattin's, trained on images taken from both an ideal and realistic environment.

Specifically, the purpose of this study will be to build a database of images encompassing the inventory of Mattin's ranging from ideal to realistic shots, as well as to use various approaches to actually recognize the grocery products in Mattin's. This will include color histogram matching, SIFT matching, compared with training a neural network that takes image pairs as input (where the image pair consists of an ideal and realistic shot of a grocery object in Mattin's) for classification.
#### Data and Methdology
To begin, we will need to obtain the relevant types of data for input. As mentioned in the previous study, one database that can be used is the (http://grozi.calit2.net/grozi.html - GroZi-120 database), which is a database of 120 products with images of objects, ranging over various attributes of the image, and where each product has two different representations: either \textit{in situ}, i.e. in a realistic environment, or \textit{in vitro}, i.e. in an idealistic environment. Another possible way to scrape data could be to use Google searches, and take a sample of the top image hits as training/test data.

Additionally, data would be obtained from Mattin's in person, and due to the changing inventory, images and videos can be taken periodically of each product in the whole inventory to better recognize the inventory, given the varying nature of the products sold. To better train the network being used, photos and videos taken in person will vary in scale and lighting to simulate a more realistic environment.

Once the relevant data has been obtained, it will be used independently on each localization and recognition algorithm, as well as arranged into pairwise input to be used for training on a convolutional neural network built in TensorFlow. Specifically, we will build a sample of several neural networks built in TensorFlow (which will be chosen from the set of all possible networks by using distinctive heuristics) and see how they perform compared to each other on various samplings of training and testing data. Once we have selected the network that performs best, we will compare the results of the standard algorithms with the new accumulation of data to the results in the previous study, as well as comparing how the chosen network built in TensorFlow performs compared to other algorithms on the new accumulation of data.
#### References
Merler, Michelle; Galleguillos, Carolina; Belongie, Serge. *Recognizing Groceries in situ Using in vitro Training Data*. SLAM, Minneapolis, MN, 2007.