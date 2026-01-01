# Hate-Speech-Detection in Roman Urdu

---

## Project Overview
This project addresses the challenge of detecting hate speech in Roman Urdu (RU), a low-resource linguistic environment commonly used on social media. RU is particularly difficult to analyze due to several factors:
* Non-standardized orthography: Multiple spellings for the same word, such as "kya", "kia", and "kiya".
* Code-mixing: Frequent switching between Urdu and English.
* Subjective boundaries: Difficulty in distinguishing between subtle levels of toxicity, such as "offensive" versus "hostile".

The research validates a methodology centered on problem simplification (binary classification) and custom data normalization using Transformer-based models.

---

## Dataset and Preprocessing
The study utilized a dataset of 8,569 text samples. 

### Custom Normalization Pipeline
A critical component of this project is the rule-based Roman Urdu Normalization Pipeline designed to reduce sparsity and noise caused by spelling variability. 
* Phase A (Raw Data): Training on uncorrected text to establish a benchmark for noise impact.
* Phase B (Normalized Data): Training on text where variant spellings and abbreviations were unified to improve model robustness.

### Feature Engineering
Before modeling, the following structural features were analyzed for correlation with content severity:
* Word and Character Count
* Caps Ratio and Punctuation Count
* Lexical Diversity

---

## Methodology: The Three Analogies
The implementation followed a progressive three-stage approach:

| Stage | Task | Outcome |
| :--- | :--- | :--- |
| Analogy 1 | Exploratory Multi-Class: Fine-tuning transformers on four labels: Hate, Offensive, Hostile, and Neutral. | Suffered from high misclassification rates due to label ambiguity and data scarcity in minority classes. |
| Analogy 2 | Simplified Binary: Re-engineering the task into "Abusive" vs. "Neutral" by merging toxicity categories. | Significantly reduced ambiguity and improved class balance, establishing a higher performance baseline. |
| Analogy 3 | Optimized Transformers: Fine-tuning advanced models (Hing-BERT, XLM-RoBERTa) on binary, normalized data. | Achieved optimal performance and set a new benchmark for Roman Urdu NLP. |

---

## Implementation Details
* Model Selection: Focused on the BERT family, specifically Hing-BERT, mBERT, and XLM-RoBERTa-base.
* Tokenization: Utilized AutoTokenizer with a maximum sequence length of 128 tokens.
* Training: Leveraged the Hugging Face Trainer with a learning rate of 2e-5 and EarlyStopping (patience of 2 epochs) to prevent overfitting.
* Evaluation Metric: The Macro F1-Score was used for balanced assessment, with a specific focus on Recall for the 'Abusive' class to ensure effective content filtering.

---

## Results and Discussion
The integration of data normalization and domain-specific models led to significant and consistent performance gains.

### Performance Comparison (Binary Task)
| Model | Data State | Macro F1-Score | Toxic Recall |
| :--- | :--- | :--- | :--- |
| Hing-BERT | Raw (Phase A) | 0.825 | 0.771 |
| Hing-BERT | Normalized (Phase B) | 0.869 | 0.844 |

**Key Findings**: 
* The custom Normalization Pipeline provided an improvement of approximately 4.4% in Macro F1-Score. 
* Hing-BERT outperformed XLM-RoBERTa, likely due to its domain-specific pre-training on Indic languages, providing embeddings better aligned with the Roman Urdu lexicon.

---

## Conclusion and Future Work
This study successfully established a robust methodology for Roman Urdu hate speech detection by validating a two-part strategy: problem simplification and aggressive data normalization. 

Future work will focus on utilizing generalized Transformer architectures to address remaining linguistic challenges, such as sarcasm and irony, through targeted data augmentation or continued pre-training.

---

## References
* [1] Shahzad Khan et al., "Hate Speech Detection in Roman Urdu," ACM Transactions on Asian and Low-Resource Language Information Processing, 2021.
* [2] Jacob Devlin et al., "BERT: Pre-training of Deep Bidirectional Transformers for Language Understanding," 2019.
* [3] Akshat Gaurav et al., "XLM-RoBERTa Based Sentiment Analysis of Tweets on Metaverse and 6G," ScienceDirect.
