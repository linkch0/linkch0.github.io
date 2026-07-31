---
icon: material/face-recognition
tags: [Updating]
comments: true
---

# Deepfake Research

Ref: <https://github.com/flyingby/Awesome-Deepfake-Generation-and-Detection>

## Problem Definition

### Deepfake Generation

Deepfake Generation tasks can essentially be expressed as controlled content generation problems under specific conditions, such as images, audio, text, specific attribute.

$$
I_o = {\bm{\phi_{G}}}(I_{t}, C)
$$

- Target image $I_t$
- Condition information $C = \{ \mathtt{Image}, \mathtt{Audio}, \mathtt{Text}, \dots \}$
- Generation network $\phi_{G}$
- Output image $I_o$

### Deepfake Detection

Deepfake Detection tasks can be viewed as an image-level or pixel-level classification problem.

$$
S_o = {\bm{\phi_{D}}}(I_{o}),
$$

- Detection network $\phi_{D}$
- Fake score $S_o$

### Tasks

1. Face Swapping
    - Replacing the identity of the target face with that of the source face
    - Maintaining target-specific, ID-irrelevant attributes such as skin tone and expressions

2. Face Reenactment
    - Transferring the facial movements from a driving image or video to a target image
    - Keeping the target's identity and attributes unchanged
    - Relying on facial motion capture techniques

3. Talking Face Generation
    - Generating a talking video for a target image driven by audio, text, or multimodal inputs
    - Accurately reflecting the driving information, including lip motion, facial pose, emotions, and spoken content

4. Facial Attribute Editing
    - Modifying semantic attributes of a target face (e.g., age, expression, or skin tone)

5. Forgery Detection
    - Detecting and localizing tampering or forged regions in images or videos

## Methods

### Generative Framework

See [AIGC](../notes/Techniques/AIGC.md) for more details.

## Datasets

## Metrics

### Peak Signal-to-Noise Ratio (PSNR)

### Structured Similarity (SSIM)
