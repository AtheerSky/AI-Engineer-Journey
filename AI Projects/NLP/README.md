# Under One Sky: How Arabic Words Are Represented in Similar Contexts

> **Can two words mean the opposite, yet look similar to an AI model?**
Words can share the same context without sharing the same meaning. A word like *love* and its opposite, *hate*, can appear in very similar sentences. But does a language model recognize the difference in meaning, or does it mainly learn from the contexts in which words appear?

That led to our **research question**:

> **If a language model sees two words in similar contexts, will it place their representations close even if they differ in spelling and are opposite in meaning?**


## Method

Using [**UBC-NLP/ARBERT**](https://huggingface.co/UBC-NLP/ARBERT), we:

- Fine-tuned the model on an [Arabic Natural Language Inference (NLI) dataset](https://huggingface.co/datasets/Omartificial-Intelligence-Space/Arabic-NLi-Pair-Class)
- Extracted contextual word embeddings before and after fine-tuning.
- Compared synonyms, antonyms, and unrelated control words.
- Conducted two experiments using different sentence-frame designs.
- Used **Cosine Similarity** to measure representation similarity and **PCA** for visualization.

  
## Results

**Experiment 1:**

| Relationship | Before | After |
|---|---:|---:|
| Synonyms | 0.7746 | 0.8221 |
| Antonyms | 0.8443 | 0.7561 |
| Control | 0.6962 | 0.5490 |

Synonym similarity increased, while antonym and control similarity decreased.

**Experiment 2:**

| Relationship | Before | After |
|---|---:|---:|
| Synonyms | 0.8240 | 0.7862 |
| Antonyms | 0.8258 | 0.7365 |
| Control | 0.6772 | 0.5588 |

In this experiment, similarity decreased across all categories, but synonyms remained closer to the reference words than antonyms.

<img width="947" height="381" alt="nlp1" src="https://github.com/user-attachments/assets/44ad52d6-a28b-4125-8f34-43863721a677" />
<img width="947" height="410" alt="nlp2" src="https://github.com/user-attachments/assets/0c5a4322-b154-4c57-98dc-24e9f137d09c" />

## Conclusion

In our experiments, ARBERT represented antonyms with similarity scores close to those of synonyms when the words appeared in similar contexts.
After NLI fine-tuning, similarity decreased across all groups in the second experiment, while antonyms remained more similar to reference words than unrelated control words in both experiments.
The effect on synonyms differed between the two experiments, highlighting the influence of sentence-frame design on the results.
