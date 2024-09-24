#### Author
- **Name**: Asif Khan
- **Date**: September 2024
- **Module 6 Challenge**

# NASA CME-GST Prediction

## Challenge Description

### Background:

The **NOAA Space Weather Prediction Center** aims to predict **Geomagnetic Storms (GSTs)** that can cause significant disruptions to modern infrastructure such as satellites, GPS systems, and power grids. These storms result from **Coronal Mass Ejections (CMEs)**, which are large bursts of solar plasma emitted by the sun that interact with Earth's magnetic field.

NASA and NOAA monitor space weather and operate satellites to collect data on CMEs and other space weather phenomena. This data helps power grid operators, GPS operators, and other affected systems prepare for the potential impacts of geomagnetic storms.

### Challenge Task:

This project involves the following steps:

#### 1. Set Up NASA API Key

To access data from NASA's various APIs, including the DONKI API used in this project, you will need to generate an API key. Follow these steps to obtain your NASA API key:

  &nbsp;&nbsp;&nbsp;&nbsp;***Visit the NASA API Website***:  
  &nbsp;&nbsp;&nbsp;&nbsp;Navigate to the [NASA API site](https://api.nasa.gov/) and click on the **"Generate API Key"** button.

  &nbsp;&nbsp;&nbsp;&nbsp;***Enter Your Information***:  
  &nbsp;&nbsp;&nbsp;&nbsp; Fill in the required fields, including your name and email address. You can optionally add a short note that you are using the API for educational purposes.

  &nbsp;&nbsp;&nbsp;&nbsp;***Check Your Email for the API Key***:  
  &nbsp;&nbsp;&nbsp;&nbsp;  After submitting the form, check your email inbox (or your spam folder) for an email from NASA. This email will contain your newly generated API key.

  &nbsp;&nbsp;&nbsp;&nbsp;***Store the API Key Securely***:  
  &nbsp;&nbsp;&nbsp;&nbsp;  Once you have your API key, save it securely. You will not be able to retrieve this key again from NASA's website, so ensure it is stored somewhere safe for future use.

  &nbsp;&nbsp;&nbsp;&nbsp;***Add the API Key to Your Project***:  
  &nbsp;&nbsp;&nbsp;&nbsp;  You can store the API key in a secure environment file (`.env`) within your project directory:
   
   
#### 2. Data Collection
   - Use NASA's API to gather data related to both **Geomagnetic Storms (GSTs)** and **Coronal Mass Ejections (CMEs)**. This data spans from 2013 to the present day.
   - Data for GSTs and CMEs will be collected from NASA's **DONKI (Database of Notifications, Knowledge, Information)** API.

#### 2. Data Processing
   - Merge the two datasets (GST and CME) using the unique activity identifiers from each event.
   - Calculate the average time difference between a CME event and the corresponding GST event to understand the time it takes for a CME to cause a geomagnetic storm.

#### 3. Potential Improvements
   - The final processed dataset, which includes time differences between CME and GST events, can be used in future machine learning models to predict the occurrence of GSTs based on CME activity.
   - These models aim to improve the accuracy of forecasting geomagnetic storms, enhancing decision-making for operators of power grids and satellite systems.

### Steps for Data Collection and Merging:

1. **Extract Data from NASA API**:  
   Use Python and the `requests` library to query the NASA API for both **CME** and **GST** events. 
   
2. **Merge Data**:  
   Merge the two datasets on their respective activity IDs using `pandas`. Ensure that each geomagnetic storm is matched with its corresponding CME event.

3. **Calculate Time Differences**:  
   Compute the time difference between CME and GST events using `pandas` date-time functionality. This step will give insight into the average time it takes for a CME to result in a GST.

4. **Export Data**:  
   Save the final dataset to a CSV file, which can be later used for building predictive models.

---

## 3. Author's Environment Details

### Environment Details

- **Python Implementation**: CPython
- **Python Version**: 3.10.14
- **IPython Version**: 8.25.0
- **Compiler**: Clang 14.0.6
- **Operating System**: Darwin
- **Release**: 23.4.0
- **Machine**: arm64
- **Processor**: arm
- **CPU Cores**: 8
- **Architecture**: 64-bit

### Installed Packages
- **requests**: 2.32.2
- **watermark**: 2.5.0
- **IPython**: 8.25.0
- **ipywidgets**: 8.1.5
- **numpy**: 1.26.4
- **json**: 2.0.9
- **xarray**: 2023.6.0
- **pandas**: 2.2.2

### System Information
- **sys**: 3.10.14 (main, May 6 2024, 14:42:37) [Clang 14.0.6]

---
## Challenge Instructions

This Challenge has three parts, and must be completed in order:

• Part 1: Request CME data from the NASA API.

• Part 2: Request GST data from the NASA API.

• Part 3: Merge and Clean the Data for Export.

The starter code includes importing the required dependencies and your API key from your .env file, but you will need to ensure your API key is added to that file.

#### Part 1: Request CME data from the NASA API
1. The base URL is included in the starter code, along with the search string and query dates. Consult the NASA API documentationLinks to an external site. to help you build your query_url using these variables.
If you accidentally delete these variables, they are:

Set the base URL
base_url = "https://api.nasa.gov/DONKI/"

Set the specifier for CMEs:
specifier = "CME"

Search for CMEs between a begin and an end date
startDate = "2013-05-01"
endDate   = "2024-05-01"

2. Make a GET request for the CME URL and store it in a variable named cme_response, then convert the response variable to JSON and store it as a variable named cme_json.
3. Preview the first results in JSON format using json.dumps with the argument indent=4 to format the data.
4. Convert cme_json to a Pandas DataFrame and keep only the activityID, startTime, and linkedEvents columns.
5. The linkedEvents column allows us to identify the corresponding GST. Remove the rows with missing 'linkedEvents', since we won't be able to assign these to GSTs.
6. Note that the linkedEvents column sometimes contains multiple events per row. Write a nested for loop that first iterates over each row in the cme DataFrame (using the index), and then iterates over the values in linkedEvents and adds the elements individually to a list of dictionaries, where each row is one element.
   
Initialize an empty list called expanded_rows to store the expanded rows:
expanded_rows =

Iterate over each index in the DataFrame:

for i in cme.index:
                             # Get the corresponding value from row i in 'activityID'
                             # Get the corresponding value from row i in 'startTime'        
                             # Get the list of dictionaries from row i in 'linkedEvents'
    
    # Iterate over each dictionary in the list
    for item in linkedEvents:
        # Append a new dictionary to the expanded_rows list for each dictionary item and corresponding 'activityID' and 'startTime' value
         
Create a new DataFrame from the expanded row

7. Create a function called extract_activityID_from_dict that takes a dict as input, such as in linkedEvents, and verify below that it works as expected, using one row from linkedEvents as an example. Be sure to use a try-except block to handle errors:
    def extract_activityID_from_dict(input_dict):
        try:

return
        except (ValueError, TypeError) as e:

return 

extract_activityID_from_dict(cme.loc[0,'linkedEvents'])

8. Apply this function to each row in the linkedEvents column (you can use apply() and a lambda function) and create a new column called GST_ActivityID using loc indexer:
9. Remove rows with missing 'GST_ActivityID', since we can't assign them to GSTs.
10. Convert the GST_ActivityID column to string format. Convert startTime to datetime format and rename it startTime_CME.
11. Rename startTime to startTime_CME and activityID to cmeID. Drop linkedEvents.
12. We are only interested in CMEs related to GSTs, so keep only the rows in which the GST_ActivityID column contains 'GST'. Use the method contains() from the str library.

#### Part 2: Request GST data from the NASA API
1. The base URL is included in the starter code, along with the search string and query dates. Consult the NASA API documentationLinks to an external site. to help you build your query_url using these variables.
If you accidentally delete these variables, they are:
Set the base URL
base_url = "https://api.nasa.gov/DONKI/"

Set the specifier for Geomagnetic Storms (GST):
specifier = "GST"

Search for GSTs between a begin and end date
startDate = "2013-05-01"
endDate   = "2024-05-01"

2. Make a GET request for the GST URL and store it in a variable named gst_response, and then convert the response variable to JSON and store it as a variable named gst_json.
3. Preview the first results in JSON format using json.dumps with the argument indent=4 to format the data.
4. Convert gst_json to a Pandas DataFrame and keep only the activityID, startTime, and linkedEvents columns.
5. The linkedEvents column allows us to identify the corresponding CME. Remove the rows with missing 'linkedEvents', since we won't be able to assign them to CMEs.
6. Note that the linkedEvents column sometimes contains multiple events per row. Use the explode() method to spread those events out into individual rows.
7. Apply the previously created extract_activityID_from_dict, as before, to each row in the linkedEvents column (you can use apply() and a lambda function) and create a new column called CME_ActivityID using the loc indexer.
8. Remove the rows with missing 'CME_ActivityID', since we can't assign them to CMEs.
9. Convert the gstID column to string format, then convert startTime to datetime format and rename it startTime_GST.
10. Rename startTime to startTime_GST and drop linkedEvents.
11. We are only interested in GSTs related to CMEs, so keep only the rows in which the CME_ActivityID column contains 'CME'. Use the method contains() from the str library.

#### Part 3: Merge and Clean the Data for Export
Now that you've collected the data for both events, you need to merge the two DataFrames, clean the data, and then export it for future use. Notice that both DataFrames have observations linked to multiple events, i.e., each CME can be linked to multiple GSTs and each GST can be linked to multiple CMEs. Each DataFrame will thus have duplicate observations to account for this type of relationship. In order to merge these DataFrames correctly, we need to merge on all four ID columns (you can verify this by conducting the merge on a small subset).
1. Merge both datasets using gstID and CME_ActivityID for GST, and GST_ActivityID and cmeID for cme.
2. Verify that the new DataFrame has the same number of rows as the cme and gst DataFrames.
3. Compute the time difference between startTime_GST and startTime_CME by creating a new column called timeDiff.
4. Use describe() to compute the mean and median time.
5. Export data to a CSV file without the DataFrame's index.
