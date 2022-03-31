---
tags: opencv
---

# OpenCV

## bitwise逐位元操作
- 255(白), 0(黑)
- bitwise_and用會留下白色遮罩(255)共同的部分，黑色蓋掉(用黑色呈現)
- bitwise_or會挖掉白色遮罩(255)共同的部分(用白色呈現)
- bitwise_not會把黑變白,白變黑,其他顏色改成互補色
- bitwise_xor會把bitwise_or跟bitwise_not結合在一起

## 範例
![](https://i.imgur.com/Bx5STzG.png) ![](https://i.imgur.com/Olrx6oU.png)

---

```python=
#image_calculator.py
import cv2 as cv 
import numpy as np

img = cv.imread('./apple.jpg')
img2 = cv.imread('./android.jpg')
img3 = cv.bitwise_and(img,img2)#逐位元and邏輯運算

cv.imwrite('./img.png',img)
cv.imwrite('./img2.png',img2)
cv.imwrite('./img3.png',img3)
```
![](https://i.imgur.com/Cp2vCi4.png)

---

```python=
from cv2 import cv2 as cv 
import numpy as np

img = cv.imread('./apple.jpg')
img2 = cv.imread('./android.jpg')
img3 = cv.bitwise_or(img,img2)#逐位元or邏輯運算

cv.imwrite('./img.png',img)
cv.imwrite('./img2.png',img2)
cv.imwrite('./img3.png',img3)
```
![](https://i.imgur.com/36CtukO.png)

---

```python=
from cv2 import cv2 as ![https://ithelp.ithome.com.tw/upload/images/20201002/201211765A7QxEhPkQ.png](https://ithelp.ithome.com.tw/upload/images/20201002/201211765A7QxEhPkQ.png)cv 
import numpy as np

img = cv.imread('./apple.jpg')
img2 = cv.imread('./android.jpg')
img3 = cv.bitwise_not(img)#逐位元not邏輯運算1
img4 = cv.bitwise_not(img2)#逐位元not邏輯運算2
cv.imwrite('./img.png',img)
cv.imwrite('./img2.png',img2)
cv.imwrite('./img3.png',img3)
cv.imwrite('./img4.png',img4)
```
![](https://i.imgur.com/YKBUbAT.png) ![](https://i.imgur.com/oaiu1zE.png)
![](https://i.imgur.com/nKU5Z4N.png) ![](https://i.imgur.com/TDDAfYj.png)

---

```python=
from cv2 import cv2 as cv 
import numpy as np

img = cv.imread('./apple.jpg')
img2 = cv.imread('./android.jpg')
img3 = cv.bitwise_xor(img,img2)#逐位元xor邏輯運算

cv.imwrite('./img.png',img)
cv.imwrite('./img2.png',img2)
cv.imwrite('./img3.png',img3)
```
![](https://i.imgur.com/v7Kmvdz.png)

---

## logo覆蓋應用
- logo, img，logo要蓋在img上
- 挖logo
    - 灰階化 img2gray = cv2.cvtColor(logo,cv2.COLOR_BGR2GRAY)
    - 取值 ret, mask = cv2.threshold(img2gray, 10, 255, cv2.THRESH_BINARY)
    - 反向(製造mask) mask_inv = cv2.bitwise_not(mask)
    - 取出logo部分 img2_fg = cv2.bitwise_and(logo,logo,mask = mask)
- img
    - 取值範圍挖空 img1_bg = cv2.bitwise_and(roi,roi,mask = mask_inv)
- img, logo
    - 兩張圖疊加 dst = cv2.add(img1_bg,img2_fg)

---

## HSV取顏色範圍
- 取值函數cv2.inRange()需要採用HSV色彩空間

![](https://i.imgur.com/7Nt5aDi.png)

```python=
lower_green = np.array([35,43,46]) 
upper_green = np.array([77, 255, 255]) 
mask = cv2.inRange(hsv, lower_green, upper_green) 
#cv2_imshow(mask)
leaf=cv2.bitwise_and(pot,pot,mask=mask)
cv2_imshow(leaf)
```