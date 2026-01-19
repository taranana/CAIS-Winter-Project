# Sarcasm Detection in News Headlines using BERT

**Name:** Taran Anand
**E-mail:** taranana@usc.edu


---
## Project Overview:
The goal of this project was to distinguish between sarcastic and non-sarcastic headlines. Using a pre-trained transformer-based architecture (BERT), the model learned to differentiate between the two types of headlines by learning contextual clues for inference.
---

## Dataset:
The dataset used for this project was the **News Headlines for Sarcasm Detection** dataset compiled by Rishabh Misra, publically available on Kaggle. The sarcastic headlines were taken from **The Onion**, and the non-sarcastic headlines were taken from **HuffPost**.

Each data sample included:
- 'headline': the text in the headline itself
- 'is_sarcastic': a binary label (1 = sarcastic, 0 = not sarcastic)
- 'article_link': a link to the original article

### Preprocessing:
The dataset was provided in json format and loaded line-by-line. Only the 'headline' and 'is_sarcastic' fields were necessary as the article content itself does not prove valuable to the purpose of the project. Only headlines were used because full articles would extend training time at far too little reward, possibly hindering model performance due to the nature of news articles. Articles are typically formulated with most of the article being factual data, and similarities between sarcastic headline articles and non-sarcastic headline articles would make the model perform worse when distinguishing the two. The argument could be made that sarcastic sentences within the article could help improve model performance; however, the sarcastic sentence number far too few compared to the non-sarcastic sentences to make sampling entire articles a viable idea. Headlines were then tokenized using the BERT-tokenizer with truncation and padding for a maximum sequence length of 64 tokens. This length was chosen due to the shorter nature of headlines compared to other longer forms of samples used in NLP. Limiting the sequence length also improves training efficiency. The dataset was also split into training and testing data using the conventional 80/20 train-test split.

## Model Development and Training
I used **BERT-base-uncased** because of its strong performance on sentence-level tasks, especially with its ability to understand nuanced contextual relationships, which is necessary for sarcasm detection.

### Training Details
- **Model:** BERT-base-uncased
- **Loss Function:** Cross-Entropy Loss
- **Optimizer:** AdamW
- **Learning Rate:** 2e-5
- **Batch Size:** 16
- **Epochs:** 3
- **Hardware:** Google Colab T4 GPU Runtime

These are standard hyperparameters; however, I reduced the number of epochs for training as it seemed to converge around 3 epochs and extended the training time seemed pointless as each epoch would take around 5 minutes to train.

## Model Evaluation and Results
To evaluate the model's performance, I used accuracy, precision, recall, and F1-Score. F1-Score is the most important metric as nuanced NLP tasks like sarcasm detection often have false positives and false negatives.


               precision    recall  f1-score   support

    Not Sarcastic   0.92      0.95      0.94      2996
    Sarcastic       0.93      0.90      0.92      2346

     accuracy                           0.93      5342
    macro avg       0.93      0.92      0.93      5342
 weighted avg       0.93      0.93      0.93      5342

I also generated a confusion matrix based on the model's predictions which illustrated strong performance on both sarcastic and non-sarcastic headlines with failures on edge cases with subtleties too nuanced for the scope of the project.

## Discussion

### Model and Dataset Fit
The dataset fits the goal of the project well and proves to be well-suited for sarcasm detection in news headlines. However, a posisble pitfall lies in the fact that the model could be learning stylistic differences between **TheOnion** and **HuffPost** rather than a general understanding of sarcasm as a whole. However, BERT's contextual modeling capabilities still make it a strong model for this task.

### Limitation and Future Work
The main limitation for this project is that the data comes from only two sources. This may reduce generalizability. Moreover, sarcasm relies on broader context that sometimes is unavailable in headlines.

If I were to continue this project, next steps would include:
- Evaluating the model on more diverse datasets
- Exploring different possible models to reduce training time should the dataset and training methods expand
- Incorporating other features for sarcasm detection

---

## Conclusion
This project determines that BERT and other transformer-based models produce satisfactory results for sarcasm detection; however, further work could possibly determine stronger and more stable systems for this task.