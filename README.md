# Indian-Scene-Text-Dataset

The Indian scene text dataset is generated as part of the work towards [Indian Signboard Translation Project](https://ai4bharat.org/articles/sign-board) by [AI4Bharat](https://ai4bharat.org/). I worked on this project under the mentorship of [Mitesh Khapra](http://www.cse.iitm.ac.in/~miteshk/) and [Pratyush Kumar](http://www.cse.iitm.ac.in/~pratyush/) from IIT Madras.

Indian Signboard Translation  involves 4 modular tasks:
1. **`T1`: Detection:** Detecting bounding boxes containing text in the images
2. **`T2`: Classification:** Classifying the language of the text in the bounding box identifed by `T1`
3. **`T3`: Recognition:** Getting the text from the detected crop by `T1` using the `T2` classified recognition model
4. **`T4`: Translation:** Translating text from `T3` from one Indian language to other Indian language

![Pipeline for sign board translation](../master/Images/Pipeline.jpg)
> Note: `T2`: Classification is not updated in the above picture


# `D`: Detection & Recognition Dataset 
[Shubham Patel](https://www.linkedin.com/in/shubhampateliet/) and [Jaya Ingle](https://www.linkedin.com/in/inglejaya95/) synthetically generated the [Indian language text detection & recognition dataset](https://drive.google.com/folderview?id=1hnNxuHbBBZrrI7Ee6FePTsUfW97qrJAS) based on [SynthText](http://www.robots.ox.ac.uk/~vgg/data/scenetext/) while at IIT Madras. This synthetic detection & recognition dataset is a collection of images where in word instances of specific Indian languages are placed over natural scences. Each image has a corresponding annotation csv file that lists the bounding box coordinates for each word instance in that image. Check the sample images in the dataset below: 
Sample - Tamil            |  Sample - Hindi
:------------------------:|:------------------------:
![Sample - Tamil](../master/Images/Tamil-Detection-Recognition.jpg)  |  ![Sample - Hindi](../master/Images/Hindi-Detection-Recognition.jpg)

I compiled new standalone datasets for the isolated tasks in the Indian Signboard Translation Pipeline. This will be helpful to those who intend to build pipeline models individually, by saving a lot of time in data preparation.


# `D1`: Detection Dataset
<!----------------------->
`D1` is filtered and processed from `D`. This include images with text instances from the language set `L` comprising **Tamil, Hindi, Telugu, Malayalam, and  Punjabi.** Images are resized to the common shape with width of 600 pixels and height of 450 pixels. And, the bounding box coordinates are processed accordingly and made availabe in 2 geometries namely **Quadilateral(QUAD)** and **Axes-Aligned-Bounding-Box(AABB)**. A bigger size variant(`D1-Big`) of this dataset is also created.

It has 3 top level folders, namely, `Train`, `Val` and `Test`. Each of these folders has 3 sub folders, namely, `Images`, `Annotations-AABB` and `Annotations-QUAD`. For each image in the `Images` folder, you can find the corresponding annotation csv files in the folders `Annotations-AABB` and `Annotations-QUAD` with the same name. In `AABB` representation, the *x*, *y* in the top left coordinate in the bounding box is available along with *w*(width) and *h*(height). In `QUAD` representation, *x* and *y* coordiantes for the four corner points of the bounding boz are available.  

Images are sampled uniformally in each data split with respect to the languages.

|Download Link              |# Images in Train |# Images in Val |# Images in Test |
|:-------------------------:|:----------------:|:--------------:|:---------------:|
|[`D1`][D1 Zip]             |10000             |1000            |1000             |
|[`D1-Big`][D1-Big Zip]     |50000             |1000            |1000             |

|Image Sample                                          |AABB Representation |QUAD Representation |
|:----------------------------------------------------:|:------------------:|:------------------:|
|![Image Sample](../master/Images/Tamil_24_3693.jpg)   |![AABB Sample](../master/Images/Tamil_24_3693-AABB.png)|![QUAD Sample](../master/Images/Tamil_24_3693-QUAD.png)|

**Code:** [Prepare-Detection-Dataset.ipynb](../master/Prepare-Detection-Dataset.ipynb)


# `D2`: Classification Dataset
<!--------------------------->
`D2` is filtered from `D3`. It has cropped image examples having word instances from the language set `L`.  

It has 3 top level folders, namely, `Train`, `Val` and `Test`. Each of these folders has a sub folder for each language in the language set `L`.

Images are sampled uniformally in each data split with respect to the languages.

|Download Link              |# Images in Train |# Images in Val |# Images in Test |
|:-------------------------:|:----------------:|:--------------:|:---------------:|
|[`D2`][D1 Zip]             |25000             |1000            |1000             |

|Image Sample                                          |Class / Language |
|:----------------------------------------------------:|:---------------:|
|![Image Sample](../master/Images/அகரம்_30_670_0.jpg)  |Tamil            |
|![Image Sample](../master/Images/अगर_25_308_0.jpg)    |Hindi            |
|![Image Sample](../master/Images/అజయ్_25_2491_2.jpg)  |Telugu           |
|![Image Sample](../master/Images/അകവൂർ_22_2655_0.jpg) |Malayalam        |
|![Image Sample](../master/Images/ਉਸਦੇ_30_3782_1.jpg)   |Punjabi          |

**Code:** [Prepare-Classification-Dataset.ipynb](../master/Prepare-Classification-Dataset.ipynb)


# `D3`: Recognition Dataset
<!------------------------>
`D3` is filtered and processed from `D`. Each language in the set `L` has the separate recognition datasets. `D3` has cropped image examples having word instances identified using the image file name. The version 2 of `D3` (`D3-V2`) is also generated by filtering out the ambiguous images (non human recognizable) from `D3`, which are identified using the neural network.

`D3` for each language in `L`, (`D3-Language`) has 3 top level folders, namely, `Train`, `Val` and `Test`. Each of these data split folders, has a collection of uniform size cropped images, with the width of 200 pixels and height of 50 pixels, named with text label. The text before the first underscore('\_') in the image name represents the indian language text in the image. 

|Download Link                    |# Images in Train |# Images in Val |# Images in Test |Image Sample                                          |Image Sample Word Instance |
|:-------------------------------:|:----------------:|:--------------:|:---------------:|:----------------------------------------------------:|:-------:|
|[D3-Tamil][D3-Tamil Zip]         |500000            |5000            |5000             |![Image Sample](../master/Images/அகரம்_30_670_0.jpg)  |அகரம்    |
|[D3-Hindi][D3-Hindi Zip]         |500000            |5000            |5000             |![Image Sample](../master/Images/अगर_25_308_0.jpg)    |अगर       |
|[D3-Telugu][D3-Telugu Zip]       |400000            |5000            |5000             |![Image Sample](../master/Images/అజయ్_25_2491_2.jpg)  |అజయ్     |
|[D3-Malayalam][D3-Malayalam Zip] |400000            |5000            |5000             |![Image Sample](../master/Images/അകവൂർ_22_2655_0.jpg) |അകവൂർ    |
|[D3-Punjabi][D3-Punjabi Zip]     |399989            |5000            |5000             |![Image Sample](../master/Images/ਉਸਦੇ_30_3782_1.jpg)   |ਉਸਦੇ      |

|Download Link                          |# Images in Train |# Images in Val |# Images in Test |Image Sample                                          |Image Sample Word Instance |
|:-------------------------------------:|:----------------:|:--------------:|:---------------:|:----------------------------------------------------:|:-------:|
|[D3-Tamil-V2][D3-Tamil-V2 Zip]         |227822            |2324            |2500             |![Image Sample](../master/Images/அகரம்_30_670_0.jpg)  |அகரம்    |
|[D3-Hindi-V2][D3-Hindi-V2 Zip]         |301732            |2974            |3050             |![Image Sample](../master/Images/अगर_25_308_0.jpg)    |अगर       |
|[D3-Telugu-V2][D3-Telugu-V2 Zip]       |187645            |2365            |2307             |![Image Sample](../master/Images/అజయ్_25_2491_2.jpg)  |అజయ్     |
|[D3-Malayalam-V2][D3-Malayalam-V2 Zip] |184722            |2403            |2333             |![Image Sample](../master/Images/അകവൂർ_22_2655_0.jpg) |അകവൂർ    |
|[D3-Punjabi-V2][D3-Punjabi-V2 Zip]     |188301            |1981            |2577             |![Image Sample](../master/Images/ਉਸਦੇ_30_3782_1.jpg)   |ਉਸਦੇ      |

Generation of `D3` involved the following 3 subsequent steps:

**1. Character Map Definition** <br>
Most of the popular Indian languages comprise of compound characters which can be formed by merging two base characters, usually a consonant and a glyph. Such a Character-Consonant-Glyph mapping has been generated for the languages in set `L` and available in the [characters directory](Characters). Identifification of such map will let us do **multi-label classification** (consonant-glyph classfication) over a simple character classification in the text recognition task. Check the sample rows of character mapping below:
|Sample - Tamil            |Sample - Hindi            |Sample - Telugu           |Sample - Malayalam        |Sample - Punjabi          |
|:------------------------:|:------------------------:|:------------------------:|:------------------------:|:------------------------:|
|![Sample - Tamil](../master/Images/Tamil-Character-Map.png) |![Sample - Hindi](../master/Images/Hindi-Character-Map.png) |![Sample - Telugu](../master/Images/Telugu-Character-Map.png) |![Sample - Malayalam](../master/Images/Malayalam-Character-Map.png) |![Sample - Punjabi](../master/Images/Punjabi-Character-Map.png) |
**Code:** [Define-Char-Maps.ipynb](../master/Define-Char-Maps.ipynb)

**2. V1 Dataset Preparation** <br>
This involves cropping the bounding rectangle of the text instance in the detection & recognition dataset images and resizing them to the common size of (200, 50).  Filtering is done to drop the improper/impure text label examples using the character map defined above. For example, *Tamil* word instances has been observed in *Telugu* and *Malayalam* detection & recognition dataset. Such images are ignored. Train-Val-Test split is also done in this stage.
**Code:** [Prepare-Recognition-Dataset.ipynb](../master/Prepare-Recognition-Dataset.ipynb)

**3. V2 Dataset Preparation** <br>
While evaluating the recognition model, we observed out that there are many images (roughly around 30%) that are not even human recognizable in `D3` which caused the poor test performance. Hence, we manually labelled 5000 images in `D3-Hindi-Test` set and trained a neural network to classify ambiguous and non-ambiguous cropped images. The trained model can be found in [Models/Ambiguity-Classifier.pth](../master/Models/Ambiguity-Classifier.pth). We used this model to filter out the ambiguous images in `D3-V2`.
**Code:** [Prepare-Recognition-Dataset-V2.ipynb](../master/Prepare-Recognition-Dataset-V2.ipynb)


[D1 Zip]: https://drive.google.com/file/d/1xHhe1VfEKRElkbYXzcIyN520Nqqdjpze/view?usp=sharing
[D1-Big Zip]: https://drive.google.com/file/d/1c8BjyMRO_I_ZotNbwiFRZPE6TmbJG1Uz/view?usp=sharing
[D2 Zip]: https://drive.google.com/file/d/1FBwhm5IhnZXEKQxQEPdiq5kGFfI4z94D/view?usp=sharing
[D3-Tamil Zip]: https://drive.google.com/file/d/1l0ifp-ny0Ssy8APjTaYDzoq2MNMf4PfH/view?usp=sharing
[D3-Hindi Zip]: https://drive.google.com/file/d/1iYX4SdF07brsn2F4NkwjvmWG4unn6IBv/view?usp=sharing
[D3-Telugu Zip]: https://drive.google.com/file/d/1Rx-jT_4rvK4cdeSVS_j4q598DzA1bxN4/view?usp=sharing
[D3-Malayalam Zip]: https://drive.google.com/file/d/1HfGNsNAMVeP17kDaZA8C52z_HvBa-QpH/view?usp=sharing
[D3-Punjabi Zip]: https://drive.google.com/file/d/1V8ummr3nCnO32Qm8igJRXdr7sgpQE-g8/view?usp=sharing
[D3-Tamil-V2 Zip]: https://drive.google.com/file/d/1z-tjkTxtF1SjY8vxEGq1Qnql55kOHVqk/view?usp=sharing
[D3-Hindi-V2 Zip]: https://drive.google.com/file/d/1eanV3SBoNd-igHe3mZNLEYfSGeXK9VPb/view?usp=sharing
[D3-Telugu-V2 Zip]: https://drive.google.com/file/d/10fRAkQIQMT_FjLM-GNITFxb8-5NtSm6-/view?usp=sharing
[D3-Malayalam-V2 Zip]: https://drive.google.com/file/d/1XxqgjwrjwS1MsgrDxUCd6a5G2e-4qXcL/view?usp=sharing
[D3-Punjabi-V2 Zip]: https://drive.google.com/file/d/1I65AkpdmQzh_TAbLQfPDzmPxWuqlVLht/view?usp=sharing
