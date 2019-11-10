# About
YOLO ("you only look once") is a popular algorithm in object detection because it achieves high accuracy while also being able to run in real-time. This algorithm "only looks once" at the image in the sense that it requires only one forward propagation pass through the network to make predictions. The key techniques used in YOLO is so called non-max suppression.  In this project, we do the following: (1) implemented the non-max-suppression function to filter the bounding boxes (2). Test YOLO pretrained model together with our filter function (a threshold filter and the non-max-suppression filter) we implemented on images. 

# Some details of YOLO algorithm for Autonomous-driving:
 (1) For each picture, a grid, say, 19*19 is assigned.
 
 (2) ecode the picture in the following way. Firstly, each grid cell is asssigned a number of anchor boxes(which can captures 
 the size/shape of objects). For each anchor box, calculate its IOU(interface over union) ratio with ground truth box for all instances and all class of objects. The target label would be a concatenated vector with each component vector being the form ,(p,x,y,w,h,c1,c2,...cn) where p=1,0 means whether there is an object, [x,y, w,h] means the geometrical parameters of the  
 ground truth box, c1,...,cn is the one-hot vector for object classes. In labeling, for a given grid, for each object class(say A), we at most assign one anchor box to it. The other anchor boxes with smaller IOU for class A may have larger IOU for would be assiged as capturing other class or background (p=0).
 
 (3)non-max-suppression is used afer the forward propogation.  Now for each grid cell, we for each anchor, we have a max pro=p*ci for some class i(1 or 0 for target label). Note we took the class with maximum pro. There are still too many suggested boxes. We do the following two steps to filter them: (A) if pro is smaller than some threshold, discard it. (B) from the box with overall largest pro, calculate its IOU with others. For those IOU larger than some ratio, discard them. Move the box into a "chosen" set. From the remaining boxes, do this again until the remaining set is zero. In this way we discudd those similar(with slightly smaller pro) boxes. 
     
 
 
