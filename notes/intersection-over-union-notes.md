**Scenario** - I have a target boudning box for an object and a prediction bounding box, I want to know how good the prediction is! This is where intersection over union comes from

#### How do we measure how good a bounding box is?
- We need a way to inspect how good a bounding box is without doing something like visually inspecting how good each bounding box is 
- First you calculate the intersection between the bounding boxes
- Then you calculate the union or combined area of both the bounding boxes 
- Metric: intersction over union. IoU = intersection/Union, this gives you a value between zero and one that tells you how good the bounding box is 
    - IoU > 0.5 = decent 
    - IoU > 0.7 = pretty good 
    - IoU > 0.9 = almost perfect 
    - You will almost never get a 1 
- How do we get the intersection with two sets of numbers?
```
box1 = [x1, y2, x2, y2]
box2 = [x1, y1, x2, y2]
```
- These values corespond to the corner points of the bounding boxes. We want to find the corner points for the intersection of this union 
```
x1 is max(box1[0], box2[0])
y1 is max(box1[1], box2[1])
x2 is min(box1[2], box2[2])
y2 is min(box1[3], box2[3])
```