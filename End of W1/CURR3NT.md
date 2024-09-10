
***Weight Comparison's***

First Iteration using :   *DeepLabV3_ResNet50_Weights*

RUN 1: 

Epoch 1, Average Loss: 0.4213 
Epoch 2, Average Loss: 0.4184 
Epoch 3, Average Loss: 0.4165
Epoch 4, Average Loss: 0.4135
Epoch 5, Average Loss: 0.4080

Average Validation Loss: 0.4252
*average loss computed across validation data after the model has processed it*

RUN 2:

Epoch 1, Average Loss: 0.3190
Epoch 2, Average Loss: 0.3146
Epoch 3, Average Loss: 0.3127
Epoch 4, Average Loss: 0.3101
Epoch 5, Average Loss: 0.3078

Average Validation Loss: 0.2903

Run 3 (loading in trained weights): Average Validation Loss: 0.2855
Average Validation Loss: 0.1380



Guppy 1 - batch size 4, image size 520, 35 epochs 

Epoch 35, Average Loss: 0.2416


Guppy 2 - batch size 10, image size 520, 50 epochs:

Epoch 13: Average Loss: 0.0125 crashed 

Guppy 3: 

Average Loss - 0.0016
Average Validation Loss: 0.0014

Guppy 4:

Average loss - 0.0013
Average validation loss 0.0018

Ideas for metric // 

For tasks like border detection, it might be worth exploring **boundary-sensitive loss functions** like **Dice Loss** or **Jaccard Loss (Intersection over Union, IoU)**. These loss functions are particularly effective in segmentation tasks, where capturing the exact boundaries (like invoice borders) is important.

Dice loss especailly good as there are more background pixels than border pixels so weights the areas of interest higher: current dice score: 

Dice: 0.1534 (stinks)

Convolution 
Resnet101
thresholds 

- get a feel for the model 

- diff examples

save after every epoch with statistics 

focus on IoU - highest I can get 

overfit training set of 100 images (does model even learn?)

Dataset - 3,000 - 5,000 



1) get a feel for model thresholds 
2) change training code to wanddb and save epoch / statistics every time
3) small training 


fast.ai course ML course

