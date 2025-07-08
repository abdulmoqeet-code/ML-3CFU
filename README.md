##  Project Overview

The core objective of this project is to build a deep learning model capable of converting **low-resolution (LR)** images into **high-resolution (HR)** images using **ESRGAN (Enhanced Super-Resolution Generative Adversarial Network)**.

The ESRGAN framework works in two main components:



### Generator (G)

* The generator's role is to **upscale** the input LR image into a high-resolution image that is visually convincing.
* It tries to **fool the discriminator** by generating images that look as real as possible.
* In this project, a **pretrained RRDB-based generator** is used (transfer learning), but the **last convolutional layers are unfrozen** and trained to better adapt to the new dataset.
* The goal is to progressively improve the generator’s ability to restore fine details and textures.



### Discriminator (D)

* The discriminator acts as a **critic**, distinguishing between real HR images (ground truth) and fake HR images (produced by the generator).
* Unlike the generator, **the discriminator is trained from scratch**, without any pretrained weights.
* Its output is used to compute **adversarial loss**, which helps the generator improve by highlighting where its outputs fall short of looking real.



### Training Imbalance Issue

Currently, training shows signs of **imbalance**:

* The discriminator quickly becomes too strong and achieves **near-zero loss**, indicating it can easily tell apart fake images.
* This implies the generator is **struggling to improve**, as it’s not receiving useful gradients from the discriminator.
* A possible reason could be the use of transfer learning in the generator while the discriminator starts from scratch, leading to **unstable adversarial training**.

I am Investigating this issue...


