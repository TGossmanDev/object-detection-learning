**Localization** - finding what and where a single object exists in an image

**Object detection** - finding what and where multiple objects are in an image

#### How localization is done
- Object Localization is done by feeding an image through a CNN and returning output nodes for the different classes that we have 
    - For example, if you are using a dataset that usses both cats and dogs as its classes the output will have the probability that the object is either a cat or a dog
    - After this four additional nodes are added that define the bounding box of the object. (Note: you need at least four points to define a bounding box!)
        - Two common ways to define a bounding box: (x1, y1) and (x2, y2) using the upper left and upper right corners. The other way is ot have two points define a corner point and two points to define height and width of the bounding box 
- Localization is not that big of a problem, the issue is how do we generalize this for multiple objects in an image?
- There are many different approaches to solving object detection!

#### Approach 1, Sliding Windows 
- The "natural" extension 
- One of the earlier approaches
- This takes a crop of the image that is within the bounding box and resizes it, (typically 224x224) and then looks for the objects in the specific crop of that image 
- Then this bounding box with a predefined stride starting sliding along the image of its predefined stride length, pushing each through the CNN until you have reached the object and you get a "perfect" bounding box for that image. 
- Typically the sliding window is a square, this leads to less distortion when resizing, but this can work with rectangular bounding boxes 
- **Potential Problems**
    1. You need a lot of computation! The strides can be quite small and can sometimes move only about a pixel at a time which requires running so many different types of the image through the CNN. You also need to rerun multiple times since some objects can be further away than others, or even different sizes 
        - Note: this can be implemented more efficiently using a ConvNet
    2. Ther are many bounding boxes for the same object

#### Approach 2, Regional Based Networks 
1. Input the image 
2. Algorithm is run to extract region proposals (in the original paper this was not a neural network rather a deterministic search), this could extract a few thousand proposlas (~2k)
3. After tihs, the proposals with a high probability of hav ing an object are resized again (typically to 224x224) and run through a CNN
4. Then class predictions are done for the particular crop. Additionally, values can be output if we want to adjust the original bounding box 
- **Pros**
    - Fixed number of proposals that could be run through the CNN
    - You don't have to worry about determining the bounding box size of our crops since this is solved with the selective search algirhtm
- Three papers, RCNN, Fast RCNN, and Faster RCNN. At the end they change the region proposal to become a neural network, which can be tricky to implement
- **Cons**
    1. Still slow, with a complicated two step process 

#### Yolo Algorithm 
1. Start by splitting the image into an SxS grid 
2. Each cell will predict if there is a bounding box in each cell and the class probability in each cell. The cell is responsible for outputting the bounding box if its the center point of the object. Then that cell is responsible for predicitng a bounding box. This can be hard to predict if something is the center of an object so you get many different bounding boxes at once 











