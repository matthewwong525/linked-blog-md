The essential idea is to systematically destroy structure in a data distributiom through an iterative **forward diffusion process.** We then learn a **reverse diffusion process** that restores structure in data, yielding a highly flexible and tractable generative model of the data.


![[Pasted image 20240909145341.png]]

*Reverse process* uses a neural network to take an image (just noise) and remove this noise to get a new image. The neural network can predict 3 things:

- Mean of noise at each timestep
- Original image directly (can be ignored - wont work well)
- Noise of image directly (to be subtracted from noised image)

1 and 3 are actually the same - papers show that the third option (noise of image directly) is best option. n 
OpenAI's contribution was to change the fixed variance (no need to predict):

![[Pasted image 20240909145714.png]]

To the learned variance:

![[Pasted image 20240909145822.png]]

*Forward Process*

We don't employ the same amount of noise in each time step - this is regulated a scheduler for mean and variance so it doesn't explode. 2020 used linear, OpenAI used cosine: 

![[Pasted image 20240909150018.png]]


**Architectures:**

2020 Uses U-Net:

Resnet-Block, Downsample-Blocks 
- Breaks it down to a smaller resolution 

Bottleneck 


DDPL VS DL

**Similarities**

1. **Handling Uncertainty:**
    
    - Both **DL** and **DDPMs** address uncertainty in data. In **DL**, Data Assimilation integrates observational data with model predictions to improve accuracy, particularly under noisy or incomplete data conditions. Similarly, **DDPMs** add noise through a diffusion process and then reverse this noise, which helps in handling data uncertainty by generating high-quality samples.
2. **Iterative Process:**
    
    - **DL** uses an iterative process of updating models with new observations. Similarly, **DDPMs** follow a gradual, multi-step process where noise is incrementally added and removed, learning how to denoise data step by step.
3. **Improved Predictions/Generations:**
    
    - Both approaches aim to improve predictions. **DL** enhances predictions by combining data with physical models, while **DDPMs** improve generative modeling by learning a reverse diffusion process to denoise and reconstruct data distributions.

**Differences**

1. **Purpose:**

    - **DL** is primarily focused on improving predictive models in scientific and engineering domains by assimilating real-world observations (e.g., meteorology, air quality). **DDPMs**, on the other hand, are focused on **generative modeling**, particularly for high-quality image and audio generation.

1. **Methodology:**
    
    - **DL** combines machine learning and physical models to refine predictions by balancing observational data and model simulations. It’s rooted in physical sciences and aims for predictive reliability in complex systems.
    - **DDPMs** are probabilistic models that add noise to data through a diffusion process and then use a neural network to reverse the process. The focus here is more on the probabilistic and neural aspects of generating data, rather than combining physical models with observations.

1. **Type of Data:**
    
    - **DL** typically deals with real-world observational data, often from natural systems like weather or oceanography, where physical laws are known and integrated into the model.
    - **DDPMs** usually work with high-dimensional datasets, such as images or audio, where the data distribution is learned from scratch through a probabilistic framework, rather than being driven by physical models.
-
1. **Generative vs Predictive Focus:**
    
    - **DL** is about improving **predictions** in existing systems using assimilation techniques.
    - **DDPMs** are about generating new samples that match the target distribution, which is a form of **generation** rather than prediction.

### Discussion Points:

1. **How does Data Learning’s focus on real-world observations compare to Diffusion Models’ emphasis on probabilistic data generation?**
    
    - This highlights the difference between improving models based on reality (as in DL) versus learning a generative process that captures the data distribution (as in DDPMs).
2. **What are the pros and cons of incorporating physical models versus pure data-driven approaches?**
    
    - DL uses known physical laws, which can make predictions more reliable in certain domains. DDPMs, however, can generate realistic samples without needing explicit knowledge of physical systems.
3. **How do both methods handle uncertainty, and what are the implications for model accuracy and generalizability?**
    
    - Comparing how DL incorporates uncertainty from real-world noisy data versus DDPMs handling uncertainty through the diffusion process can help frame the discussion.