# 11. Automating Tasks and Scripting in Python

Automation is key to **saving time and ensuring consistency** in data workflows.

# Automating Data Cleaning

Data cleaning is repetitive. Instead of manually cleaning CSVs every day, write a **script** to do it for you.

## Example: Cleaning a CSV file

```python
import pandas as pd

def clean_data(file_path):
		df = pd.read_csv(file_path)
		
		# Remove missing values
		df.dropna(inplace=True)
		
		# Standardize column names
		df.columns = df.columns.str.lower().str.replace(" ", "_")
		
		# Convert date column to datetime format
		if "date" in df.column:
				df["date"] = pd.to_datetime(df["date"])
				
		# Save cleaned file
		df.to_csv("cleaned_data.csv", index=False)
		print("Data cleaned and saved!")
		
clean_data("raw_data.csv")
```

Now, every time a new file comes in, run this script and get a cleaned version.

# Batch Processing Multiple Files

If you receive **daily data files**, automating the merging process is **crucial.**

## Example: Merging Multiple CSVs

```python
import os
import pandas as pd

folder_path = "daily_reports"
merged_df = pd.DataFrame()

for file in os.listdir(folder_path):
		if file.endswith(".csv"):
				df = pd.read_csv(os.path.join(folder_path, file))
				merged_df = pd.concat([merged_df, df])
				
# Save the merged file
merged_df.to_csv("merged_data.csv", index=False)
print("All files merged successfully")
```

# Generating Automated Reports

Automate reporting by **summarizing data** and **exporting reports.** 

## Example: Creating a Summary Report

```python
df = pd.read_csv("merged_data.csv")

# Generate summary statistics
summary = df.describe()
# add more if desired

# Save report
summary.to_csv("summary_report.csv")
print("Summary report generated")
```

# Scheduling Scripts to Run Automatically

You can schedule Python scripts using **Task Scheduler (Windows)** or **Cron Jobs (Mac/Linux).**

## Windows: Using Task Scheduler

1. Open **Task Scheduler.**
2. Create a **Basic Task** → Choose when to run (e.g., daily at 9 AM).
3. Select **Start a Program** → Browse and select `python.exe`.
4. Add your script’s path (`C:\path\to\script.py`).
5. Finish setup.

## Mac/Linux: Using Cron Jobs

```
crontab -e  # Open the cron editor
```

Add this line to run the script every day at 9 AM:

```
0 9 * * * /usr/bin/python3 /path/to/script.py
```

# Automating Web Scripting

## Example: Scraping Data from a Website

```python
import requests
from bs4 import BeautifulSoup

url = "https://example.com/data"
response = requests.get(url)
soup = BeautifulSoup(response.txt, "html.parser")

# Extract data
data = soup.finda_all("div", class_="data-point")

# Save data
with open("scraped_data.txt", "w") as file:
		for item in data:
				file.write(item.text + "\n")
				
print("Web scraping completed")
```

# Practice Problems

```python
import os
import pandas as pd
import requests
from bs4 import BeautifulSou
```

## Automate Data Cleaning

Write a script that **removes missing values** and **renames columns** in a CSV.

```python
def clean_data(file_path):
	 df = pd.read_csv(file_path)
	 
	 # Remove missing values
	 df.dropna(inplace=True)
	 
	 # Standardize column names
	 df.columns = df.columns.str.lower().str.replace(" ", "_")
	 
	 # Convert date column to datetime format
	 if "date" in df.columns:
			 df["date"] = pd.to_datetime(df["date"])
	 
	 # Save cleaned file
	 df.to_csv("cleaned_data.csv", index=False)
	 print("✅ Data cleaned and saved!")

# Simulating data cleaning with a sample DataFrame
df_sample = pd.DataFrame({
 "Name": ["Alice", "Bob", None, "David"],
 "Age": [25, 30, 35, None],
 "Date": ["2024-01-01", "2024-02-01", "2024-03-01", "2024-04-01"]
})

df_sample.to_csv("sample_data.csv", index=False)
clean_data("sample_data.csv")

```

## Batch Processing

Create a Python script that **merges all CSV files** in a folder.

```python
folder_path = "daily_reports"
os.makedirs(folder_path, exist_ok=True)

# Creating sample daily CSV files
for i in range(3):
		df_sample.to_csv(os.path.join(folder_path, f"report_{i+1}.csv"), index=False)

		# Merging CSVs in the folder
		merged_df = pd.DataFrame()
		
		for file in os.listdir(folder_path):
				if file.endswith(".csv"):
					  df = pd.read_csv(os.path.join(folder_path, file))
					  merged_df = pd.concat([merged_df, df])

merged_df.to_csv("merged_data.csv", index=False)
print("✅ All files merged successfully!")
```

## Generate a Summary Report

Write a script that **computes summary statistics** and saves them.

```python
summary = merged_df.describe()
summary.to_csv("summary_report.csv")
print("✅ Summary report generated!")
```

## Scrape Data from a Website

```python
url = "https://books.toscrape.com/" # Sample site for scraping book prices
response = requests.get(url)
soup = BeautifulSoup(response.text, "html.parser")

# Extract book titles and prices
books = soup.find_all("article", class_="product_pod")
scraped_data = []

for book in books:
		title = book.h3.a["title"]
		price = book.find("p", class_="price_color").text
	  scraped_data.append([title, price])

# Save scraped data to a CSV file
df_scraped = pd.DataFrame(scraped_data, columns=["Title", "Price"])
df_scraped.to_csv("scraped_books.csv", index=False)
print("✅ Web scraping completed!")
```