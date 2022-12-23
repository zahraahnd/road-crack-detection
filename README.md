## Road Damage Detection & Classification

### Intro
This project is my final research works to detect and classify road damage, processing the detected object with matemathical equation to find a real size, so we can determine th elevel of road damage based on SDI (Surface Distress Index) method. In this part, lets just goes down into the detection model and prediction in real-time condition process

### The Objective
Why road damage detection? It takes a huge amount of time, resources, and cost to conduct a Road Survey for the repairing process based on a manual method these days, especially in Indonesia. With the hands of technology, it hopes the efficiency of the survey process is increased so that the damaged road will be taken care of more quickly and more precisely

### The Data
The image datasets using [RoadDamageDataset for GRDCC 2020](https://github.com/sekilab/RoadDamageDetector) contain Japan, India, and Czech road images. To broaden the insight of datasets that relate to road 
infrastructure in Indonesia, road image survey results from the Directorate of Highways of the Public Works and Housing of Gresik Region are also used. All the images is manually annotated with Pascal VOC format

- Total images : 18758 (640 x 480) 
- Label : 44% longitudinal crack, 37% alligator crack, 15% photole, and 4% shadow

### The Model
The modeling approach makes use of the TensorFlow Object Detection API using Convolutional Neural Network SSD MobileNet V2 pre-trained model. SSD is used because of its lightweight single shot detector, and also mobilenet V2 with its bottleneck block function to reduce computation while still managing the accuracy. The Hyperparameter optimization is conducted by using different batch sizes (8, 4, 2), and the training is done until 50K steps.

<img src="https://user-images.githubusercontent.com/87270138/207533766-c8639f7d-afb7-4b0b-87e9-7242e6b93cc7.jpg" width=40% height=40%>

The data also tested in Resnet50 pretrained model with same hyperparameter for the comparison

### The Result
| Model | Batch Size | mAP | AR | Total Loss |
|:-----:|:----------:|:---:|:--:|:----------:|
|SSD Mobile Net V2|8|0.086902|0.241|1.075|
|SSD Mobile Net V2|4|0.0732|0.2853|0.9778|
|SSD Mobile Net V2|2|0.071015|0.233|1.032|
|SSD Resnet50 V1|8|0.0838|0.225|0.9718|

From the table above, we can see that The smaller the batch size value, the higher the loss is obtained. However, this does not imply that a large loss can obtain a better model that is adapted to the dataset's conditions and the amount of memory used. Because the dataset, in this case, is quite complex, choosing a batch size that is small enough can save memory allocation while also producing better convergence. While a batch size of fewer than 8 results in lower loss and accuracy, a batch size of 8 is the ideal batch size value in this model. Compared to the Resnet50 V1 model, the total loss seems to be lower than Mobilenet V2, but also a lower mAP as well. In this case, SSD Mobile V2 is more considered to implement in real-time condition due to the lightweigth and compatible to be inferenced in hardware.

### The Output
- Validation result -- Detected as pothole (L00 label)
<img src="https://user-images.githubusercontent.com/87270138/207591976-38859307-4f74-4dbc-a71d-ea20684d0a2f.PNG" width=40% height=40%>

- Inference result in real condition

<img src="https://user-images.githubusercontent.com/87270138/209289124-1cca4894-ff8e-4424-8ad9-ca54ade135e8.jpg" width=25% height=25%><img src="https://user-images.githubusercontent.com/87270138/209289249-0c24c859-1588-45d4-a89e-996e740a8724.jpg" width=25% height=25%>

<img src="https://user-images.githubusercontent.com/87270138/209289320-6ad0b737-48f8-4561-aa6b-dc5c304423fd.jpg" width=25% height=25%><img src="https://user-images.githubusercontent.com/87270138/209289335-8788ecaf-51f5-45b7-a987-b0170ee49087.jpg" width=25% height=25%>

___
The trained model is embedded in Jetson Nano with USB Coral Accelerator. The testing process is carried out on a 1 km road by taking pictures using the HD Car View Camera. The detailed information about hardware implementation will not be discussed here, otherwise, we focused more on the post-processing data to extract the prediction result from inference into the calculation process to get the real size of object & defining the level of road damage with streamlit integration for visualization in the next part [here](https://github.com/zahraahnd/road-crack-detection-part2). 
