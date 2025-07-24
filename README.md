# 📰 News Article Summarization using NLP

This project fine-tunes the `facebook/bart-large-cnn` transformer model on the **CNN/DailyMail** dataset to generate concise, factually accurate news summaries. It compares **abstractive** (BART) and **extractive** (TextRank) summarization approaches, evaluates results using ROUGE metrics, and explains predictions using LIME and attention visualizations.

---

## 📚 Dataset

- **Source**: [CNN/DailyMail](https://huggingface.co/datasets/cnn_dailymail) via `datasets` library  
- **Size**: 287,113 articles  
- **Fields**: Each sample contains `article`, `highlights` (summary), and `id`

---

## 🏗️ Model Architecture

- **Model**: `facebook/bart-large-cnn`  
- **Tokenizer**: `BartTokenizer`  
- **Preprocessing**:
  - Lowercasing
  - Rare word replacement
  - Truncation (max input: 512 tokens)
- **Training Setup**:
  - Fine-tuned using `Seq2SeqTrainer`
  - Trained on a sample subset (demo scale) for performance prototyping

---

## ⚙️ Training Configuration

- **Batch Size**: 1  
- **Epochs**: 1  
- **Max Input Length**: 512  
- **Max Output Length**: 128  
- **Optimizer**: AdamW via Hugging Face Trainer  
- **Environment**: Google Colab (GPU)

---

## 🧪 Evaluation

| Metric       | BART Score |
|--------------|------------|
| ROUGE-1      | **0.4171** |
| ROUGE-2      | **0.1850** |
| ROUGE-L      | **0.2763** |
| ROUGE-Lsum   | **0.3536** |

✅ BART **outperformed** the TextRank baseline in all ROUGE metrics, demonstrating improved summary accuracy and informativeness.

---

## 🔬 Explainability


- **Attention Heatmap**: Visualizes encoder-decoder token attention to highlight focus during generation.

---

## 🧠 Example Summaries

```plaintext
📌 Actual: Harry Potter star Daniel Radcliffe gets £20M fortune as he turns 18 Monday . Young actor says he has
no plans to fritter his cash away . Radcliffe's earnings from first five Potter films have been held
in trust fund .
🔹 BART: Harry Potter star Daniel Radcliffe turns 18 on Monday . He has a reported fortune of $41.1 million .
Radcliffe says he has no plans to fritter his money away . The actor says he will have a "some sort
of party" in honor of his birthday .
📎 TextRank: Daniel Radcliffe as Harry Potter in "Harry Potter and the Order of the Phoenix" To the
disappointment of gossip columnists around the world, the young actor says he has no plans to
fritter his cash away on fast cars, drink and celebrity parties. At 18, Radcliffe will be able to
gamble in a casino, buy a drink in a pub or see the horror film "Hostel: Part II," currently six
places below his number one movie on the UK box office chart. His latest outing as the boy wizard in
"Harry Potter and the Order of the Phoenix" is breaking records on both sides of the Atlantic and he
will reprise the role in the last two films.

