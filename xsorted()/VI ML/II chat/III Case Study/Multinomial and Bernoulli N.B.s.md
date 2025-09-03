Naive Bayes Algorithm
"My main goal for this analysis is to train a Naive Bayes algorithm which classifies text reviews as good or bad, or ideally can directly classify them in categories from 1 to 5 for their rating."

gem's response & suggestion:
The Plan: From Text to Prediction

**Prepare the Data**
Create a Target Variable: We'll create a new column, let's call it sentiment. It will have a value of 1 for "Good" reviews (ratings 4 & 5) and 0 for "Bad" reviews (ratings 1, 2, & 3).
Define Features (X) and Target (y): Our feature (X) will be the review_comment text, and our target (y) will be the new sentiment column.
		{{ I'm with you so far }}
**Vectorize the Text**
A machine learning model can't understand words, so we need to convert the text comments into numbers. We'll use a technique called Bag-of-Words.
This process converts each comment into a vector that counts the frequency of each word in it. We will use the CountVectorizer from the scikit-learn library to do this.
		{{ Bag of Words is crucial step, and will need to be encoded into our ML Model as well }}
**Split the Data**
We'll split our dataset into two parts: a training set (for the model to learn from) and a testing set (to evaluate its performance on unseen data). This is the most important step to ensure we are building a model that can generalize to new, real-world reviews.
		{{ good we have it }}
**Train the Naive Bayes Model**
We will feed the vectorized text and the corresponding sentiment labels from our training set into a Multinomial Naive Bayes classifier. This specific type of Naive Bayes is the standard for text classification.
		{{ gemini chose a Multinomial Naive Bayes classifier }}
**Evaluate the Model's Performance**
Once the model is trained, we'll use the testing set to see how well it performs. We'll look at:
Accuracy: The overall percentage of correct predictions.
Confusion Matrix: A table that shows us exactly where the model is getting confused (e.g., how many "Bad" reviews it mistakenly classified as "Good").
Classification Report: This will give us more detailed metrics like Precision and Recall, which tell us how reliable the model is at identifying each class.
		{{ good accuracy, confusion matrix, reporting }}
		{{ no fine tuning, or deployment mentioned; also not what I asked it }}

Model's choice of Multinomial:
	most likely correct; Bernoulli does not account, or barely accounts, for frequencies of words, so Multinomial allows us to predict sentiment based off commonly used words for bad reviews