# Podcast Retriever

Podcast Retriever is a Python-based tool designed to aggregate and consolidate podcast data from multiple sources, including the iTunes Search API, RSS feeds and  Podchaser. The tool builds a comprehensive podcast database by fetching data, processing raw JSON responses, and outputting the final dataset as an Excel file.

## Features

- **Legacy Data Collection:** Uses the iTunes Search API to build an initial dataset (legacy data) by iterating over search terms.
- **Raw Data Management:** Saves raw JSON responses in a dedicated folder (`raw_data`) for transparency and troubleshooting.
- **RSS Feed Extraction:** Processes raw data files to extract unique RSS feed URLs.
- **Multi-Source Fetching:** Retrieves podcast metadata from:
  - Podchaser (via GraphQL)
  - RSS Feeds (with email extraction from XML)
- **Data Consolidation:** Combines data from all sources and cleans it by removing entries without valid contact emails.
- **Export to Excel:** Saves the consolidated dataset to an Excel file (`podcasts_data.xlsx`) using `openpyxl`.
- **Automation Ready:** Includes an optional scheduler to automate database updates on a daily basis.
- **Configurable RSS Feeds:** Maintains an updatable list of RSS feed URLs in a separate file (`rss_feed.py`).

## Project Structure

- **`build_dataset.py`**  
  - Uses the iTunes Search API to fetch podcast data.
  - Iterates over search terms (default is a–z) and saves each JSON response to the `raw_data` directory.
  - Processes and returns data as a pandas DataFrame.

- **`extract_raw_data.py`**  
  - Loads all JSON files stored in the `raw_data` folder.
  - Extracts unique RSS feed URLs from the raw data.
  - Prints the extracted RSS URLs for verification.

- **`fetch.py`**  
  - Consolidates podcast data from multiple sources:
    - **Podchaser:** Fetches data via a GraphQL API.
    - **RSS Feeds:** Extracts metadata (including contact emails) using feed parsing.
    - **Legacy Data:** Integrates data built using `build_dataset.py`.
  - Updates the RSS feeds list in `rss_feed.py` with new URLs extracted from raw data.
  - Saves the final, combined dataset to an Excel file.
  - Optionally automates the data build process on a schedule (daily at 03:00 AM).

- **`rss_feed.py`**  
  - Contains a list of default RSS feed URLs used to fetch podcast metadata.
  - This file is updated automatically when new RSS URLs are extracted from raw data.

- **`readme.md`**  
  - This file, containing an overview, setup instructions, and usage details for the project.

## Prerequisites

- Python 3.7 or higher
- It is recommended to use a virtual environment for dependency management.

## Installation

1. **Clone the Repository:**

   ```bash
   git clone https://github.com/HelixCipher/podcast-retriever.git

   cd Podcast-retriever

----------------------------------------------------------------
2. **Set Up a Virtual Environment:**
python -m venv venv
source venv/bin/activate  # On Windows: venv\Scripts\activate
----------------------------------------   
Install Dependencies:

pip install -r requirements.txt
-----------------------------------
3. **Configuration**
Environment Variables

Create a .env file in the project root and add your API credentials. For example:

Production_Client_Token=your_podchaser_api_token

-----------------------------
RSS Feeds

    The rss_feed.py file holds a list of initial RSS feed URLs. You can edit this list manually or let the program update it automatically during the data build process.
----------------------------------------------------------------
## Usage
#### 1. Build the Legacy Dataset

Fetch podcast data using the iTunes Search API:
python build_dataset.py
--------------------------
This script will:

    * Iterate over search terms (default: a–z).
    * Save raw JSON responses in the raw_data directory.
    * Create a dataset using pandas.
----------------
#### 2. Extract RSS Feed URLs

Extract unique RSS feed URLs from the raw data:
python extract_raw_data.py
-------------------------
python extract_raw_data.py

This will load all JSON files in raw_data and print out the extracted RSS URLs.
----------------------------------------------------------------
#### 3. Fetch and Consolidate Data

Run the main fetching script to collect data from all sources and save the consolidated dataset to an Excel file:

python fetch.py

The script will:

    Fetch data from Podchaser, RSS feeds and legacy (iTunes).
    Update the RSS feeds list in rss_feed.py if new feeds are found.
    Save the combined dataset to podcasts_data.xlsx.

Optional: To automate the database build process on a schedule, uncomment the call to automate_database_build() at the bottom of fetch.py.
----------------------------------------------------------------
## Contributing

Contributions, suggestions, and improvements are welcome. Feel free to fork the repository and submit pull requests. Please include detailed explanations for any changes or additions.
------------------
## Contact

For questions, support, or further discussions, please open an issue on GitHub or contact the repository maintainer.
-------------------------
This project is intended to serve as a robust solution for aggregating podcast data, enabling efficient data collection and analysis in the podcasting industry.
