Text Extraction to JSON File
Project Overview
The Text Extraction to JSON File project is a sophisticated Python solution designed to automate the extraction of structured data from unstructured text documents, such as PDFs and HTML files. The core functionality revolves around parsing bid documents, contracts, or similar text-heavy files to extract relevant fields and convert the extracted data into a well-organized, machine-readable JSON format. This ensures that key information, such as bid numbers, titles, deadlines, and contact details, is easily accessible and can be integrated into further data processing or analysis workflows.

Purpose and Scope
The project aims to provide a robust and scalable solution for processing documents in various formats (PDF, HTML) and converting them into a structured, standardized format (JSON). Key fields extracted from these documents can include:

Bid Numbers
Titles
Due Dates
Submission Types
Contact Information
Payment Terms
Product Specifications
By using this solution, users can significantly reduce the manual effort involved in parsing and organizing complex documents. The goal is to create a flexible framework capable of adapting to various document structures and efficiently extracting the necessary fields.

Core Functionalities
1. PDF and HTML Parsing: The project supports both PDF and HTML document formats. It leverages specialized libraries such as PyPDF2, pdfplumber for PDF parsing, and BeautifulSoup for HTML parsing. These libraries enable accurate extraction of text content from different document layouts, including those with tables, images, and embedded text.

2. Data Extraction: Data is extracted using customizable extraction rules defined in the config.py file. The script utilizes regular expressions (regex) to identify specific data patterns within the raw document text. These regex patterns are highly flexible, allowing the extraction logic to be easily adapted to different types of documents and varying formats.

3. Structured JSON Output: Once the necessary fields are extracted, the project outputs the data in a structured JSON format. This format is ideal for further processing, storage, or integration with other systems. Each extracted document results in a JSON object that groups the data under clearly defined keys, such as "Bid Number," "Title," "Due Date," and more.

4. Configurable Field Extraction: The config.py file allows users to define the field names and their associated regex patterns for extraction. This makes it easy to extend the project and adapt it for various document types by simply modifying the configuration.

5. Utility for Data Parsing: The data_parser.py module provides helper functions for cleaning and processing the raw text, ensuring that the extracted data is formatted correctly before being converted to JSON.

6. Testing Suite: The project includes a robust testing suite to ensure that the extraction logic works correctly under a variety of document formats and conditions. The tests/ folder contains unit tests for different scenarios, helping to ensure that edge cases and unexpected document structures are handled appropriately.


text_extraction_jason_file/
├── README.md                # Project overview and technical documentation

├── requirements.txt         # Python dependencies required to run the project

├── extract_data.py          # Main script responsible for extracting data

├── data_parser.py           # Utility functions for parsing raw text

├── config.py                # Configuration for field extraction rules and regex patterns

├── sample_data/             # Folder containing sample input files (PDF, HTML)

├── output/                  # Folder where JSON output is stored

└── tests/                   # Unit tests validating the extraction process

Detailed Breakdown
extract_data.py
The heart of the project, extract_data.py, is responsible for:

Reading input documents (PDF or HTML).
Applying the extraction logic defined in config.py.
Parsing the raw text using regular expressions to identify and capture relevant data points.
Formatting the extracted data into a structured JSON object.
This script uses a well-defined flow:

Input file is loaded and processed (PDF or HTML).
Each data field is matched to its corresponding regex pattern from config.py.
If a match is found, the data is extracted and stored.
The extracted data is then written into a JSON file for later use.
data_parser.py
This module contains functions that:

Handle text preprocessing, such as stripping unwanted characters, normalizing text, and performing basic cleaning tasks.
Ensure the parsed text is in a consistent and clean format before further processing.
Extract specific fields from the raw document text and return them in a usable format (such as strings or integers).
The data_parser.py module also handles any necessary transformations or validations of the extracted data, ensuring consistency in the final output.

config.py
In this file, users define the extraction rules for various fields. For each field, the corresponding regex pattern is specified to match the data in the document. This is a crucial part of the system's flexibility — users can easily modify the regex patterns or add new fields to fit the requirements of different document types.

Project Architecture
The project's architecture is modular, with clear separation between different components responsible for parsing, data extraction, and output formatting.

1. extract_data.py – The Extraction Engine
extract_data.py is the core of the project. It is responsible for:

Loading Input Files: The script can handle both PDF and HTML files, accepting file paths as input arguments. The input file is loaded using libraries such as pdfplumber for PDFs and BeautifulSoup for HTML files.
Text Extraction: Depending on the file type, the appropriate library is invoked to extract text. For PDFs, the library attempts to read both the main content and any embedded tables, while for HTML, it parses the document and extracts text while ignoring non-relevant tags (like <script>, <style>, etc.).
Field Extraction: The extracted raw text is processed using regular expressions defined in config.py to identify key data points (such as Bid Number, Title, Due Date, etc.).
Data Structuring: Once the fields are extracted, the data is stored in a dictionary and converted into a JSON object for easy readability and use.

2. data_parser.py – Text Parsing and Preprocessing
The data_parser.py module ensures that the raw text extracted from the document is cleaned, normalized, and processed before further use. This step is critical as the raw text extracted from documents can often contain formatting artifacts, unwanted characters, and irregular spacing. Key functionalities include:

Text Normalization: Stripping unnecessary whitespace, converting text to a uniform case, and standardizing date and number formats.
Field Parsing: After applying regex patterns, the parsed fields are validated, formatted, and stored in the required structure (e.g., converting a string date into datetime or cleaning product specifications).

3. config.py – Configurable Extraction Rules
config.py serves as the central location for configuring the extraction process. This file contains:

Field Definitions: Each field to be extracted is defined by a regex pattern. For example, a pattern to extract "Bid Number" might be defined as:

FIELD_CONFIG = {
    "Bid Number": r"Bid Number:\s*(\d+)",
    
    "Title": r"Title:\s*(.*?)\n",  # Non-greedy match
    
    "Due Date": r"Due Date:\s*(\d{2}/\d{2}/\d{4})",
    
    "Contact Info": r"Contact:\s*(\S+@\S+\.\S+)",
    
    ...
}

Customization: The regex patterns can be easily modified to accommodate the specific format of different documents. The extraction rules are highly configurable to ensure adaptability across different document structures and data formats.

4. requirements.txt – Dependencies Management
The requirements.txt file lists all Python dependencies necessary to run the project. This includes libraries such as pdfplumber, beautifulsoup4, and pytest. The file ensures that all dependencies are installed at once and allows for easy environment setup.

5. tests/ – Unit Testing
The tests/ directory contains unit tests that validate the correctness of the extraction process. It includes tests for:

PDF Documents: Verifying the extraction of key fields from sample PDFs with varied layouts.
HTML Documents: Testing extraction from HTML documents with complex structures.
Edge Case Scenarios: Ensuring the system can handle missing fields, unusual document structures, and malformed inputs.
Each test case checks that the extraction logic correctly identifies the fields and structures the output as expected.

Key Technical Highlights
Regex-Based Extraction: Regular expressions are used to extract key information, making the system highly adaptable. This allows users to define flexible and custom extraction rules for different types of documents. Whether it's a bid number, due date, or contact info, the regex approach ensures accurate data matching.

Modular and Configurable Design: The system is designed to be modular. The core extraction logic is separated into the extract_data.py script, while customizable extraction patterns are stored in config.py. This makes it easy for users to modify the system according to their needs without having to change the underlying extraction code.

Scalable: The system is designed to be scalable for processing large batches of documents. By using efficient text parsing libraries (PyPDF2 for PDFs and BeautifulSoup for HTML), the extraction process is both fast and scalable.

Error Handling and Robustness: The code handles potential errors gracefully, such as missing data fields or misformatted documents. The system ensures that even if certain fields are not found in the document, the script continues processing without crashing.

Output in JSON Format: The extracted data is returned in JSON format, which is widely used and can be easily integrated into other systems for further processing, storage, or analysis.

Conclusion
The Text Extraction to JSON File project offers a powerful, flexible, and extensible solution for converting unstructured text data from documents into structured JSON formats. With its configurable extraction logic, comprehensive error handling, and modular design, this project is ideal for anyone needing to automate the extraction of key information from complex documents like bid proposals, contracts, and reports.

This project can easily scale to handle large volumes of documents and is customizable enough to support a wide variety of document structures. It provides a reliable foundation for integrating document data extraction into larger automated workflows.
