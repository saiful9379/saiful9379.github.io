# VGG Annotation format To COCO Format

Vgg annotation format,
```json
{
    "sample-license-plate.jpg162945": {
        "filename": "sample-license-plate.jpg",
        "size": 162945,
        "regions": [
            {
                "shape_attributes": {
                    "name": "rect",
                    "x": 107,
                    "y": 255,
                    "width": 127,
                    "height": 31
                },
                "region_attributes": {
                    "Layout": "Text"
                }
            }
           ]
        }
  }
```


Here is an example for the COCO data format JSON file which just contains one image as seen the top-level “images” element, 3 unique categories/classes in total seen in top-level “categories” element and 2 annotated bounding boxes for the image seen in top-level “annotations” element.

```json
{
  "type": "instances",
  "images": [
    {
      "file_name": "0.jpg",
      "height": 600,
      "width": 800,
      "id": 0
    }
  ],
  "categories": [
    {
      "supercategory": "none",
      "name": "date",
      "id": 0
    },
    {
      "supercategory": "none",
      "name": "hazelnut",
      "id": 2
    },
    {
      "supercategory": "none",
      "name": "fig",
      "id": 1
    }
  ],
  "annotations": [
    {
      "id": 1,
      "bbox": [
        100,
        116,
        140,
        170
      ],
      "image_id": 0,
      "segmentation": [],
      "ignore": 0,
      "area": 23800,
      "iscrowd": 0,
      "category_id": 0
    },
    {
      "id": 2,
      "bbox": [
        321,
        320,
        142,
        102
      ],
      "image_id": 0,
      "segmentation": [],
      "ignore": 0,
      "area": 14484,
      "iscrowd": 0,
      "category_id": 0
    }
  ]
}
```
### This script create json file coco fromat and also image mapping txt file,

```py
# -*- coding: utf8 -*-
import json
import cv2
import os

DEBUG = True

path = "data/val/data.json"
image_dir = "data/val/img/" 

################### output file ##########################333

OUTPUT_TXT_FILE = "test.txt"
OUTPUT_JSON_FILE = "coco/test.json"


classes_names=['Person','Car','Bicycle']

json_dict = {"images": [], "type": "instances", "annotations": [], "categories": []}

categories = {}
with open(OUTPUT_TXT_FILE,"w") as txt_f:
    with open(path,"r") as json_file:
        data = json.load(json_file)
        image_id = 0
        ano_id = 0
        categories_list=[]
        annotaion_list = []
        for i in data:

            file_name = data[i]['filename']
            img_path = image_dir+file_name
            if os.path.isfile(img_path):
                txt_f.write(file_name[:-4]+"\n")
        #       print(img_path)
                img = cv2.imread(img_path)
        #         print(img)
                h,w,_= img.shape
                
                image = {
                "file_name": file_name,
                "height": h,
                "width": w,
                "id": image_id,
                }
                json_dict["images"].append(image)
                for region in data[i]['regions']:
                    class_name = region['region_attributes']['layout']
                    indexs = classes_names.index(class_name)
                    id_name = (indexs,class_name)
                    if id_name not in categories_list:
                        categories_list.append(id_name)
                    if region['shape_attributes']['name'] =='rect':
                        x,y,w,h = region['shape_attributes']['x'],region['shape_attributes']['y'],region['shape_attributes']['width'],region['shape_attributes']['height']
                    elif region['shape_attributes']['name'] =='polygon':
                        all_x,all_y = region['shape_attributes']['all_points_x'],region['shape_attributes']['all_points_y']
                        x = min(all_x)
                        y = min(all_y)
                        w = max(all_x)
                        h = max(all_y)  
                    else:
                        pass
                    
                    ann = {
                        "area": w * h,
                        "iscrowd": 0,
                        "image_id": image_id,
                        "bbox": [x, y, w, h],
                        "category_id": indexs,
                        "id": ano_id,
                        "ignore": 0,
                        "segmentation": [],
                    }
                    json_dict["annotations"].append(ann)
                    ano_id+=1
                image_id += 1
            
            
        print("classes :",categories_list)
        # exit()
        list_of_cat= []
        categories_list = sorted([(i[0],i[1]) for i in categories_list])
        print(categories_list)
        # exit()
        # categories_list= categories_list.sort(key=lambda x: float(x[0]))
        # sorted_categoris= categories_list.sort(key=lambda x: int(x[0]))
        for i in categories_list:
            categoris_= {
            "supercategory": "none",
            "name": i[1],
            "id": i[0]       
            }
            list_of_cat.append(categoris_)
            
        json_dict['categories']=list_of_cat

with open(OUTPUT_JSON_FILE, 'w', encoding='utf8') as json_file:
    json.dump(json_dict, json_file, ensure_ascii=False)
```
