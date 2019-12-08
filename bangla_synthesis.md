
```py
from PIL import ImageFont, ImageDraw, Image
import matplotlib.pyplot as plt
import numpy as np
import cv2
import random
import codecs
from scipy import ndimage
def synthesis_data_generator(input_text,wight):
    h = 40
    character_len = len(input_text)
    
    if character_len > 1:
        w = wight + character_len*10
    else:
        w = wight
        
    image = np.zeros((h,w,3), np.uint8)
    # Convert to PIL Image
    cv2_im_rgb = cv2.cvtColor(image, cv2.COLOR_BGR2RGB)
    # print(cv2_im_rgb)
    # exit()
    pil_im = Image.fromarray(cv2_im_rgb)

    draw = ImageDraw.Draw(pil_im)


    # Choose a font
    font = ImageFont.truetype("font/kalpurush.ttf", 25)
    # font = ImageFont.truetype(str(combo.get()),18)
    print("df dsf pillow img ")
    # exit()

    # Draw the text
    draw.text((2,5),input_text, font=font)

    # Save the image
    cv2_im_processed = cv2.cvtColor(np.array(pil_im), cv2.COLOR_RGB2BGR)
    a = 255 - cv2_im_processed
    gray = cv2.cvtColor(a, cv2.COLOR_BGR2GRAY)
    #     gray_specl = speckle(gray)
    img_name = input_text+"_"+str(1)+".jpg"
    cv2.imwrite(img_name,gray)
    plt.imshow(gray,cmap="gray")
    plt.show()
    
if __name__ =="__main__":
    w = 20
    input_text="সুন্দারগঞ্জ"
    
    synthesis_data_generator(input_text,w)
```
