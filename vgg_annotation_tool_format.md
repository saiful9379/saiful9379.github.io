# VGG16 annotation tool format json file create by python Programming


```json
{
    "zurb-foundation-templates-2.JPG37087": {
        "filename": "zurb-foundation-templates-2.JPG",
        "size": 37087,
        "regions": [
            {
                "shape_attributes": {
                    "name": "rect",
                    "x": 26,
                    "y": 20,
                    "width": 184,
                    "height": 14
                },
                "region_attributes": {
                    "Layout": "Menu"
                }
            },
            {
                "shape_attributes": {
                    "name": "rect",
                    "x": 31,
                    "y": 40,
                    "width": 174,
                    "height": 73
                },
                "region_attributes": {
                    "Layout": "Section"
                }
            }
           ]
         }
}

```

# Script

```py
import json
dic = {}
filename = "file_name"
size = 162945
regions= []
for i in range(2):
    shape_attributes = {
        "name": "rect",
        "x": 107,
        "y": 255,
        "width": 127,
        "height": 31
    }
    region_attributes= {
        "Layout": "Text"
    }
    shape_region_com = {
        "shape_attributes":shape_attributes,
        "region_attributes":region_attributes
    }
    regions.append(shape_region_com)

annotation_structure = {
    "filename":filename,
    "size":size,
    "regions":regions,
}
dic[filename]=annotation_structure

print(dic)

```
