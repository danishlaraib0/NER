This project involves training a Named Entity Recognition (NER) model to detect and classify various personally identifiable information (PII) entities in educational data, using a pre-trained transformer model (DeBERTa v3). Here's a high-level summary of the key components:
<br>
<h3>1. Dataset Preparation</h3>
The project starts by loading and combining multiple datasets related to PII detection, including datasets with both positive and negative samples (positive samples contain labeled PII entities, negative samples don't).
The dataset is then tokenized and preprocessed to extract useful information for the model, including text, tokenized tokens, and labels.
<h3>2. Tokenization and Preprocessing</h3>
The text is tokenized using a tokenizer from the Hugging Face transformers library.
Tokenization includes handling whitespace, converting tokens into ids, and preparing the data in a format suitable for model input (including offset mappings and token labels).
The labels are mapped to appropriate indices, and special tokens (e.g., [CLS], [SEP]) are handled to ensure they don't interfere with the model's predictions.
<h3>3. Model Training</h3>
A pre-trained DeBERTa v3 model is fine-tuned on the tokenized dataset for entity classification. The model is trained using the Trainer class, with customized training arguments (e.g., batch size, learning rate, evaluation strategy).
The training is done on sequences of tokens with a maximum length of 1024, but longer inputs are handled by splitting them into chunks (using stride) to avoid truncation of important context.
<h3>4. Inference and Prediction</h3>
The trained model is used to predict PII entities (e.g., email, phone number, student names) in new, unseen data (test set).
The predictions are processed using a threshold (e.g., 0.9) to make final decisions about which tokens are part of PII entities.
The predictions are mapped back to the original tokens and their corresponding labels, and token-level predictions are generated for each document.
<h3>5. Post-Processing</h3>
The predicted labels are stored along with the token IDs and the actual token strings in a DataFrame.
The DataFrame is further enriched with a unique row_id for each entry to ensure each prediction is tracked and can be analyzed or exported.
<h3>6. Metrics and Evaluation</h3>
Evaluation is done using standard NER metrics such as precision, recall, and F1-score, which are calculated on the model's predictions to assess its performance on the task.
Outcome
The result is a fine-tuned NER model capable of detecting and classifying PII entities in text, which can be applied to various educational datasets for the purpose of sensitive data detection and removal.
This project demonstrates the application of transformer-based models for the task of PII detection and highlights how to effectively preprocess and fine-tune such models for specific entity classification tasks.
