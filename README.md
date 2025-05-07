# README for Relation Extraction Project

## Introduction

This repository contains two different approaches (Method 1 and Method 2) for performing Relation Extraction (RE) on the TACRED dataset.

- **Method 1 (`method1.ipynb`)** uses a hybrid model that combines a BiLSTM with attention, rule-based features, and SVM-style TF-IDF features in a unified architecture.
- **Method 2 (`method2.ipynb`)** uses a transformer-based approach (e.g., BERT) for sequence classification, fine-tuned for relation extraction.

## Repository Structure

Below are the key files and folders in this repository (some files/folders might be omitted for brevity):

- **`method1.ipynb`**  
  Contains the hybrid BiLSTM + Rule-based + TF-IDF RE model (a "unified" approach).

- **`method2.ipynb`**  
  Contains the transformer-based (`BERT`/`AutoModel`) approach to RE.

- **`dataset/`**  
  Where the TACRED dataset JSON files should be placed (`dev.json`, `test.json`, `train.json`).

- **`models/`**  
  Used by `method1.py` to save/load its unified model checkpoints.

- **`outputs/`**  
  Used by `method2.py` to save/load checkpoints (`best_model/`, `checkpoint-xxxx/`) and logs.

- **`glove.6B.300d.txt`**  
  The pretrained GloVe embeddings file (300-dimensional). Must be placed in the project’s main directory if using Method 1.

- **`README.md`**  
  This file.

## Prerequisites and Installation

1. **Python 3.7+** (recommended)

2. **Create and activate a virtual environment** (optional but recommended):

   ```bash
   python3 -m venv venv
   source venv/bin/activate    # Linux/Mac
   # or
   venv\Scripts\activate       # Windows

   ```

3. **Install the required packages**:
   ```bash
   pip install -r requirements.txt

   ```
4. **Download the necessary files** (see "Downloads and Setup below").

5. To use spaCy for advanced tokenization in Method 1, install the English model:
   ```bash
   python -m spacy download en_core_web_sm
   ```

## Downloads and Setup

You will need the following large files:

To download files click [here](https://www.dropbox.com/scl/fo/w0k1zl3c8xzn4u3miu8uu/ADVnCnBYbIl3mSLMANy5dE0?rlkey=cilyla90h0bk1gz86yaparuxd&e=1&st=qav0rtqr&dl=0).

1. **TACRED Dataset** (`dev.json`, `test.json`, `train.json`)

   - Download from the provided cloud link.
   - Place them in the `dataset/` directory.
   - Example structure:
     ```
     dataset/
       ├─ dev.json
       ├─ test.json
       └─ train.json
     ```

2. **GloVe Embeddings** (`glove.6B.300d.txt`) (~1 GB)

   - Download from the provided cloud link (or from a standard source if you already have it).
   - Place `glove.6B.300d.txt` in the main project folder (same directory level as `method1.py`).

3. **Pre-trained Model Files (Checkpoints)**

   - **Method 1** (BiLSTM + Rule-based + TF-IDF): Place the final checkpoint (e.g., `best_unified_model.pth`) in `models/` (e.g., `models/best_unified_model.pth`).
   - **Method 2** (Transformer-based): Place the final checkpoint directory (e.g., `best_model/`) in `outputs/`, containing the config files and model weights.

   By default, the code expects:

   - Method 1: `models/best_unified_model.pth`
   - Method 2: `outputs/best_model/`

   If you place them elsewhere, adjust paths in the code accordingly.

---

## Running the Code

### Method 1 (Hybrid BiLSTM + Rule-based + TF-IDF)

1. Ensure you have the correct environment and that `glove.6B.300d.txt` is in the project root.
2. Make sure `dataset/` contains `train.json`, `dev.json`, and `test.json`.
3. If you wish to train from scratch, uncomment the training lines in `method1.ipynb` (in the “Training Phase” section).

### Method 2 (Transformer-based BERT/AutoModel)

1. Ensure the TACRED data is in `./dataset/`.
2. Place the trained model folder (e.g., `best_model/`) in `./outputs/`.
3. If you want to train, uncomment the training lines in `method2.ipynb`.

## Inference with Custom Inputs

- **Method 1**  
  Look for the “Example prediction on a few test instances” section in `method1.ipynb`, where you can tailor the code to new inputs by defining the tokenized text and subject/object spans.

- **Method 2**  
  After loading the best checkpoint in `method2.ipynb`, modify the “Inference Mode” section to build your own text examples and run them through the model in a similar manner.

---

## Troubleshooting

- Verify you have installed all Python dependencies in a virtual environment.
- Double-check the dataset, models and GloVe file paths against those set in the code.
- If CUDA memory errors occur, reduce the `batch_size` or sequence length.
- If using spaCy, make sure you have run:
  ```bash
  python -m spacy download en_core_web_sm
  ```
- Adjust any file paths if you place the dataset, GloVe embeddings, or model checkpoints in different locations.
