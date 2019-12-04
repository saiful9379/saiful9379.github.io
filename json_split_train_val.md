# Split json file train and val 
Suppose we have a image folder and annotation json folder but you need split train image and json, And other need val image and json.So you  need to spit this json file what why this code may be 


Annotation file and folder structure,
```
                        ├── data
                        │   ├── 24c59362285bbddc26a914866a6041cd.png
                        │   ├── ...................................
                        │   ├── ...................................
                        │   ├── ...................................
                        │   ├── ...................................
                        │   ├── ecommerce-wireframes-magorg-proddet.jpg
                        └── via_export_json.json
                   
  ```                     
                        
 Script,
``` 
import json
import shutil
import random
import os

path = "via_export_json.json"
img_dir = "data"
percentage = 20
li=[]
with open(path,"r") as f:
    data = json.load(f)
    # print(data)
    for i in data:
        x = (i,data[i])
        li.append(x)

lenght_li = int((len(li)*percentage)/100)
print(lenght_li)

train_list = li[4:]
val_list = li[:4]
train_dic = {}

train_path = "train/img"
if not os.path.exists(train_path):
    os.makedirs(train_path)

for train in train_list:
    train_dic[train[0]]=train[1]
    img_name = train[1]['filename']
    shutil.move(img_dir+"/"+img_name, train_path+"/"+img_name)
with open('train/data.json', 'w') as outfile:
    json.dump(train_dic, outfile) 

val_dic = {}
val_path = "val/img"
if not os.path.exists(val_path):
    os.makedirs(val_path)

for val in val_list:
    val_dic[val[0]]=val[1]
    img_name = val[1]['filename']
    shutil.move(img_dir+"/"+img_name, val_path+"/"+img_name)
with open('val/data.json', 'w') as outfile:
    json.dump(val_dic, outfile)
```

Result folder structure,

```
                      ├── train
                      │   ├── data.json
                      │   └── img
                      │       ├── f33abea8e5021d41911365156f84a943.png
                      │       ├── .....................................
                      │       ├── .....................................
                      │       └── united-business-html-website-template-1.jpg
                      ├── val
                      │   ├── data.json
                      │   └── img
                      │       ├── WB0412697.png
                      │       ├──...............
                      │       └── zurb-foundation-templates-2.JPG

```
                        
                        
                        
            
