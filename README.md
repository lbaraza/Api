# Api

# Collecting Job Data Using APIs

## Project Overview
This project focuses on determining the number of job postings currently available for various technologies and locations using a Jobs API.
The goal is to collect and analyze job market data to provide insights into job availability across different regions.

## Objectives

The main objective of this project is to determine the number of job openings for various technologies in the following locations:

-  Los Angeles
-  New York
-  San Francisco
-  Washington DC
-  Seattle
-  Austin
-  Detroit
 

## Data Sources

The project utilizes job listing data from the following APIs:

- https://www.kaggle.com/promptcloud/jobs-on-naukricom

  
## Tools and Libraries
-  Python: The primary programming language used for data collection and analysis.
-  Pandas: Used for data manipulation and analysis.
-  Requests: Used to make HTTP requests to the Jobs API.
-  JSON: Used to parse the API response data.
  
## Data Collection
The data is collected from the Jobs API, which provides information about job postings. The keys in the JSON response include:

- Job Title
- Job Experience Required
- Key Skills
- Role Category
- Location
- Functional Area
- Industry
- Role

## Installation
To run this project, you need to have Python installed along with the following libraries:

-  pip install pandas requests openpyxl
## Usage
Step-by-Step Instructions
1. Create a Python list of all locations for which you need to find the number of job postings:
python
# List of all locations
locations = ["Los Angeles", "New York", "San Francisco", "Washington DC", "Seattle", "Austin", "Detroit"]

2. Write a function to get the number of jobs for the Python technology for a given location:

import requests
import pandas as pd
import json

def get_job_count(location, technology="Python"):
    api_url = "https://api.example.com/jobs"
    params = {
        "location": location,
        "technology": technology,
        "api_key": "YOUR_API_KEY"
    }
    
    response = requests.get(api_url, params=params)
    
    if response.status_code == 200:
        job_data = response.json()
        return len(job_data["jobs"])
    else:
        print("Failed to retrieve data:", response.status_code)
        return 0

    3.Import libraries required to create an Excel spreadsheet:
    import openpyxl
from openpyxl import Workbook

4.Create a workbook and select the active worksheet:


        # Create a new workbook
wb = openpyxl.Workbook()
# Select the active worksheet
ws = wb.active

5.Collect the number of job postings for the given locations using the API and store the results in an Excel file:

# List of all locations
locations = ["Los Angeles", "New York", "San Francisco", "Washington DC", "Seattle", "Austin", "Detroit"]

job_counts = {}

for location in locations:
    job_counts[location] = get_job_count(location)

# Create a DataFrame to store the results
job_counts_df = pd.DataFrame(list(job_counts.items()), columns=["Location", "Job Count"])

# Write the DataFrame to an Excel file
job_counts_df.to_excel("job_counts.xlsx", index=False)

# Create a new workbook and select the active worksheet
wb = openpyxl.Workbook()
ws = wb.active

# Write headers to the worksheet
ws.append(["Location", "Job Count"])

# Write data to the worksheet
for index, row in job_counts_df.iterrows():
    ws.append(row.tolist())

# Save the workbook
wb.save("job_counts.xlsx")

print(job_counts_df)

## Data Processing
The function get_job_count sends a request to the Jobs API with the specified location and technology,then parses the JSON response to count the number of job postings.
The results are stored in a Pandas DataFrame and exported to an Excel file for further analysis.

## Conclusion
This project provides a method to collect and analyze job posting data from an API.
By examining the number of job openings for different technologies across various locations,we can gain valuable insights into job market trends.



   


