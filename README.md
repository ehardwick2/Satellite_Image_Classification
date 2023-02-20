# Satellite Image Classification


<p align="center">
  
![image](https://user-images.githubusercontent.com/102127193/219988116-3b1d3e6d-609c-4175-bccf-8958c078c44e.png)

</p>

Classifying land cover satellite images can be useful in a number of situations:
- Classifying the same geographic area on repeatedly over time in a zone that is at risk for illegal timber harvesting or land clear-cutting to make way for farmland.
- Monitoring progress of an area where reforestation is underway following a wildfire. 
- Estimating biomass extents where ground truth evidence is not available.
- Land use planning for commercial timber operations.

Using convolutional neural networks (CNN) and the Keras and TensorFlow libraries, I created a model that classifies satellite images as either containing trees/forested or no trees/not-forested. I tried scratch-built networks and customized pre-trained transfer learning networks using MobileNetV2 and ResNet50. 

## Data
The dataset consists of a balanced, labeled set of 10400 images total with 5200 images in each class (forested, non-forested). Each image is an RGB jpg of 64x64 pixels. The dataset is compiled and available on [Kaggle](https://www.kaggle.com/datasets/mcagriaksoy/trees-in-satellite-imagery). The images are sourced from the European Space Agency’s Copernicus Sentinel 2 mission, which aims at monitoring variability in land surface conditions with a wide swath width (290 km) and high revisit time to support monitoring of changes in the Earth's surface. No additional wrangling or processing of the images was necessary. Exploration of the data included viewing a selection of the images from both classes to get an idea of what types of scenes were included. A selection is displayed below:
<p align="center">
  
![image](https://user-images.githubusercontent.com/102127193/219989806-34a853d7-8ce2-430b-8251-67eaac3ba1fd.png)
  
</p>

## Modeling
First, I explored scratch-built models with various architectures including with varying numbers of convolutional layers, numbers of neurons in the convolutional and dense layers, different activation functions, different optimizers, and different learning rates. I also tried all of the above with different sizes of validation sets including an 80/20 and a 75/25 validation/training split (with validation sets further split into a large validation and small test set).

**[Scratch-Built networks with 80/20 split](https://github.com/ehardwick2/Satellite_Image_Classification/blob/main/Scratch-Built-80-20-split.ipynb)**

**[Scratch-Built networks with 75/25 split](https://github.com/ehardwick2/Satellite_Image_Classification/blob/main/Scratch-Built-75-25-split.ipynb)**

**[MobileNetV2 Transfer Learning Model](https://github.com/ehardwick2/Satellite_Image_Classification/blob/main/MobileNetV2_transfer.ipynb)**

**[ResNet50 Transfer Learning Model](https://github.com/ehardwick2/Satellite_Image_Classification/blob/main/ResNet50_transfer.ipynb)**
<p align="center">

Learning curves for fine-tuned training epochs from ResNet50 transfer learning model:
  
![image](https://user-images.githubusercontent.com/102127193/219992091-0838fc8e-6a0d-476c-8e32-94a27400659e.png)

</p>

## Conclusions
### Take Home:
Both transfer learning models achieve good accuracy, around 98%, on validation and test sets. If the model will be updated with additional training data frequently, the better choice might be the MobileNetV2 model, as the training time is less than half that of the ResNet50 model. 
<p align="center">
  
![image](https://user-images.githubusercontent.com/102127193/219991866-8b472ada-c9c2-4cab-b07e-8449471d89e0.png)

</p>

### Further Investigation:
This dataset consisted only of RGB images, but the Sentinel-2 satellite collects data in 13 different bands, including in the near infrared and short wave infrared spectral ranges. Certain pigments in plants strongly reflect certain wavelengths of near-infrared light (which is invisible to the human eye) and these bands are used in remote sensing for vegetation and forest mapping. It would be very interesting to obtain the additional band information from the same images and reperform the modeling with the additional information and compare results. Misclassification with bodies of water would probably not occur as frequently with near-infrared band data included. 
