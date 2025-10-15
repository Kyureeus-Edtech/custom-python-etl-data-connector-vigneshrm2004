# SonarQube Metrics ETL Project

This project fetches SonarQube metrics for a specific project and stores them in MongoDB using Python. It follows the ETL (Extract, Transform, Load) methodology.

---

## Project Structure

```

A2/
├── n.py                  # Main ETL script
├── .env                  # Environment variables
├── requirements.txt      # Python dependencies
└── README.md             # Project documentation

```

---

## Requirements

- Python 3.10+
- MongoDB running locally or on a remote server
- SonarQube Community Edition running locally (http://localhost:9000)
- SonarScanner installed for project analysis

---

## Usage

### 1. Analyze your project using SonarScanner:

```bash
sonar-scanner ^
  -Dsonar.projectKey=VIGS ^
  -Dsonar.sources=. ^
  -Dsonar.host.url=http://localhost:9000 ^
  -Dsonar.token=sqa_e6b6d99027a85d57c66b6dcf7dd2eca7f0704026
````

### 2. Run the Python ETL script:

```bash
python n.py
```

The script will:

* Fetch metrics from SonarQube API
* Transform the data
* Insert the metrics into the MongoDB collection `sonar_metrics`

---

## Metrics Fetched

* `bugs`
* `code_smells`
* `vulnerabilities`
* `coverage`
* `duplicated_lines_density`

Each record also includes a timestamp.

---

## Output Example

Example document inserted into MongoDB:

```json
{
  "project_key": "VIGS",
  "timestamp": "2025-10-15T09:34:07.882215",
  "coverage": "0.0",
  "bugs": "0",
  "code_smells": "1",
  "duplicated_lines_density": "0.0",
  "vulnerabilities": "0"
}
```

---

## Dependencies

Install dependencies using:

```bash
pip install -r requirements.txt
```

**Example `requirements.txt`:**

```
requests
pymongo
python-dotenv
```

---

## Notes

* Ensure SonarQube server is running before running the ETL script.
* Run `sonar-scanner` on your project first to generate metrics.
* The ETL script stores timestamped metrics for historical tracking.

---

## References

* [SonarQube API Documentation](https://sonarcloud.io/web_api)
* [MongoDB Python Driver (PyMongo)](https://pymongo.readthedocs.io/)

