# Data annotation convert East format
```py
import json
import os
def get_txt_annotation(json_path):
    root_path = json_path.split("/")[0]
    train_txt = open(root_path+"/train_list.txt","w")
    with open(json_path) as file_:
        data = json.load(file_)
        for i in data:
            file_name = data[i]['filename']
            region = data[i]['regions']
            # print(region)
            gt_path = root_path+"/gt_train"
            os.makedirs(gt_path,exist_ok = True)
            gt_txt = open(gt_path+"/"+file_name[:-4]+".txt","w")
            train_txt.write(file_name+"\n")
            for region in data[i]['regions']:
                class_name = region['region_attributes']['layout']
                if class_name =="Text" or class_name =="text":
                    if region['shape_attributes']['name'] =='rect':
                        x,y,w,h = region['shape_attributes']['x'],region['shape_attributes']['y'],region['shape_attributes']['width'],region['shape_attributes']['height']
                    elif region['shape_attributes']['name'] =='polygon':
                        all_x,all_y = region['shape_attributes']['all_points_x'],region['shape_attributes']['all_points_y']
                        x,y,w,h = min(all_x), min(all_y), max(all_x), max(all_y)
                    x1,y1,x2,y2,x3,y3,x4,y4 = x,y,w,y,w,h,x,h
                    gt_txt.write(str(x1)+","+str(y1)+","+str(x2)+","+str(y2)+","+str(x3)+","+str(y3)+","+str(x4)+","+str(y4)+",text\n")
            gt_txt.close()
    train_txt.close()
if __name__=="__main__":
    json_path = "val/data.json"
    get_txt_annotation(json_path)
```
