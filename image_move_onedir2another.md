# Split data 20% and move dav_data directory use shutil,glob. 

```py

import os 
import glob
import shutil

img = glob.glob("train_data/*.jpg")

val = int((len(img)*20)/100)

for i in img[:val]:
    txt = i.split("/")[-1].split(".")[0]
    txt_file = i.split("/")[0]+"/gt_"+txt+".txt"
    if os.path.isfile(txt_file):
        shutil.move(i, "val_data/"+i.split("/")[-1])
        shutil.move(txt_file, "val_data/"+txt_file.split("/")[-1])
        print(i)

```
