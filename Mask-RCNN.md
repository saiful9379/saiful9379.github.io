# MaskRCNN
### Instance image segmentation with Mask R-CNN



#### Region proposal network (RPN)

The RPN should take two inputs, image features (i.e. features extracted by ResNet) and ground truth bounding boxes and produce object proposals and corresponding “objectness” scores. 


I’m visualizing something like:

```py
x = keras.layers.Input((223, 223, 3))

a = keras_resnet.ResNet50(x)

b = keras.layers.Input((None, 4))

y = keras_rcnn.layers.RPN((14, 14))([a, b])


```
