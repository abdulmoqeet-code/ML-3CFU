 **Experiment Summary & Observations**

 **Recent Improvements**

1. **Dataset Size**
   Trained with 5,000 images

2. **Discriminator Behavior Improved**
   Previously, the **discriminator loss dropped to zero** after just 1 epoch, completely overpowering the generator.
   This time, the loss behaves more normally in early epochs — allowing better generator learning initially.

3. **Generator Loss is More Stable**
   Generator loss is now more consistent, though it appears to **plateau after 5 epochs**, suggesting learning saturation or adversarial imbalance.

4. **Input Normalization Fixed**
   Previously, the **input to the discriminator was not normalized**, unlike the real images.
   This mismatch caused instability and poor gradient flow — now resolved.

5. **Image Resolution Comparison**

   * Tried two combinations:

     * LR → 64 × 64 → HR → 256 × 256
     * LR → 32 × 32 → HR → 128 × 128
   * **Observation**: Increasing image resolution mainly increases computation cost without significantly improving output quality. Needs more investigation.(It matters because I've compared the results of 32x32 and 64x64 models. Interestingly, the 64x64 model still works well on 32x32 images. However, the 32x32 model struggles with 64x64 images and doesn't produce significantly distinguishable results.)
   



 **Upcoming Experiments**

1. **Handling Discriminator Dominance**

   * Issue: Discriminator loss still approaches **zero after 5 epochs**, causing an **adversarial imbalance**.
   * Plan:

     * Introduce **dropout** in the discriminator to regularize learning.(Have Tried)
     * Try **training the discriminator less frequently** (e.g., once every 2 epochs) to give the generator more room to improve. (Have Tried)

2. **Improving Generator Guidance**

   * Issue: Generator loss becomes stagnant; likely due to overpowered discriminator or limited capacity to adapt.
   * Plan:

     * Increase **perceptual loss weight** in the combined loss to enhance **feature-level supervision**, helping the generator focus more on visual details. (scale the Perceptual loss to 1.7, this only increased the loss but could not help)
     * **Unfreeze more layers** of the pretrained generator (currently only the last CNN layer is unfrozen) to allow it to **better adapt to the specific dataset**.

3. **Increasing Dataset**
   * Also will increase the dataset, most probably 8K (Done)
  
     
4. **Adding Label Smoothing in Discriminator**
   * To make it more usefull feedback to improve generation
   * To make it less confident, as loss is approches to 0 after couple of epochs
5. **Data Argumenation** 
   * I applied random data augmentations including horizontal flipping, rotation (±10°), and color jittering           (brightness, contrast, saturation) to increase dataset diversity. Additionally, I resized images to ensure        consistent low-resolution and high-resolution sizes.
6. **Unfreezing additional model layers**
   * First I Have tried with 1,2 now trying with last 10 layers(have attached the output also in result folder 
    for comparison)
  
* I've trained the model for 10 epochs on 64x64 images, achieving better results than before, including the generation of facial features. I'll now restart the model from this 10-epoch checkpoint and compare the results after 20 epochs; if the outcome improves, I'll continue training the model further, otherwise, I'll resume training after making some updates.
