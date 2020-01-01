# Vgg format to East dataset format convert

```py
import json
import numpy as np
import cv2
import matplotlib.pyplot as plt

output_path = "raw"
path="via_export_json_menon.json"
with open(path,"r") as json_file:
    data = json.load(json_file)
    for i in data:
        print(data[i]['filename'])
        txt_file_name = "gt_"+data[i]['filename'][:-4]+".txt"
        txt_file = open(output_path+"/"+txt_file_name,'w')
        for region in data[i]['regions']:
            x,y,width,height = region['shape_attributes']['x'],region['shape_attributes']['y'],region['shape_attributes']['width'],region['shape_attributes']['height']
            w,h = x+width,y+height
            x1,y1,x2,y2,x3,y3,x4,y4 = x,y,w,y,w,h,x,h
            txt_file.write(str(x1)+","+str(y1)+","+str(x2)+","+str(y2)+","+str(x3)+","+str(y3)+","+str(x4)+","+str(y4)+","+"###"+"\n")
        txt_file.close()
```
# East format to Roi converstion

```py
import numpy as np
import cv2
import matplotlib.pyplot as plt
img = cv2.imread("Scan_20191211 (3).jpg")
def text_roi():
    with open("gt_Scan_20191211 (3).txt",'r') as txt:
        data = txt.read()
        x = [i.split(',')[:-1] for i in data.split("\n")if len(i.split(',')[:-1])== 8]
        return x
polygon = text_roi()
for i in polygon:
    x1,y1,x2,y2,x3,y3,x4,y4 = int(i[0]),int(i[1]),int(i[2]),int(i[3]),int(i[4]),int(i[5]),int(i[6]),int(i[7])
    x = [x1,x2,x3,x4]
    y = [y1,y2,y3,y4]
    new_x = min(x)
    new_y = min(y)
    w = max(x)
    h = max(y)
    img_mod = cv2.rectangle(img, (new_x,new_y), (w,h), (0,255,0), 2) 
    cv2.imwrite("shape.jpg",img_mod)

```
