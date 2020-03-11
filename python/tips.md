python tips
---

## 線画抽出

これで意外とそれっぽくなる

```python
import numpy as np
import cv2 as c
import sys
import os

# 8近傍の定義
neiborhood8 = np.array([[1, 1, 1],
                        [1, 1, 1],
                        [1, 1, 1]],
                        np.uint8)

def create_senga(img_path):
    """create senga from img."""
    img = c.imread(img_path, 0) # 0なしでカラー
    img_dilate = c.dilate(img, neiborhood8, iterations=1)
    img_diff = c.absdiff(img, img_dilate)
    img_diff_not = c.bitwise_not(img_diff)
    filename = img_path.split('/')[-1][:-4] + '_sen.png'
    output_path = os.path.join('result', filename)
    c.imwrite(output_path, img_diff_not)
    print('success to out put senga: ' + output_path)

if __name__ == '__main__':
    img_path = sys.argv[1]
    if img_path:
        create_senga(img_path)
    else:
        print('need path to img!!')
```
