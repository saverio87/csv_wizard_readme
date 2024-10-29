# fastapi_csv_wizard

# API Documentation

## Overview
This API allows users to upload CSV files and perform various operations such as previewing, splitting, counting duplicates, and removing null entries. Each operation returns a response with relevant information about the processed data.

## Base URL

https://fastapi-csv-wizard.onrender.com/

## Endpoints

### 1. Upload Test File
**POST** `/test-upload/`

#### Description
Receives an uploaded file and prints its details.

#### Request
- **Body**: 
  - `file`: The file to upload (required).

#### Response
- **200 OK**: 
  ```json
  {
      "message": "File received successfully!"
  }

### 2. Preview CSV
**POST** `/preview-csv/`

#### Description
Reads the first specified number of rows from a large CSV file and writes them to a new CSV.

#### Request
- **Body**: 
  - `file`: The CSV file to upload (required).
  - `preview_rows`: The number of rows to preview (required).

#### Response
- **200 OK**: 
  ```json
  {
      "message": "Preview of file available for download.",
      "download_url": "path/to/preview.csv"
  }

### 3. Split CSV
**POST** `/split-csv/`

#### Description
Splits a CSV file based on specified criteria.

#### Request
- **Body**: 
  - `file`: The CSV file to upload (required).
  - `split_type`: The type of split (required).
  - `number`: The number of files to create (required).

#### Response
- **200 OK**: 
  ```json
  {
      "message": "File processed and available for download.",
      "deletion": "The file will be stored for a maximum of 2 minutes.",
      "download_url": "path/to/archive.zip"
  }

### 4. Count Duplicates
**POST** `/count-duplicates/`

#### Description
Counts the number of duplicate entries in specified columns of a CSV file.

#### Request
- **Body**:
  - `file`: The CSV file to upload (required).
  - `columns`: A list of columns to check for duplicates (required).

#### Response
- **200 OK**:
  ```json
  {
      "message": "Number of duplicates found for the columns selected:",
      "info": {
          "column_name": {
              "duplicates": 10,
              "no_duplicates": 90
          }
      }
  }

### 5. Count Duplicates for All Columns
**POST** `/count-duplicates-all/`

#### Description
Counts the number of duplicate entries for all columns in a CSV file.

#### Request
- **Body**:
  - `file`: The CSV file to upload (required).

#### Response
- **200 OK**:
  ```json
  {
      "message": "Number of duplicates found for the columns selected:",
      "info": {
          "column_name": {
              "duplicates": 10,
              "no_duplicates": 90
          }
      }
  }

### 6. Remove Duplicates
**POST** `/remove-duplicates/`

#### Description
Removes duplicate entries based on a specified column in a CSV file and returns the cleaned file.

#### Request
- **Body**:
  - `file`: The CSV file to upload (required).
  - `column`: The column to check for duplicates (required).

#### Response
- **200 OK**:
  ```json
  {
      "message": "Duplicates removed based on column {column_name}",
      "info": {
          "original_row_count": 100,
          "new_row_count": 90,
          "rows_dropped": 10
      },
      "deletion": "The file will be stored for a maximum of 2 minutes.",
      "file_path": "path/to/processed/file.csv"
  }

### 7. Count Nulls
**POST** `/count-nulls/`

#### Description
Counts the number of null entries in specified columns of a CSV file.

#### Request
- **Body**:
  - `file`: The CSV file to upload (required).
  - `columns`: A list of columns to check for nulls (required).

#### Response
- **200 OK**:
  ```json
  {
      "message": "Number of null entries found for the columns selected:",
      "info": {
          "column_name": {
              "nulls": 5,
              "no_nulls": 95
          }
      }
  }

### 8. Count Nulls in All Columns
**POST** `/count-nulls-all/`

#### Description
Counts the number of null entries in all columns of a CSV file.

#### Request
- **Body**:
  - `file`: The CSV file to upload (required).

#### Response
- **200 OK**:
  ```json
  {
      "message": "Number of null entries found for the columns selected:",
      "info": {
          "column_name": {
              "nulls": 3,
              "no_nulls": 97
          },
          "another_column": {
              "nulls": 0,
              "no_nulls": 100
          }
      }
  }

### 9. Remove Nulls
**POST** `/remove-nulls/`

#### Description
Removes rows with null entries in a specified column from a CSV file.

#### Request
- **Body**:
  - `file`: The CSV file to upload (required).
  - `column`: The name of the column to check for nulls (required).

#### Response
- **200 OK**:
  ```json
  {
      "message": "Null entries removed based on column column_name",
      "info": {
          "original_row_count": 100,
          "new_row_count": 97,
          "rows_dropped": 3
      },
      "deletion": "The file will be stored for a maximum of 2 minutes.",
      "file_path": "path/to/processed_file.csv"
  }

### 10. Remove Duplicates
**POST** `/remove-duplicates/`

#### Description
Removes duplicate entries based on a specified column from a CSV file.

#### Request
- **Body**:
  - `file`: The CSV file to upload (required).
  - `column`: The name of the column to check for duplicates (required).

#### Response
- **200 OK**:
  ```json
  {
      "message": "Duplicates removed based on column column_name",
      "info": {
          "original_row_count": 100,
          "new_row_count": 95,
          "duplicates_removed": 5
      },
      "deletion": "The file will be stored for a maximum of 2 minutes.",
      "file_path": "path/to/processed_file.csv"
  }

### 11. Drop Unwanted Columns
**POST** `/drop-columns/`

#### Description
Removes specified unwanted columns from a CSV file.

#### Request
- **Body**:
  - `file`: The CSV file to upload (required).
  - `columns`: A list of column names to be removed (required).

#### Response
- **200 OK**:
  ```json
  {
      "message": "Unwanted columns removed",
      "info": {
          "original_columns": ["column1", "column2", "column3"],
          "remaining_columns": ["column1", "column3"],
          "columns_dropped": ["column2"]
      },
      "deletion": "The file will be stored for a maximum of 2 minutes.",
      "file_path": "path/to/processed_file.csv"
  }
