
- **U-Net**:
    - **Pros**: Effective for tasks requiring detailed segmentation, such as medical imaging or document processing. Simpler and faster compared to DeepLabV3.
    - **Cons**: May struggle with extremely complex forms without sufficient training data.
- **FCN (Fully Convolutional Network)**:
    - **Pros**: Lightweight and faster to train, good for tasks where speed is critical.
    - **Cons**: May not capture the fine details or context as effectively as DeepLabV3 or U-Net.
- **Mask R-CNN**:
    - **Pros**: Great for instance segmentation, where you need to identify and mask multiple objects or elements separately.
    - **Cons**: More complex and heavier than U-Net, might be unnecessary if only one object or form needs to be segmented.

Mask limitation in pytorch using deeplab v3 

