# SoundScape AI — Audio Modeling Experiments
حين تُروى المشاهد بالأصوات

**What if a rain sound could be made lighter, calmer, or farther away just by asking?**

Text-to-audio models can generate environmental sounds from text prompts, but how much control do we really have over the characteristics of the generated audio?

In SoundScape AI, We explored this question through **AudioLDM 2** and **LoRA fine-tuning**, focusing on two perceptual dimensions: **intensity** and **comfort**.

We experimented with fine-tuning the model, compared different configurations against the original pretrained model, and investigated whether these adaptations could improve text-guided control over environmental sounds.

## Project Overview

This repository focuses on the audio modeling experiments conducted as part of SoundScape AI.

The work investigates whether a pretrained text-to-audio model can be adapted to generate environmental sounds with different perceptual characteristics, rather than simply generating sounds that match a general category.

The experiments focused on:

- **Intensity:** Generating sounds with light, moderate, and heavy intensity.
- **Comfort:** Exploring the distinction between calm and harsh environmental sounds.
- **Model Adaptation:** Using LoRA to fine-tune AudioLDM 2 while keeping the number of trainable parameters relatively small.
- **Evaluation:** Comparing fine-tuned models against the original model to examine whether the adaptations produced meaningful changes.

## Dataset

The experiments used **200 audio clips from ESC-50**, covering five environmental sound categories:

- Rain
- Sea waves
- Wind
- Flowing water
- Thunderstorm

Since ESC-50 does not provide labels for perceptual attributes such as intensity and comfort, we derived these labels for our experiments based on audio characteristics.
The dataset preparation included:

- Audio inspection and quality checks.
- Duplicate detection.
- Split integrity validation.
- Silence and clipping analysis.
- Audio feature extraction.

## Model and Methodology

**Base Model:** AudioLDM 2  
**Fine-tuning Method:** Low-Rank Adaptation (LoRA)

The pretrained model was adapted through separate experiments targeting intensity and comfort.

Rather than fine-tuning the entire model, LoRA was applied to selected cross-attention layers in the U-Net, allowing a smaller number of parameters to be trained.

The experiments were conducted in stages to examine the effect of training duration, task-specific labels, and control configurations.

## Experiments

### Experiment 1 — Initial LoRA Fine-tuning

The first experiment investigated whether LoRA could adapt AudioLDM 2 to the two target dimensions.

Two separate adapters were trained:

- Intensity
- Comfort

Each adapter was trained for **150 steps**.

The experiment involved approximately **1.59 million trainable parameters**, representing around **0.45% of the U-Net parameters**.

**Observations:**

- Validation loss decreased from 0.0526 to 0.0506.
- The intensity adapter showed the expected direction of change in 4 out of 5 evaluated classes.
- However, the distance between generated and real audio was higher for the adapter (3.9 dB) than for the original model (2.5 dB).
- The comfort adapter did not establish a reliable distinction between calm and harsh sounds.

The decrease in validation loss alone was therefore insufficient to demonstrate improved perceptual control.

### Experiment 2 — Extended Fine-tuning and Control Experiment

The second experiment extended training to **300 steps** and introduced a control condition to investigate whether the model was learning meaningful relationships between text labels and audio characteristics.

Three adapters were evaluated:

- Intensity V2
- Comfort V2
- Shuffled Captions V2 (control)

The shuffled-caption experiment was particularly important: it helped examine whether the observed changes were related to the semantic relationship between captions and audio, or simply to adapting the model to the audio data.

**Observations:**

- Test loss decreased by approximately 4.7–5.2% across the three adapters.
- Similar loss reductions were observed in the task-specific adapters and the shuffled-caption control.
- This made it difficult to attribute the improvements to learning meaningful text-audio relationships.

The results raised an important question: was the model learning the intended perceptual relationships, or was it mainly adapting to the training data?

## Evaluation

The goal was to test whether LoRA fine-tuning could improve AudioLDM 2's control over sound intensity and comfort through text prompts.

### Quantitative Evaluation

The fine-tuned models were compared with the original model using audio-based measurements.

To account for natural variation in generation, the original model was evaluated across six random seeds.

In the extended intensity experiment, the original model moved in the expected direction in **13 out of 15 comparisons**, compared with **12 out of 15** for Intensity V2. Fine-tuning did not improve performance over the original model in this evaluation.

### Blind Listening Evaluation

We also listened to and compared the generated audio samples to examine their perceptual differences.

A blind listening package was prepared with **20 audio clips and 15 intensity comparisons**, along with rating templates.

## Key Findings

- **Lower loss did not mean better control.** Reductions in validation and test loss did not demonstrate more accurate generation of the intended intensity and comfort characteristics.

- **The original model remained competitive.** Intensity V2 did not outperform the pretrained model in the extended evaluation.

- **Shuffled captions raised questions about what the model learned.** Similar loss reductions across task-specific and shuffled-caption adapters did not provide clear evidence that the model learned meaningful text-audio relationships.

**Overall, the experiments did not demonstrate reliable text-guided control over intensity and comfort. They showed that lower loss alone is not enough to establish improvements in generated audio.**


## Full Project Repository

For the complete SoundScape AI project, visit:

**[SoundScape AI — Main Project Repository](https://github.com/LeenAlaslani/SoundScape-AI)**


 [the live studio](https://soundscape-ai-studio.onrender.com/)

<img width="1440" height="1479" alt="image" src="https://github.com/user-attachments/assets/010e5332-5495-445b-9c6c-4cf22386d75d" />
