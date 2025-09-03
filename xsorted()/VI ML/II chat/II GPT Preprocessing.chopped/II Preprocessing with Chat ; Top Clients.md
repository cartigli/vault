after previous code and analysis, ask chat what other analysis we could perform
	it suggested RFM ; Recenency Frequency Monetary grouping for Customer Segmentation
		ask chat how to do it with code
		it gave this:

```python
import pandas as pd

# --- RFM Analysis ---

# To ensure Recency is calculated correctly, we'll find the most recent order date
# and add one day to it. This will be our reference point ('snapshot_date').
snapshot_date = sales_data['order_date'].max() + pd.Timedelta(days=1)
print(f"Snapshot date for Recency calculation: {snapshot_date}")

# Calculate RFM metrics for each customer
rfm_data = sales_data.groupby('customer_id').agg({
    'order_date': lambda date: (snapshot_date - date.max()).days, # Recency
    'order_id': 'count', # Frequency
    'revenue': 'sum' # Monetary
})

# Rename the columns for clarity
rfm_data.rename(columns={'order_date': 'Recency',
                         'order_id': 'Frequency',
                         'revenue': 'Monetary'}, inplace=True)

# --- Create RFM Segments ---

# We will now score each customer from 1 to 4 for each metric.
# For Recency, a lower value (fewer days since last purchase) is better.
# For Frequency and Monetary, a higher value is better.
r_labels = range(4, 0, -1) # 4 is best, 1 is worst
f_labels = range(1, 5)    # 4 is best, 1 is worst
m_labels = range(1, 5)    # 4 is best, 1 is worst

# Create the score labels using quintiles (dividing data into 4 groups)
rfm_data['R_Score'] = pd.qcut(rfm_data['Recency'], q=4, labels=r_labels, duplicates='drop').astype(int)
rfm_data['F_Score'] = pd.qcut(rfm_data['Frequency'], q=4, labels=f_labels, duplicates='drop').astype(int)
rfm_data['M_Score'] = pd.qcut(rfm_data['Monetary'], q=4, labels=m_labels, duplicates='drop').astype(int)


# Combine the scores to create a single RFM score
rfm_data['RFM_Score'] = rfm_data['R_Score'].astype(str) + rfm_data['F_Score'].astype(str) + rfm_data['M_Score'].astype(str)

# --- Map Segments to Names ---

# Define segment names based on the combined RFM score
segment_map = {
    r'[3-4][3-4][3-4]': 'Champions',
    r'[3-4][1-2][3-4]': 'Loyal Customers',
    r'[3-4][1-2][1-2]': 'Potential Loyalists',
    r'2[3-4][3-4]': 'Recent Customers',
    r'1[3-4][3-4]': 'Promising',
    r'2[1-2][1-4]': 'Customers Needing Attention',
    r'1[1-2][1-4]': 'At-Risk Customers',
    r'111': 'Lost'
}


rfm_data['Segment'] = rfm_data['RFM_Score'].replace(segment_map, regex=True)


# --- Display Results ---

print("\n--- RFM Analysis Results (Top 5 Customers) ---")
print(rfm_data.head())

print("\n--- Customer Count by Segment ---")
print(rfm_data['Segment'].value_counts())