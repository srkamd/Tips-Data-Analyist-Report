## Tips for data analyst 
This repositrory contains a Tips data from seaborn library for data analyst purpose.

## 1.  Installation by creating a python virtual envoirnment 
```bash 
# Now Create a virtual envoirment.
python -m venv .venv 
# Now Activate the virtual envoriment 
source .venv/scripts/activate
# Now installing the libraries 
# now create the requirements.txt file and add basic libraries
pip install -r requirements.txt
```
## 2. Create a Jupyter note book in scripts folder

```bash
#create a jupiyter notebook using .ipnyb extension
#or you can manually type this command
mkdir scripts
cd scripts
touch 01_data_analyst.ipynb
```
# 1. Data Composition Report 
## 1. The structure of the dataset (rows and columns)

print("Shape of the dataset:", df.shape) 

## 2. Data types of each column
print("\nData Types:\n", df.dtypes)

## 3. Missing values in each column
print("\nMissing Values:\n", df.isnull().sum())

## Sum of missing values
print("\nTotal Missing Values:\n", df.isnull().sum().sum())

## 4. Unique values in each column
print("\nUnique Values:\n", df.nunique())

## 5. Basic statistics for numerical columns (mean, median, mode, std, min, max, quartiles)
print("\nBasic Statistics:\n", df.describe())

## Median for numerical columns
print("\nMedian for numerical columns:\n", df.median(numeric_only=True))

## Mode for numerical columns
print("\nMode for numerical columns:\n", df.mode(numeric_only=True).iloc[0])

## Categorical variables summary
print("Categorical Variables Summary:")
categorical_cols = df.select_dtypes(include=['object', 'category']).columns
for col in categorical_cols:
   print(f"\n{col}:")
   print(df[col].value_counts())
   print(f"Unique values: {df[col].nunique()}")

# 2. Data Composition Interpretation
The tips dataset contains 244 observations with 7 variables. The dataset is complete with no missing values, which is excellent for analysis. We have 4 numerical variables (total_bill, tip, size) and 3 categorical variables (sex, smoker, day, time). The data represents restaurant tips with key metrics like bill amount, tip amount, party size, and demographic information.

# Data Distribution Report
```bash
# Set up the plotting style
plt.style.use('seaborn-v0_8')
sns.set_palette("husl")

# Create distribution plots for numerical variables
fig, axes = plt.subplots(2, 2, figsize=(15, 12))
fig.suptitle('Distribution of Numerical Variables', fontsize=16, fontweight='bold')

# Total Bill Distribution
axes[0,0].hist(df['total_bill'], bins=20, alpha=0.7, color='skyblue', edgecolor='black')
axes[0,0].axvline(df['total_bill'].mean(), color='red', linestyle='--', label=f'Mean: ${df["total_bill"].mean():.2f}')
axes[0,0].axvline(df['total_bill'].median(), color='green', linestyle='--', label=f'Median: ${df["total_bill"].median():.2f}')
axes[0,0].set_title('Total Bill Distribution')
axes[0,0].set_xlabel('Total Bill ($)')
axes[0,0].set_ylabel('Frequency')
axes[0,0].legend()

# Tip Distribution
axes[0,1].hist(df['tip'], bins=20, alpha=0.7, color='lightcoral', edgecolor='black')
axes[0,1].axvline(df['tip'].mean(), color='red', linestyle='--', label=f'Mean: ${df["tip"].mean():.2f}')
axes[0,1].axvline(df['tip'].median(), color='green', linestyle='--', label=f'Median: ${df["tip"].median():.2f}')
axes[0,1].set_title('Tip Distribution')
axes[0,1].set_xlabel('Tip ($)')
axes[0,1].set_ylabel('Frequency')
axes[0,1].legend()

# Size Distribution
axes[1,0].hist(df['size'], bins=range(1, df['size'].max()+2), alpha=0.7, color='lightgreen', edgecolor='black')
axes[1,0].set_title('Party Size Distribution')
axes[1,0].set_xlabel('Party Size')
axes[1,0].set_ylabel('Frequency')

# Tip Percentage Distribution
df['tip_percentage'] = (df['tip'] / df['total_bill']) * 100
axes[1,1].hist(df['tip_percentage'], bins=20, alpha=0.7, color='gold', edgecolor='black')
axes[1,1].axvline(df['tip_percentage'].mean(), color='red', linestyle='--', label=f'Mean: {df["tip_percentage"].mean():.1f}%')
axes[1,1].axvline(df['tip_percentage'].median(), color='green', linestyle='--', label=f'Median: {df["tip_percentage"].median():.1f}%')
axes[1,1].set_title('Tip Percentage Distribution')
axes[1,1].set_xlabel('Tip Percentage (%)')
axes[1,1].set_ylabel('Frequency')
axes[1,1].legend()

plt.tight_layout()
plt.show()

```


















