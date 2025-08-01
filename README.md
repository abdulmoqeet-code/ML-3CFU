
#  Real-ESRGAN Super-Resolution Project

## Project Summary

This project aimed to convert **low-resolution (LR) images** into **high-resolution (HR) images** using a deep learning model called **Real-ESRGAN (Real Enhanced Super-Resolution Generative Adversarial Network)**.

By the end of the project, I successfully trained and fine-tuned an ESRGAN model that could generate detailed and visually appealing high-resolution images from blurry, low-quality inputs.



## How It Works

The ESRGAN model is made up of two main parts:

###  Generator (G)

* The generator takes a blurry image and tries to create a sharp, high-quality version of it.
* I used a **pretrained RRDB-based generator** and **fine-tuned it** on a custom dataset.
* Initially, only the last layer was trainable. Later, I unfroze more layers to help the model adapt better.

###  Discriminator (D)

* The discriminator checks whether an image is real (from the dataset) or fake (from the generator).
* It helps the generator improve by pointing out the differences.
* This model was **trained from scratch**, without any pretrained weights.


##  Code Workflow

1. **Data Preparation**

   * I used around 8,000 HR images and generated corresponding LR versions.
   * Applied data augmentations like flipping, rotation, and color jittering.
   * Worked with two image sizes:

     * 32×32 → 128×128
     * 64×64 → 256×256

2. **Model Setup**

   * Loaded a pretrained generator (RRDBNet).
   * Built a custom discriminator from scratch.
   * Set up loss functions: content loss, adversarial loss, and perceptual loss.

3. **Training**

   * Trained both models together using adversarial training.
   * Saved intermediate results for evaluation.
   * Applied techniques like label smoothing, dropout, and selective layer unfreezing to balance training.

4. **Evaluation**

   * Compared generated images visually and tracked generator/discriminator loss curves.
   * Achieved clearer textures, improved facial features, and more stable training performance over time.



##  Key Challenges & Solutions

###  Discriminator Getting Too Strong

* Problem: The discriminator quickly learned to spot fake images, making it hard for the generator to improve.
* Solutions:

  * Added **dropout** to slow down its learning.
  * Trained the discriminator **less frequently** (every other epoch).
  * Used **label smoothing** to make it less confident.

###  Generator Plateauing

* Problem: After a few epochs, the generator stopped improving.
* Solutions:

  * Increased the weight of **perceptual loss** (although this had limited effect).
  * **Unfroze more layers** of the generator to give it more flexibility.
  * Continued training from a 10-epoch checkpoint and saw better image quality after 20 epochs.



## Final Results

* Trained on 64×64 → 256×256 images with 8K dataset.
* Generator produced sharper, more detailed outputs than in early stages.
* Generated images started showing clear facial features and better textures.
* Resolved instability issues in early training stages.
* The 64×64 model worked well even on 32×32 images, but not the other way around.





## Conclusion

This project successfully demonstrated how to apply **REAL-ESRGAN** with **transfer learning** and **custom training strategies** to enhance image resolution. Throughout the project, I explored various ways to fix training imbalance, stabilize adversarial learning, and improve visual output quality.
