more instances of one class than another - imbalanced

if we had a dataset of 1000 people, 5 of which had a rare disease, and trained a model to predict who had the disease, accuracy of 99.5% would be achieved when the model did not accurately predict any infected people ; 99.5% is completely misleading

Overcoming Imbalanced Datasets:
	Resampling: mods original dataset to create more balanced distribution
		undersampling: resampling that reduces the majority class
			loss of data is obvious downside
		oversampling: increases minority class through replication
			overfit risk increases due to repeated conditions
		smote:
			generates new synthetic samples in the minority class
				like overfit but tweaks values and data to make new samples
	Weighted Classes: assigns different weights to classes
		makes model more sensitive to minority class
			misclassifying minority instances gets a more severe penalty
	Data Augmentation: like smote, but more generalized
		like for photos, generates slightly altered variations of the image
			like rotating, flipping, zooming

Weighted ML Algorithms:
	ex:
		SVM's {{ Support Vector Machines }} assign different classes different weights
		Decision Trees can adjust their splitting criteria to adjust for imbalance

All these techniques or adjustments aim to resolve issues brought by imbalanced data