# Product-Review-Sentiment-Classifier

## Error Analysis

Across the seven examples where both models failed (1 positive, 1 negative, 5 neutral), the errors share a few causes: **mixed or balanced sentiment** (praise and complaints in one review), **hedged or negated wording** such as "not bad, but nothing special" that token-level cues read as negative, and **sentiment carried by events rather than opinion words** (e.g. an insect found in the soup). Some "errors" are probably **label noise**: the text of two neutral examples is clearly positive but carries a 3-star label, so the models may be right and the rating wrong. In several cases DistilBERT was wrong with 0.90 or higher confidence, which shows its probabilities are not a reliable signal without calibration.

## Model Comparison Verdict

For real-time support triage I recommend **DistilBERT**: it made fewer errors than TF-IDF + Logistic Regression on the identical test split (510 vs 558 of 2,400) and far fewer costly negative→positive mistakes, and its CPU latency of **[Z] ms per review** is well within a real-time budget. TF-IDF + LR would only be the better choice if hardware were too limited to run a transformer, and neutral predictions should go to human review for either model.
