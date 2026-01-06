## Project Overview
"Training Data Ltd" creates predictive models to determine if students are looking for new jobs. However, the sheer size of the customer dataset has resulted in slow prediction times. This project focuses on cleaning and optimizing a proof-of-concept dataset (`customer_train.csv`) to ensure efficient storage and faster model execution without sacrificing data utility.

## Dataset
The dataset contains anonymized student information and their job-seeking status. Key features include:

* **ID & Location:** `student_id`, `city`, `city_development_index`.
* **Demographics:** `gender`.
* **Education:** `enrolled_university`, `education_level`, `major_discipline`.
* **Experience:** `relevant_experience`, `experience`, `company_size`, `company_type`, `last_new_job`.
* **Target:** `job_change` (1 = looking for a job, 0 = not looking).

## Methodology

### 1. Exploratory Data Analysis (EDA)
* Loaded the dataset using `pandas`.
* Analyzed value counts for object columns to identify nominal, ordinal, and two-factor categories.

### 2. Data Type Optimization
To reduce memory usage and improve efficiency, the pipeline iterates through columns and downcasts data types:
* **Booleans:** Converted `relevant_experience` and `job_change` to `bool`.
* **Integers:** Downcasted `student_id` and `training_hours` to `int32`.
* **Floats:** Downcasted `city_development_index` to `float16`.
* **Ordered Categories:** Converted ordinal data (e.g., `education_level`, `experience`, `company_size`) to ordered `CategoricalDtype` to preserve hierarchy.
* **Nominal Categories:** Converted remaining object columns to standard `category` type.

### 3. Strategic Filtering
After optimization, the dataset was filtered to isolate a specific high-value subset of students:
* **Experience:** Candidates with 10 or more years of experience.
* **Company Size:** Candidates working at companies with at least 1000 employees.

## Results
The final output is a transformed DataFrame `ds_jobs_transformed` that is memory-efficient and strictly contains experienced professionals from large enterprises, ready for high-speed modeling.

## Technologies Used
* **Python**: Core programming language.
* **pandas**: Used for data ingestion (`read_csv`), type conversion (`astype`, `CategoricalDtype`), and filtering.

## Usage
1.  Place `customer_train.csv` in the project root.
2.  Run the Jupyter Notebook.
3.  The notebook will generate the optimized `ds_jobs_transformed` dataframe.
