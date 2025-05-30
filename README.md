# Sentiment Analysis Using Transformer-Based Hybrid Models T5 and RoBERTa

## Overview

This project implements a hybrid sentiment analysis system combining T5 (a generative transformer) and RoBERTa (a discriminative transformer) to classify tweets into Positive, Neutral, or Negative categories. While T5 interprets sentiment via text generation, RoBERTa directly classifies the sentiment. A rule-based fusion strategy is used to enhance prediction consistency and handle ambiguity, resulting in superior performance compared to standalone models.

## Model Architecture

- T5: Fine-tuned using a text-to-text format with prompts like:  
  "Analyze Sentiment: <tweet_text>"  
  and trained to generate one of the sentiment labels as output.

- RoBERTa: Fine-tuned as a classification model, predicting probabilities across sentiment classes (positive, neutral, negative) using a softmax layer.

- Hybrid Decision Logic:  
  - If T5 and RoBERTa agree → their shared prediction is used.  
  - If they disagree → a precedence rule is applied:
    - Positive + Neutral → Neutral  
    - Negative + Neutral → Negative  
    - Positive + Negative → Neutral

## Evaluation 📈

The models were evaluated using a 70:30 train-test split from a cleaned Twitter sentiment dataset. The following metrics were used:

- Accuracy  
- Precision  
- Recall  
- F1 Score  
- Confusion Matrix  
- ROC Curve and AUC Score (One-vs-Rest)

## Results

| Model      | Accuracy | Precision | Recall | F1 Score | AUC  |
|------------|----------|-----------|--------|----------|------|
| RoBERTa    | 92.00%   | 91.77%    | 90.66% | 90.65%   | 0.95 |
| T5         | 93.33%   | 92.27%    | 91.55% | 91.89%   | 0.97 |
| Hybrid     | ✅ 96.00% | ✅ 95.33% | ✅ 95.11% | ✅ 95.21% | ✅ 0.97 |
