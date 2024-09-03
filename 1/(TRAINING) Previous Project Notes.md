
Boring stuff: 

1) CustomDataset class: 

Inherits from `torch.utils.data.Dataset` and represents a dataset consisting of images and their corresponding masks.

Takes in `image_folder` and `mask_folder` paths, a `transform` for the images, and a `mask_transform` for the masks.

 `self.image_filenames` stores the list of image filenames found in the `image_folder`. This assumes that each image has a corresponding mask with the same filename in the `mask_folder`.

 **`__len__` method**: Just returns the total number of images in the dataset.

**`__getitem__` method**:
    
    -  Fetches the image and corresponding mask based on the index `idx`.
    - The image and mask are loaded using `PIL.Image.open`.
	- The image and mask are then transformed using the transformations defined earlier (e.g., resizing, normalization).
    - Returns a tuple of `(image, mask)`.


2) Transformations 

- Resizes images to 1280x960 pixels.
-  Converts the image to a PyTorch tensor.
-  Normalizes the image tensor using the specified mean and standard deviation, which is  done to match the distribution of the dataset used to train the original model.

3) Data stuff

The `CustomDataset` is instantiated with the paths to the image and mask folders and the transformations defined earlier. This creates a dataset object that can be indexed to get (image, mask) pairs.


Optimizer and Loss function:

```python
import torch.optim as optim
device = 'cuda'
criterion = nn.MSELoss(reduction='mean')
optimizer = optim.Adam(pretrained_deeplab.parameters(), lr=1e-5)
pretrained_deeplab.to(device)
```
- **Optimizer**: Old version is using the Adam optimizer - meaning it adjusts the learning rate for each parameter individually. The learning rate is set super low at `1e-5`, likely because the model (`pretrained_deeplab`) is already pretrained, so we want to fine-tune it gently without disrupting the existing weights too much.
  
- **Loss Function**: The loss function chosen is Mean Squared Error. It's typically used for regression tasks but here, it might be applied because we're treating the segmentation as a continuous prediction problem (where each pixel value might be treated as a probability or intensity rather than a hard class label).

- **Device Setup**: We're ensuring that everything runs on a GPU (`device = 'cuda'`), which is essential for speeding up training, especially with deep models. !!! Ask about cuda (have not used before can read on it)

Training Loop: 

```python
# Set the model to training mode
pretrained_deeplab.train()

for epoch in range(100):
  total_loss = 0
  count = 0
  for images, masks in train_dataloader:
      images = images.to(device)
      masks = masks.to(device)
      optimizer.zero_grad()

      # Forward pass
      outputs = pretrained_deeplab(images)['out']

      # Calculate the loss
      loss = criterion(outputs, masks.float())
      count += 4
      total_loss += loss.item()

      # Backward pass and optimization
      loss.backward()
      optimizer.step()
  print(total_loss / count)
```

- **Training Mode**: Calls `pretrained_deeplab.train()`. This looks super important! It tells the model that we’re in training mode, so it should keep things like dropout active (if it has it) and update the running statistics for batch normalization layers.

- **Epoch Loop**: We’re running the training for 100 epochs(overkill?), but it depends on how well the model converges. If the loss isn't improving much after a certain point, we might want to consider early stopping or reducing the number of epochs.

- **Inner Loop - Batch Processing** - WHAT I NEED HELP WITH MOST:
    - **Moving Data to GPU**: Each batch of images and masks is moved to the GPU for faster computation.
    
    - **Zeroing Gradients**: `optimizer.zero_grad()` clears out the gradients from the previous step. If you don’t do this, gradients from multiple steps would accumulate, which would mess up the optimization process.

    - **Forward Pass**: We feed the images through the model, and it gives us the outputs.  `['out']` -That’s because DeepLab models often return multiple outputs that we dont need (right?)
    
    - **Loss Calculation**: The loss function compares the model's output to the ground truth masks. Since `masks` might be an integer type, converting them to `float()` ensures compatibility with the model’s output.

    - **Backward Pass**: `loss.backward()` calculates the gradients for all the parameters in the model based on the loss we just computed.  Backpropagation bby 

    - **Optimization Step**: `optimizer.step()` actually updates the model's weights based on the gradients calculated in the backward pass. This is how the model learns.

Tracking the progress with   print(total_loss / count) - This can be changed.

