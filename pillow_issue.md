# ImageDraw support for Bangla language

if your bangla conbine character boken to draw pillow image please follow this instruction.

```py
from PIL import ImageFont, Image, ImageDraw, ImageChops, ImageOps
w, h = 64, 64
w0, h0 = 256, 256
blank = Image.new('L', (w0 * 5, h0 * 3), 255)
font = 'Siyamrupali.ttf'
font = ImageFont.truetype(font, 20)  
char = 'দৃষ্টিভঙ্গি'
img = Image.new("L", (w0 * 5, h0 * 3), 255) 
draw = ImageDraw.Draw(img)
draw.text((w0, h0), char, font=font,layout_engine=ImageFont.LAYOUT_RAQM)
diff = ImageChops.difference(img, blank)
lx, ly, hx, hy = diff.getbbox()
img = img.crop((lx, ly, hx, hy))
img.save('image' + '.png')
```
Run,
```
sudo apt-get install libfreetype6-dev libharfbuzz-dev libfribidi-dev gtk-doc-tools
```

then clone pillow git and go depends folder
Run,
```
chmod +x install_raqm.sh
```
```
./install_raqm.sh
```

uninstall your previous pillow version and install,
```
conda install pillow=6.0.0
```
After following this process my problem solve.
