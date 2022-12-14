## Road Damage Detection & Classification

### Intro
This project is my final research works to detect and classify road damage, processing the detected object with matemathical equation to find a real size, so we can determine th elevel of road damage based on SDI (Surface Distress Index) method. In this part, lets just goes down into the detection model and prediction in real-time condition process

### The Objective
Why road damage detection? It takes a huge amount of time, resources, and cost to conduct a Road Survey for the repairing process based on a manual method these days, especially in Indonesia. With the hands of technology, it hopes the efficiency of the survey process is increased so that the damaged road will be taken care of more quickly and more precisely

### The Data
The image datasets using RoadDamageDataset for GRDCC 2020 contain Japan, India, and Czech road images. To broaden the insight of datasets that relate to road 
infrastructure in Indonesia, road image survey results from the Directorate of Highways of the Public Works and Housing of Gresik Region are also used. All the images is manually annotated with Pascal VOC format

- Total images : 18758 (640 x 480) 
- Label : 44% longitudinal crack, 37% alligator crack, 15% photole, and 4% shadow

### The Model
The modeling approach makes use of the TensorFlow Object Detection API using Convolutional Neural Network SSD MobileNet V2 pre-trained model. SSD is used because of its lightweight single shot detector, and also mobilenet V2 with its bottleneck block function to reduce computation while still managing the accuracy. The Hyperparameter optimization is conducted by using different batch sizes (8, 4, 2), and the training is done until 50K steps.


The data also tested in Resnet50 pretrained model with same hyperparameter for the comparison
