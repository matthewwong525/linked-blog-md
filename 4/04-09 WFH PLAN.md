
- Ragged School Museum 
- Obtain pen and notebook to write out notes on Julios paper throughout rest of week.
- Fully write up (pen and paper) process, get terminology down
- Look more into synthetic data (maybe generate 10 new images to be used later for **testing**)
- Find out what a metric actually is and make a big block for testing this on GPU's on Thursday 



inference code - DEF GOES HERE 

50 epochs compared (metrics)

:::

save weights directly on drive (altered) tesserocr

model.save_state_dict(torch.save('/content/drive/My Drive/savedWeights/model_weights.pth', map_location=torch.device('cpu')))
model.to('cpu')  # Ensure the model is on the CPU


model.load_state_dict(torch.load('/content/drive/My Drive/savedWeights/model_weights.pth', map_location=torch.device('cpu')))
model.to('cpu')  # Ensure the model is on the CPU


wandb - saving weights and biases // Dont really need - good to know 


