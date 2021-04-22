# CDNet-2014-MotSeg
In this repository we provide the modified CDNet-2014 groundtruth, we used to train our model for the paper "Deep Fusion of Appearance and Frame Differencing for Motion Segmentation" by Ellenfeld et al., IEEE CVPR Workshops 2021. Here is the direct link to the paper: [click me](#)

## Groundtruth Details
Our groundtruth was created semi-automatically, as described in our paper, and contains all categories and scenes of the original CDNet-2014. The data is structured as follows:

```
CDNet-2014-MotSeg
|  README.md 
└─ data
   └─ <category>
      └─ <scene> 
         ├─ groundtruth
         |      gtXXXXXX.png
         |      ...
         |
         ├─ groundtruth-semantic
         |      gtXXXXXX.png
         |      ...
         |
         ├─ groundtruth-semantic-separated
         |      gtXXXXXX.png
         |      ...
         |
         | temporalROI.txt
         | ROI.bmp
         | ROI.jpg
            
```

Each scene contains the three sub-directories *groundtruth*, *groundtruth-semantic* and *groundtruth-semantic-separated*. The data located in the sub-directory *groundtruth* is what we used to train our model for class agnostic motion segmentation. In addition we provide the two additional variants *groundtruth-semantic* and *groundtruth-semantic-separated* which include the semantic classes of moving objects. The files *ROI.bmp* and *ROI.jpg* show the spatial area of interest of the respective scene. These files are unchanged from the CDNet-2014 dataset. We edited the *temporalROI.txt* file to reflect the actual range of annotated frames. All frames outside of this range are fully annotated as *Outside region of interest*.

## Class Agnostic Motion Segmentation
The sub-directory *groundtruth* contains the class agnostic motion masks we used to train our model for motion segmentation. An example of the modified groundtruth is shown below. These grayscale images contain the 4 labels:

- 0: Static
- 85: Outside region of interest
- 170: Unknwon motion (Three pixel wide border around moving objects to accomodate for motion blur)
- 255: Motion

Note that the original annotations for *hard shadow* have been removed as they are not relevant to our task.

<p align="center">
    <img src="./figures/AdaptedGT.png" height="350px" width="auto">
    <br/>
    <span> Examples for the CDNet-2014  dataset groundtruth adapted to the task of motion segmentation.</span>
</p>


## Semantic Motion Segmentation
The sub-directories *groundtruth-semantic* and *groundtruth-semantic-separated* extend our class agnostic groundtruth to include the semantic class of moving objects. The version *groundtruth-semantic* assigns each object visible in the groundtruth exactly one semantic class. This creates the most accurate segmentation of objects, as each objects is simply relabeled to reflect the most prominent semantic class. In many scenes, however, moving objects are composed of multiple different objects, as seen in the example below. For this reason, the more detailed *groundtruth-semantic-separated* was created. This version separates different objects based on their semantic class. Note that the automatic relabeling depends on the accuracy of the classifier to do this. This results in the same object being split into different parts in certain frames.   

<p align="center">
    <img src="./figures/GT adapted, semantic, semantic-separated.png" height="400px" width="auto">
    <br/>
    <span> Examples for the CDNet-2014  dataset groundtruth adapted to the task of semantic motion segmentation. Semantic classes are colorized for better visualization. Blue represents the class <em>vehicle</em>, red represents <em>person</em> and white represents <em>other</em>.</span>
</p>

The semantics differentiate between the classes *person*, *vehicle* and *other*. Both semantic-groundtruth variants are grayscale images containing the 6 labels:

- 0: Static
- 85: Outside region of interest
- 100: Person (Motion originating from a person)
- 150: Vehicle (Motion originating from a vehicle)
- 170: Unknown Motion (Three pixel wide border around moving objects to accomodate for motion blur)
- 200: Other (Motion originating from an unknown Object)


# Cite us
If you use our groundtruth or the findings of our paper, then please cite us:
```
@InProceedings{ EllenfeldCVPR2021,   
   Title = {{Deep Fusion of Appearance and Frame Differencing for Motion Segmentation}},   
   Author = {Marc Ellenfeld and Sebastian Moosbauer and Ruben Cardenes and Ulrich Klauck and Michael Teutsch},   
   Booktitle = {IEEE CVPR Workshops},   
   Year = {2021}   
}
```