# Optical character recognition

![](https://images.unsplash.com/photo-1535054820380-92c41678b087?ixlib=rb-4.0.3&ixid=M3wxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8fA%3D%3D&auto=format&fit=crop&w=1171&q=80)

📷 by [Kristian Strand](https://unsplash.com/fr/@kristianstrand)

## Install dependencies

```bash
pip install -U opencv-python pytesseract
```

## Image preprocessing and characters extraction

```python
import cv2
import pytesseract

img = cv2.imread("my_image.png")

gray = cv2.cvtColor(img, cv2.COLOR_BGR2GRAY)
blur = cv2.GaussianBlur(gray, (5, 5), cv2.BORDER_DEFAULT)
thresh = cv2.threshold(blur, 200, 255, cv2.THRESH_BINARY)[1]
kernel = cv2.getStructuringElement(cv2.MORPH_ELLIPSE, (1, 1))
opening = cv2.morphologyEx(thresh, cv2.MORPH_OPEN, kernel, iterations=1)

print(pytesseract.image_to_string(opening, lang="eng", config="--oem 3 --psm 6"))
```
