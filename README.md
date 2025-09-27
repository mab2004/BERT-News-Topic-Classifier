# 📰 BERT News Topic Classifier

## 🎯 Objective

The primary goal of this project was to **fine-tune a pre-trained transformer model (BERT)** for the task of **news headline classification**. The model classifies headlines into one of four categories: World, Sports, Business, or Sci/Tech. The final requirement was to deploy the functional model using **Streamlit** for a live, interactive demonstration.

## 🛠️ Methodology / Approach

### 1. Dataset & Preprocessing

* **Dataset:** Used the **AG News Dataset** from Hugging Face, which contains 120,000 training samples and 7,600 test samples across 4 classes.
* **Model:** The `bert-base-uncased` model was selected as the base transformer.
* **Preprocessing:** The dataset was tokenized using the BERT tokenizer, with text input truncated and padded to a fixed maximum length. The dataset was converted to the PyTorch format.
* **Reduced Training Set:** For faster iteration in the Colab environment, training was performed on a smaller, shuffled subset of **10,000 samples** for training and **1,000 samples** for evaluation.

### 2. Model Fine-Tuning

* **Architecture:** The `AutoModelForSequenceClassification` was loaded with `num_labels=4`.
* **Training Parameters:**
    * **Optimizer:** AdamW
    * **Learning Rate:** $2 \times 10^{-5}$
    * **Batch Size:** 16 (per device)
    * **Epochs:** 3
* **Framework:** The training and evaluation pipeline was built using the Hugging Face `transformers.Trainer`.

### 3. Deployment

The fine-tuned model and tokenizer were saved locally and then deployed as a web application using **Streamlit**. The application uses the `transformers` `pipeline` utility for streamlined prediction and was hosted publicly via **localtunnel** within the Google Colab environment.

## 📊 Key Results and Evaluation

The model was evaluated on the 1,000-sample evaluation set using **Accuracy** and **Weighted F1-Score**.

| Metric | Result |
| :--- | :--- |
| **Final Accuracy** | **92.00%** |
| **Weighted F1-Score** | **92.04%** |

### Detailed Classification Report

The model achieved high performance across all classes, with particularly strong results in the 'Sports' and 'World' categories.

| Class | Precision | Recall | F1-Score | Support |
| :--- | :--- | :--- | :--- | :--- |
| **World** | 0.96 | 0.91 | 0.93 | 266 |
| **Sports** | 0.98 | 0.98 | 0.98 | 246 |
| **Business** | 0.90 | 0.88 | 0.89 | 246 |
| **Sci/Tech** | 0.84 | 0.91 | 0.88 | 242 |
| **Macro Avg** | 0.92 | 0.92 | 0.92 | 1000 |

## 🚀 How to Run the App (Google Colab)

To run the Streamlit application and generate a public URL for live testing, execute the cells in the provided Jupyter Notebook (`[Your_Notebook_Name].ipynb`) sequentially.

The final block, which uses the `pkill` and `time.sleep(30)` commands, is critical for successfully establishing the localtunnel connection after the model loads.

**Steps to launch the Streamlit app:**

1.  Ensure all cells from **Setup** to **Deployment Files Setup** have been executed.
2.  Run the final block titled **Running the Streamlit App**.
3.  The output will provide a public URL (e.g., `your url is: https://spotty-peaches-lie.loca.lt`).
4.  Open the link and enter the tunnel password (which is the current Colab endpoint IP: `34.138.9.65`).

### Sample Interaction:

| Headline | Predicted Topic | Confidence Score |
| :--- | :--- | :--- |
| International Diplomatic Tensions Rise Over Trade Disputes | World | 0.9967 |
| New AI Model Demonstrates Advanced Problem-Solving Capabilities | Sci/Tech | 0.9900 |
| Stock Markets Reach New Highs Amid Economic Optimism | Business | 0.9934 |
