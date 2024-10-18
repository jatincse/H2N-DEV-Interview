
 XML to JSON Conversion and SQLite Storage Script

--> Overview

This script processes a set of XML files, converts the XML data into JSON format, and stores both the raw XML data and the processed JSON data in a SQLite database. The script handles errors such as malformed XML, missing data, and retries processing files that encounter errors. It logs the results of each file processing attempt into a log file (`process.log`), allowing you to track the status of each XML file.

--> Features
- Convert XML to JSON: Extracts key fields from XML files, processes them into JSON format, and stores them in a folder.
- Store Data in SQLite: Both raw XML content and processed JSON are stored in a SQLite database.
- Retry Mechanism: The script retries processing files up to 3 times if an error occurs.
- Logging: Errors and processing status are logged to `process.log`.

-->Setup

1. Clone or Download the Repository:
   Clone the repository or download the script to your local machine.

2. Ensure Python 3.13 is installed:
   Make sure you have Python 3.13 installed on your system.

3. Install Required Libraries:
   Open a terminal or command prompt, and run the following command to install the necessary libraries:
   ```bash
   pip install sqlite3 logging xml.etree.ElementTree json glob
   ```

4. Prepare the XML Files:
   Place all your XML files in a folder named `xml-files` in the root directory (or modify the `xml_folder_path` variable in the script to point to your XML folder).

5. Run the Script:
   Execute the script using the following command:
   ```bash
   python your_script_name.py
   ```

6. View the Output:
   - Processed JSON files will be stored in the `json-output` folder.
   - Logs will be available in the `process.log` file.
   - The SQLite database `orders.db` will contain both raw XML and processed JSON data.

7. Check SQLite Database:
   You can use "DB Browser for SQLite" or the "SQLite CLI" to open the `orders.db` file and inspect the tables (`raw_data` and `processed_data`).


--> Handling Errors:
- XML Parsing Errors: If an XML file is improperly formatted (such as missing closing tags), the script records the error in process.log and attempts to process it again, with up to 3 retry attempts.
- Missing Data: Certain XML files might have incomplete data (such as missing <Customer> or <Products> elements). In such cases, the issue is logged, and the file is skipped if essential information is absent.
- Retry : The script tries to process each file up to three times in case of an error. If it still fails after the third attempt, the error is logged, and the file is skipped.

--> Challenges:
- Handling multiple orders in a single XML file: Some XML files contain multiple orders. To handle this, I loop through all `<Order>` elements in the XML structure to ensure each order is processed correctly.
- Storing in SQLite: Inserting both raw XML content and processed JSON into the SQLite database required designing a flexible structure that can handle both types of data.

--> Online Resources Used

- ChatGPT: I utilized ChatGPT to enhance the XML parsing process, improve error handling, and implement a retry mechanism for handling failed file processing. Additionally, ChatGPT assisted in optimizing the logging system and integrating the database for more efficient data management and troubleshooting.
- StackOverflow: I consulted StackOverflow to learn the best practices for storing both raw XML text and JSON data in an SQLite database
- Official Python Documentation: I referenced the official documentation for the `xml.etree.ElementTree` library to ensure I was correctly parsing XML elements and handling missing fields gracefully.

