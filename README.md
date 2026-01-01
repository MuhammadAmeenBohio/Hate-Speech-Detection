# Hate-Speech-Detection in Roman Urdu

## Project Overview
[cite_start]This project addresses the challenge of detecting hate speech in **Roman Urdu (RU)**, a low-resource linguistic environment commonly used on social media[cite: 3, 12, 13]. RU is particularly difficult to analyze due to several factors:
* [cite_start]**Non-standardized orthography**: Multiple spellings for the same word, such as "kya", "kia", and "kiya"[cite: 4, 34].
* [cite_start]**Code-mixing**: Frequent switching between Urdu and English[cite: 4, 14].
* [cite_start]**Subjective boundaries**: Difficulty in distinguishing between subtle levels of toxicity, such as "offensive" versus "hostile"[cite: 4, 16].

[cite_start]The research validates a methodology centered on **problem simplification** (binary classification) and **custom data normalization** using Transformer-based models[cite: 10, 79].

---

## Dataset and Preprocessing
[cite_start]The study utilized a dataset of **8,569 text samples**[cite: 28]. 

### Custom Normalization Pipeline
[cite_start]A critical component of this project is the rule-based Roman Urdu Normalization Pipeline designed to reduce sparsity and noise caused by spelling variability[cite: 8, 32]. 
* [cite_start]**Phase A (Raw Data)**: Training on uncorrected text to establish a benchmark for noise impact[cite: 33].
* [cite_start]**Phase B (Normalized Data)**: Training on text where variant spellings and abbreviations were unified to improve model robustness[cite: 34, 35].

### Feature Engineering
[cite_start]Before modeling, the following structural features were analyzed for correlation with content severity[cite: 30]:
* [cite_start]Word and Character Count [cite: 30]
* [cite_start]Caps Ratio and Punctuation Count [cite: 30]
* [cite_start]Lexical Diversity [cite: 30]

---

## Methodology: The Three Analogies
[cite_start]The implementation followed a progressive three-stage approach[cite: 17, 43]:

| Stage | Task | Outcome |
| :--- | :--- | :--- |
| **Analogy 1** | [cite_start]**Exploratory Multi-Class**: Fine-tuning transformers (e.g., XLM-RoBERTa) on four labels: Hate, Offensive, Hostile, and Neutral[cite: 18, 45]. | [cite_start]Suffered from high misclassification rates due to label ambiguity and data scarcity in minority classes[cite: 19, 46]. |
| **Analogy 2** | [cite_start]**Simplified Binary**: Re-engineering the task into "Abusive" vs. "Neutral" by merging toxicity categories[cite: 7, 20, 48]. | [cite_start]Significantly reduced ambiguity and improved class balance, establishing a higher performance baseline[cite: 21, 49]. |
| **Analogy 3** | [cite_start]**Optimized Transformers**: Fine-tuning advanced models (Hing-BERT, XLM-RoBERTa) on binary, normalized data[cite: 22, 51, 66]. | [cite_start]Achieved optimal performance and set a new benchmark for Roman Urdu NLP[cite: 24, 80]. |

---

## Implementation Details
* [cite_start]**Model Selection**: Focused on the BERT family, specifically **Hing-BERT**, **mBERT**, and **XLM-RoBERTa-base**[cite: 8, 23, 51].
* [cite_start]**Tokenization**: Utilized `AutoTokenizer` with a maximum sequence length of **128 tokens**[cite: 39, 40].
* [cite_start]**Training**: Leveraged the Hugging Face Trainer with a learning rate of **2e-5** and **EarlyStopping** (patience of 2 epochs) to prevent overfitting[cite: 52, 76].
* [cite_start]**Evaluation Metric**: The **Macro F1-Score** was used for balanced assessment, with a specific focus on **Recall** for the 'Abusive' class to ensure effective content filtering[cite: 53, 57, 77].

---

## Results and Discussion
[cite_start]The integration of data normalization and domain-specific models led to significant and consistent performance gains[cite: 69].

### Performance Comparison (Binary Task)
| Model | Data State | Macro F1-Score | Toxic Recall |
| :--- | :--- | :--- | :--- |
| Hing-BERT | Raw (Phase A) | 0.825 | 0.771 |
| **Hing-BERT** | **Normalized (Phase B)** | **0.869** | **0.844** |

**Key Findings**: 
* [cite_start]The custom Normalization Pipeline provided an improvement of approximately **4.4% in Macro F1-Score**[cite: 70]. 
* [cite_start]**Hing-BERT** outperformed XLM-RoBERTa, likely due to its domain-specific pre-training on Indic languages, providing embeddings better aligned with the Roman Urdu lexicon[cite: 72, 73].

---

## Conclusion and Future Work
[cite_start]This study successfully established a robust methodology for Roman Urdu hate speech detection by validating a two-part strategy: **problem simplification** and **aggressive data normalization**[cite: 79]. 

[cite_start]Future work will focus on utilizing generalized Transformer architectures to address remaining linguistic challenges, such as **sarcasm and irony**, through targeted data augmentation or continued pre-training[cite: 81].

---

## References
* [cite_start][1] Shahzad Khan et al., "Hate Speech Detection in Roman Urdu," ACM Transactions on Asian and Low-Resource Language Information Processing, 2021[cite: 83].
* [cite_start][2] Jacob Devlin et al., "BERT: Pre-training of Deep Bidirectional Transformers for Language Understanding," 2019[cite: 83].
* [cite_start][3] Akshat Gaurav et al., "XLM-RoBERTa Based Sentiment Analysis of Tweets on Metaverse and 6G," ScienceDirect[cite: 83].
