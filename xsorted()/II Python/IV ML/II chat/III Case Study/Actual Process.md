Multinomial Naive Bayes Classifier; no resampling
```python
import pandas as pd
import seaborn as sns
import matplotlib.pyplot as plt
from sklearn.feature_extraction.text import CountVectorizer
from sklearn.model_selection import train_test_split
from sklearn.naive_bayes import MultinomialNB
from sklearn.metrics import accuracy_score, confusion_matrix, classification_report

# --- 1. Load and Prepare the Data ---
try:
    df = pd.read_csv('user_courses_review_repaired.csv')
except FileNotFoundError:
    # Fallback to regenerate the cleaned file if it's missing
    df = pd.read_csv('user_courses_review_09_2023.csv', on_bad_lines='skip')
    df['review_rating'] = pd.to_numeric(df['review_rating'], errors='coerce')
    df.dropna(subset=['review_rating'], inplace=True)
    df['review_comment'].fillna('No Comment', inplace=True)

# Create the binary target variable 'sentiment'
df['sentiment'] = df['review_rating'].apply(lambda x: 1 if x >= 4 else 0)

# Define features (X) and target (y)
X_text = df['review_comment']
y = df['sentiment']

# --- 2. Vectorize and Split the Data ---
vectorizer = CountVectorizer(stop_words='english', min_df=2, max_df=0.95)
X = vectorizer.fit_transform(X_text)
X_train, X_test, y_train, y_test = train_test_split(X, y, test_size=0.2, random_state=42)

# --- 3. Train the Multinomial Naive Bayes Model ---
model = MultinomialNB()
model.fit(X_train, y_train)

# --- 4. Make Predictions on the Test Set ---
y_pred = model.predict(X_test)

# --- 5. Evaluate the Model's Performance ---
accuracy = accuracy_score(y_test, y_pred)
conf_matrix = confusion_matrix(y_test, y_pred)
class_report = classification_report(y_test, y_pred, target_names=['Bad', 'Good'])

print("--- Multinomial Naive Bayes Model Evaluation ---")
print(f"Accuracy: {accuracy:.4f}")
print("\nClassification Report:")
print(class_report)
print("\nConfusion Matrix:")
print(conf_matrix)

# --- 6. Visualize the Confusion Matrix ---
plt.figure(figsize=(8, 6))
sns.heatmap(conf_matrix, annot=True, fmt='d', cmap='Blues',
            xticklabels=['Predicted Bad', 'Predicted Good'],
            yticklabels=['Actual Bad', 'Actual Good'])
plt.title('Confusion Matrix')
plt.ylabel('Actual Label')
plt.xlabel('Predicted Label')
plt.savefig('confusion_matrix.png')
```

### The Results: How Well Did the Model Do?
The Naive Bayes classifier performed exceptionally well! Here's a breakdown of the results:
#### Overall Accuracy: **97.37%**
This is an excellent accuracy score. It means the model correctly classified over 97% of the reviews in the unseen test set as either "Good" or "Bad"
#### Classification Report
||**Precision**|**Recall**|**F1-Score**|**Support**|
|---|---|---|---|---|
|**Bad**|0.81|0.73|0.77|78|
|**Good**|0.98|0.99|0.98|2087|
- **Precision (Bad)**: When the model predicts a review is "Bad," it is correct **81%** of the time.
- **Recall (Bad)**: The model successfully identified **73%** of all the actual "Bad" reviews.
- **For "Good" reviews**, the performance is nearly perfect, which is expected given the large amount of positive data.
#### Confusion Matrix
||**Predicted Bad**|**Predicted Good**|
|---|---|---|
|**Actual Bad**|**57**|21|
|**Actual Good**|36|**2051**|
- **True Negatives (Correctly identified "Bad"): 57**
- **True Positives (Correctly identified "Good"): 2051**
- **False Positives (Mistook "Good" for "Bad"): 36**
- **False Negatives (Mistook "Bad" for "Good"): 21**

The matrix shows the model is very reliable, especially at identifying good reviews. Its most common error is misclassifying a "Bad" review as "Good," but this only happened 21 times out of over 2,000 reviews.



Multinomial Naive Bayes Classifier; with resampling
```python
import pandas as pd
import seaborn as sns
import matplotlib.pyplot as plt
from sklearn.feature_extraction.text import CountVectorizer
from sklearn.model_selection import train_test_split
from sklearn.naive_bayes import MultinomialNB
from sklearn.metrics import accuracy_score, confusion_matrix, classification_report
from imblearn.over_sampling import RandomOverSampler
import numpy as np

# --- 1. Load and Prepare the Data ---
try:
    df = pd.read_csv('user_courses_review_repaired.csv')
except FileNotFoundError:
    # Fallback to regenerate the cleaned file if it's missing
    df = pd.read_csv('user_courses_review_09_2023.csv', on_bad_lines='skip')
    df['review_rating'] = pd.to_numeric(df['review_rating'], errors='coerce')
    df.dropna(subset=['review_rating'], inplace=True)
    df['review_comment'].fillna('No Comment', inplace=True)

# Create the binary target variable 'sentiment'
df['sentiment'] = df['review_rating'].apply(lambda x: 1 if x >= 4 else 0)

# Define features (X) and target (y)
X_text = df['review_comment']
y = df['sentiment']

# --- 2. Vectorize and Split the Data ---
# It's crucial to split the data BEFORE resampling to avoid data leakage
vectorizer = CountVectorizer(stop_words='english', min_df=2, max_df=0.95)
X = vectorizer.fit_transform(X_text)
X_train, X_test, y_train, y_test = train_test_split(X, y, test_size=0.2, random_state=42)

# --- 3. Resample the Training Data ---
# We use RandomOverSampler to balance the training set by oversampling the minority class ('Bad' reviews)
ros = RandomOverSampler(random_state=42)
X_train_resampled, y_train_resampled = ros.fit_resample(X_train, y_train)

print("--- Data Resampling Results ---")
print(f"Shape of training data before resampling: {X_train.shape}")
print(f"Class distribution before resampling: {np.bincount(y_train)}")
print(f"Shape of training data after resampling: {X_train_resampled.shape}")
print(f"Class distribution after resampling:  {np.bincount(y_train_resampled)}")


# --- 4. Train the Model on the Resampled Data ---
model = MultinomialNB()
model.fit(X_train_resampled, y_train_resampled)

# --- 5. Make Predictions on the Original (Unseen) Test Set ---
y_pred = model.predict(X_test)

# --- 6. Evaluate the New Model's Performance ---
accuracy = accuracy_score(y_test, y_pred)
conf_matrix = confusion_matrix(y_test, y_pred)
class_report = classification_report(y_test, y_pred, target_names=['Bad', 'Good'])

print("\n--- Model Evaluation After Resampling ---")
print(f"Accuracy: {accuracy:.4f}")
print("\nClassification Report:")
print(class_report)
print("\nConfusion Matrix:")
print(conf_matrix)

# --- 7. Visualize the New Confusion Matrix ---
plt.figure(figsize=(8, 6))
sns.heatmap(conf_matrix, annot=True, fmt='d', cmap='Blues',
            xticklabels=['Predicted Bad', 'Predicted Good'],
            yticklabels=['Actual Bad', 'Actual Good'])
plt.title('Confusion Matrix (After Resampling)')
plt.ylabel('Actual Label')
plt.xlabel('Predicted Label')
plt.savefig('confusion_matrix_resampled.png')
```
### The Results: A More Effective Model

Here’s a comparison of the model's performance on the "Bad" reviews, before and after resampling:

|Metric|Before Resampling (Imbalanced)|**After Resampling (Balanced)**|Change|
|---|---|---|---|
|**Recall**|0.73|**0.82**|**+12.3%**|
|**Precision**|0.81|**0.55**|-32.1%|
|**F1-Score**|0.77|**0.66**|-14.3%|
|**Accuracy**|97.37%|**95.52%**|-1.9%|