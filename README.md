# Indian-Scene-Text-Dataset

The Indian scene text dataset has been generated as part of the work towards [Indian Signboard Translation Project](https://ai4bharat.org/articles/sign-board) by [AI4Bharat](https://ai4bharat.org/). The project involves threes modular tasks:
1. **Text Detection:** Detecting bounding boxes containing text in the images
2. **Text Recognition:** Getting the text from the detected crop 
3. **Translation:** Translating text from one Indian language to other Indian language

![Pipeline for sign board translation](../master/Images/Pipeline.jpg)


## Detection & Recognition Dataset 
 [Shubham Patel](https://www.linkedin.com/in/shubhampateliet/) and [Jaya Ingle](https://www.linkedin.com/in/inglejaya95/) have synthetically generated the [Indian language text detection & recognition dataset](https://drive.google.com/folderview?id=1hnNxuHbBBZrrI7Ee6FePTsUfW97qrJAS) based on [SynthText](http://www.robots.ox.ac.uk/~vgg/data/scenetext/) while at IIT Madras. This synthetic detection & recognition dataset is a collection of images where in word instances of specific Indian languages are placed over natural scences. Each image has a corresponding annotation csv file that lists the bounding box coordinates for each word instance in that image. Check the sample images in the dataset below: 
Sample - Tamil            |  Sample - Hindi
:------------------------:|:------------------------:
![Sample - Tamil](../master/Images/Tamil-Detection-Recognition.jpg)  |  ![Sample - Hindi](../master/Images/Hindi-Detection-Recognition.jpg)

## Recognition Dataset
I have compiled a new dataset for the recognition task alone from the above detection & recognition dataset. 

### Recognition Dataset Download Links
Currently, this repository has links to download dataset zip files for 5 Indian languages namely *Tamil*, *Hindi*, *Telugu*, *Malayalam* and *Punjabi*. After the extraction of a zip file, you can find 3 data split folders namely *Train*, *Val* and *Test*. Each of these folders has a collection of uniform size (width: 200, height:50) cropped images named with text label. The text before the first underscore('\_') in the image name represents the indian language text in the image. 
|Download Link              |# Images in Train |# Images in Val |# Images in Test |Image Sample                                          |Image Sample Word Instance |
|:-------------------------:|:----------------:|:--------------:|:---------------:|:----------------------------------------------------:|---------|
|[Tamil][Tamil Zip]         |500000            |5000            |5000             |![Image Sample](../master/Images/அகரம்_30_670_0.jpg)  |அகரம்    |
|[Hindi][Hindi Zip]         |500000            |5000            |5000             |![Image Sample](../master/Images/अगर_25_308_0.jpg)    |अगर       |
|[Telugu][Telugu Zip]       |400000            |5000            |5000             |![Image Sample](../master/Images/అజయ్_25_2491_2.jpg)  |అజయ్     |
|[Malayalam][Malayalam Zip] |400000            |5000            |5000             |![Image Sample](../master/Images/അകവൂർ_22_2655_0.jpg) |അകവൂർ    |
|[Punjabi][Punjabi Zip]     |~400000           |5000            |5000             |![Image Sample](../master/Images/ਉਸਦੇ_30_3782_1.jpg)   |ਉਸਦੇ      |

[Tamil Zip]: https://drive.google.com/file/d/1l0ifp-ny0Ssy8APjTaYDzoq2MNMf4PfH/view?usp=sharing
[Hindi Zip]: https://drive.google.com/file/d/1iYX4SdF07brsn2F4NkwjvmWG4unn6IBv/view?usp=sharing
[Telugu Zip]: https://drive.google.com/file/d/1Rx-jT_4rvK4cdeSVS_j4q598DzA1bxN4/view?usp=sharing
[Malayalam Zip]: https://drive.google.com/file/d/1HfGNsNAMVeP17kDaZA8C52z_HvBa-QpH/view?usp=sharing
[Punjabi Zip]: https://drive.google.com/file/d/1V8ummr3nCnO32Qm8igJRXdr7sgpQE-g8/view?usp=sharing
