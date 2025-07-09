 **Experiment Summary & Observations**

 **Recent Improvements**

1. **Dataset Size **
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
   * **Observation**: Increasing image resolution mainly increases computation cost without significantly improving output quality. Needs more investigation.



 **Upcoming Experiments **

1. **Handling Discriminator Dominance**

   * Issue: Discriminator loss still approaches **zero after 5 epochs**, causing an **adversarial imbalance**.
   * Plan:

     * Introduce **dropout** in the discriminator to regularize learning.
     * Try **training the discriminator less frequently** (e.g., once every 2 epochs) to give the generator more room to improve.

2. **Improving Generator Guidance**

   * Issue: Generator loss becomes stagnant; likely due to overpowered discriminator or limited capacity to adapt.
   * Plan:

     * Increase **perceptual loss weight** in the combined loss to enhance **feature-level supervision**, helping the generator focus more on visual details.
     * **Unfreeze more layers** of the pretrained generator (currently only the last CNN layer is unfrozen) to allow it to **better adapt to the specific dataset**.

3. **Increasing Dataset**
   * Also will increase the dataset, most probably 8K
