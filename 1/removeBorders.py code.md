[[BRIEF 1]]
Trying to convert the removeBorders algorithm into a CNN.  

Process: 
- **Preprocessing:** Convert the image to grayscale and binarize it.
- **Line Detection:** Detect vertical and horizontal lines using morphological operations.
- **Padding:** Apply padding to the detected lines to ensure complete removal.
- **Combine and Output:** Merge the processed image with the original to maintain as much of the text as possible while removing the grids.

```python
from PIL import Image
import cv2
import numpy as np
import re

  
def get_1s(array):
    array_clip = np.clip(array,a_min=0, a_max=1)
    a_str = ''.join([str(num) for num in np.squeeze(array_clip)])
    matched = [m.span() for m in re.finditer(r'(1+)', a_str)]
    return matched
```
- - **Purpose:** This function identifies sequences of "1s" in a binary array, which likely represents lines or other features in the image.
    - **How it works:**
        - The array is first clipped between 0 and 1 to ensure binary values.
        - The binary array is converted into a string of 0s and 1s.
        - Regular expressions (`re.finditer`) are used to find sequences of "1s", and their start and end indices are recorded.
    - **Output:** Returns a list of tuples indicating the start and end indices of sequences of "1s".

```python 
def pad_start_n_end(s, e, min_index, max_index, padding):

    if int(padding) < 0:
        padding = 0

    new_s = int(s) - int(padding)
    new_e = int(e) + int(padding)

    if new_s < min_index:
        new_s = min_index

    if new_e > max_index:
        new_e = max_index

    return new_s, new_e
```
- **Purpose:** To adjust the start (`s`) and end (`e`) indices of a sequence, applying padding while ensuring the indices stay within valid bounds.
    - **How it works:**
        - Padding is added to both the start and end indices.
        - If padding pushes the start or end beyond the minimum or maximum allowed indices, they are clamped to stay within valid bounds.
    - **Output:** Returns the new, adjusted start and end indices.
```python
def pad_array_index(arr, padding=0):
    array = np.squeeze(arr)
    max_index = len(array)
    min_index = 0
    matched = get_1s(array)

    # matched = find_1s_span(array)
    padded = [pad_start_n_end(s,e, min_index, max_index, padding) for s, e in matched]
    
    return padded

  ```
  - **Purpose:** This function pads detected sequences of "1s" within an array, expanding their range.
- **How it works:**
    - It first flattens the array and then finds all sequences of "1s" using `get_1s`.
    - For each sequence, the start and end indices are adjusted using `pad_start_n_end`.
- **Output:** A list of padded start and end indices.
  
```python
def pad_by_pixel_arrays(pixel_array, pad=0):
    pixel_array_copy = pixel_array.copy()
    ii_list = pad_array_index(pixel_array_copy, padding=pad) # indexes ranges list
    if ii_list == []:
        return pixel_array
    else:
        ii = np.hstack([np.arange(s,e) for s, e in ii_list])
        np.put(pixel_array_copy, ind=ii, v=[255 for i in range(len(ii))]) # 255 for white
        return pixel_array_copy # padded_pixel_array
```
- **Purpose:** Applies padding to specific pixel sequences (typically representing lines) within a pixel array.
- **How it works:**
    - Copies the input array.
    - Uses `pad_array_index` to get padded indices.
    - Modifies the pixel array, setting the pixels in the padded range to white (value 255).
- **Output:** Returns the modified pixel array with padded areas.

```python
def paded_edge_matrix(edge_matrix, axis = 0, padding=0 ):
    # axis = 0 for looping row, pad column edges;
    # axis = 1 for looping columns, pad row edges;
     # return paded_column_edge_matrix
    m = edge_matrix
    if axis == 0:
        return np.vstack([pad_by_pixel_arrays(row, pad=padding) for row in m ])

    elif axis == 1:
        return np.vstack([pad_by_pixel_arrays(col, pad=padding) for col in m.T ]).T

    else:
        print(f'axis is "{axis}", not 0 or 1!')
```
- **Purpose:** Applies padding to the detected edges (either vertical or horizontal) within the image.
- **How it works:**
    - Iterates over rows or columns (depending on the axis) of the `edge_matrix`.
    - Applies `pad_by_pixel_arrays` to each row/column to pad the edges.
- **Output:** Returns the padded edge matrix.
  
```python
def remove_grids_from_image_v2(image, padding = 1):

    img_np = np.array(image)
    img_np = img_np.astype(np.uint8)
    img = cv2.cvtColor(img_np, cv2.COLOR_BGR2GRAY)
    
    #thresholding the image to a binary image
    thresh,img_bin = cv2.threshold(img,128,255,cv2.THRESH_BINARY |cv2.THRESH_OTSU)
    #inverting the image 
    img_bin = 255-img_bin

    # Length(width) of kernel as 100th of total width
    kernel_len = np.array(img).shape[1]//100
    # Defining a vertical kernel to detect all vertical lines of image 
    ver_kernel = cv2.getStructuringElement(cv2.MORPH_RECT, (1, kernel_len))
    # Defining a horizontal kernel to detect all horizontal lines of image
    hor_kernel = cv2.getStructuringElement(cv2.MORPH_RECT, (kernel_len, 1))

    image_1 = cv2.erode(img_bin, ver_kernel, iterations=3)
    vertical_lines = cv2.dilate(image_1, ver_kernel, iterations=3)

    image_2 = cv2.erode(img_bin, hor_kernel, iterations=3)
    horizontal_lines = cv2.dilate(image_2, hor_kernel, iterations=3)

    new_vertical_lines = paded_edge_matrix(vertical_lines,padding=padding, axis=0)
    new_horizontal_lines = paded_edge_matrix(horizontal_lines,padding=padding, axis=1)

    img_vh = cv2.addWeighted(new_horizontal_lines, 1, new_vertical_lines, 1, 0.0)
    
    img_sum_np = cv2.addWeighted(img,1, img_vh,1,0)
    img_sum = Image.fromarray(np.uint8(img_sum_np))
SLNZVJ!!!ammoforodium
    return img_sum
```
- **Purpose:** Main function to process an image and remove grid lines that might interfere with text recognition.
- **How it works:**
    - Converts the image to grayscale.
    - Binarizes the image using Otsu's thresholding method.
    - Detects vertical and horizontal lines using morphological operations (erosion followed by dilation).
    - Pads the detected lines using `paded_edge_matrix`.
    - Combines the padded lines with the original image to produce a final image with grid lines removed.
- **Output:** Returns a processed image with grids removed, suitable for text recognition.

***Things to note / ASK : ***

- **Morphological Operations:**
    
    - The code uses erosion and dilation to detect vertical and horizontal lines. Erosion reduces the lines to a minimum width, and dilation restores them while keeping noise minimal.
- **Padding Logic:**
    
    - The padding functions ensure that lines are not just removed but their surrounding pixels are also cleared, which prevents small remnants of lines from affecting text recognition.
- **Regular Expressions in `get_1s`:**

    - Regular expressions are cleverly used to detect continuous sequences of "1s" in the binary array, which are interpreted as features (e.g., lines) that need to be processed.

