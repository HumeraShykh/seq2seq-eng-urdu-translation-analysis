# seq2seq-eng-urdu-translation-analysis
Seq2Seq performance analysis for English–Urdu translation using Google Translate and Meta M2M100 with BLEU and ROUGE evaluation


# Eng → Urdu Translation Evaluation (Seq2Seq Performance Analysis)

This project evaluates **English-to-Urdu translation quality** by comparing:
- **Google Translator** (via `deep-translator`)
- **Meta/Facebook Seq2Seq model**: `facebook/m2m100_418M` (HuggingFace Transformers)

The translations are compared against **ground-truth Urdu references** from the provided Eng–Ur dataset using:
- **BLEU**
- **ROUGE-1 / ROUGE-2 / ROUGE-L** (Urdu-friendly token-based F1)

---

## Dataset
- Total evaluated sentence pairs: **24,524**

> Note: Source and reference sentences were paired line-by-line from the provided corpus files, using the minimum common length.

---

## Method
1. Load Eng–Ur dataset and build a dataframe with:
   - `english` (source)
   - `urdu_ref` (reference / ground truth)
2. Generate model outputs:
   - `urdu_google` using Google Translator
   - `urdu_meta` using Meta M2M100 Seq2Seq (batch translation on GPU when available)
3. Compute metrics:
   - Sentence-level BLEU + dataset average BLEU
   - Sentence-level ROUGE-1/2/L F1 + dataset averages (Urdu-friendly whitespace tokenization)

---

## Results (Averages)

### BLEU (Average)
| System | Avg BLEU |
|--------|----------|
| Google Translator | **13.8202** |
| Meta (M2M100) | **6.2135** |

### ROUGE (Average F1)
| System | ROUGE-1 | ROUGE-2 | ROUGE-L |
|--------|---------|---------|---------|
| Google Translator | **0.16567** | **0.12070** | **0.16526** |
| Meta (M2M100) | **0.11286** | **0.04172** | **0.11149** |

---

## Conclusion
Based on both **Average BLEU** and **ROUGE-L**, **Google Translator performs better** than the Meta M2M100 model on this Eng→Ur dataset.

**Why Google likely wins here (brief):**
- Better handling of common Urdu phrasing and word choice in general-domain sentences  
- More fluent outputs and higher overlap with ground-truth references (reflected in ROUGE-L)

---

## Reproducibility
### Install
```bash
pip install -r requirements.txt
