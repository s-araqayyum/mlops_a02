
# Data Pipeline with Apache Airflow, DVC, and GitHub Integration 🔄

## Project Overview 🎯

This project aims to demonstrate a robust ETL (Extract, Transform, Load) pipeline that uses Apache Airflow for orchestration, Data Version Control (DVC) for data versioning, and GitHub for source control. The goal is to automatically extract news data, ensure its quality, save it in a structured format, and track all changes over time.

## Workflow Description 📋

### 1. Extraction 📥

- **Objective**: Extract news data including titles, descriptions, and URLs from [Dawn](https://www.dawn.com/) and [BBC](https://www.bbc.com/).
- **Method**:
  - Use Python `requests` to fetch webpage content.
  - Parse HTML content with `BeautifulSoup` to extract necessary details.
  - Handle absolute and relative URLs to ensure consistency.
- **Challenges**:
  - Dealing with relative URLs and converting them to absolute.
  - Filtering out non-article links such as advertisements, ensuring only relevant news data is collected.
- **Details**:
  - The extraction function dynamically adjusts URLs, ensuring that only well-formed links are processed. This helps in mitigating issues with broken or relative links that could lead to data quality problems.

### 2. Transformation 🔄

- **Objective**: Filter out articles where either the title or description is missing to maintain data quality.
- **Method**:
  - Check each extracted record for the presence of both title and description.
  - Skip adding records to the dataset if any key information is missing.

### 3. Loading 📤

- **Objective**: Save the cleaned and verified data into a CSV file, with the headers ID, Title, Description, Endpoint.
- **Method**:
  - Use Python's CSV library to write the data into `output.csv`.
  - Ensure the directory for storing the file exists.

### 4. Data Version Control with DVC 🗄️

- **Objective**: Implement version control for datasets to track changes and enhance reproducibility.
- **Method**:
  - Initialize DVC in the project directory.
  - Set a remote storage for DVC to track dataset versions.
  - Push data changes to the DVC remote storage, through tasks detailed in mlops_dag.py
- **Challenges**:
  - Configuring DVC with remote storage solutions like Google Drive and managing access securely. Usage of Google Cloud Console was pertinent.
- **Commands**:
  ```bash
  dvc init
  dvc remote add -d storage gdrive://10UGSeJ00RG8QpcKUluRRBmAUyu08gPJ2
  dvc push
  ```
  - After the initial local DVC push, secondary credentials are stored, allowing the code to seamlessly execute the workflow itself.

### 5. Code Version Control with GitHub 📝

- **Objective**: Manage and version control the project's codebase.
- **Method**:
  - Use git commands to add, commit, and push changes to a GitHub repository.
  - Automate these commands within Airflow tasks to keep the repository up-to-date.
- **Challenges**:
  - Automating git operations within Airflow tasks without manual intervention.
- **Commands**:
  ```bash
  git add .
  git commit -m 'Add DVC Files'
  git push -u origin main
  ```

## Automation and Orchestration 🤖

- **Complete Automation**: The entire ETL process, from data extraction to pushing updates to remote repositories, is automated using Apache Airflow.
- **Scheduled Runs**: Apache Airflow manages the scheduling and monitoring of the ETL workflow, ensuring that the data pipeline runs smoothly without manual oversight.

## Conclusion 🛠️
The integration of Apache Airflow, DVC, and GitHub provides a robust framework for managing data pipelines. It ensures that data extraction, transformation, and loading processes are efficient, reliable, and transparent. This project highlights the importance of data quality, automation, and version control in modern data engineering practices.



The integration of Apache Airflow, DVC, and GitHub provides a robust framework for managing data pipelines. It ensures that data extraction, transformation, and loading processes are efficient, reliable, and transparent. This project highlights the importance of data quality, automation, and version control in modern data engineering practices.
