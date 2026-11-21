# SoundScape AI: Can a Text Prompt Control How Nature Sounds?
عندما تصبح للمشهد صوت

> **What if a rain sound could be made lighter, calmer, or farther away just by asking?**

People use nature sounds to relax, sleep and focus. But a recording is fixed: you cannot ask it to be lighter, or ask a thunder to be farther away.

That led to our **research question**:

**Can a small fine-tuning teach a text-to-audio model to follow words like *light*, *heavy*, *calm*, and *harsh*?**

## Method

Using the pretrained [**AudioLDM 2**](https://huggingface.co/cvssp/audioldm2) and [**200 ESC-50 clips**](https://github.com/karolpiczak/esc-50) (rain, sea waves, wind, flowing water, thunderstorm), we:

- Built on the generation pipeline [complete project files](https://github.com/LeenAlaslani/SoundScape-AI) (candidate selection, mastering, 60-second loops, mixer).
- Checked the data: no duplicate files, no source shared between splits, 10 clips with padded silence and 31 with clipping.
- Created intensity labels (*light*, *moderate*, *heavy*) and comfort labels (*calm*, *harsh*) from the audio itself, because ESC-50 has no captions.
- Trained two **LoRA** adapters on the cross-attention layers (**1.59M** trainable parameters, about **0.45%** of the U-Net).
- Tested each adapter against the original model with intensity and comfort prompts.


## Results

- Validation loss dropped by about **4%** (0.0526 → 0.0506), almost the same for both adapters.
- **Intensity:** 4 of 5 classes moved in the right direction for both the original model and the adapter, and the adapter was not closer to the real clips (**3.9 dB** gap vs **2.5 dB**).
- **Comfort:** calm prompts did not sound calmer than harsh prompts.

| Model | Calm prompt | Harsh prompt |
|---|---:|---:|
| Original | 0.51 | 0.48 |
| Comfort adapter | 0.59 | 0.53 |

*Average harshness score (0 = calm, 1 = harsh).*

## Conclusion

In our experiments, 

[try ](https://soundscape-ai-studio.onrender.com/)
<img width="1440" height="1479" alt="image" src="https://github.com/user-attachments/assets/010e5332-5495-445b-9c6c-4cf22386d75d" />
