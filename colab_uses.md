# how to unzip file in colab
```py
import zipfile
zip_ref = zipfile.ZipFile("zipfile.zip", "r")
zip_ref.extractall()
zip_ref.close()
```
