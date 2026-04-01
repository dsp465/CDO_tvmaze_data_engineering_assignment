# CDO_tvmaze_data_engineering_assignment
Overview

This repository contains a full end-to-end Data Engineering pipeline for TVMaze data using Databricks, PySpark, Delta Lake, and CI/CD workflows.

The project covers:

Bronze Layer – raw data ingestion from TVMaze API into Delta Lake.
Silver Layer – data transformations, JSON flattening, and fact table creation.
Gold Layer – aggregated tables for analytics (episodes per season, top cast, etc.).
Data Quality & Testing – unit tests using PySpark and Pytest.
CI/CD & DevOps – GitHub Actions pipeline for deployment, unit tests.
Databricks Asset Bundles (DAB) – parameterized deployment of notebooks, jobs, and clusters.

Repository Structure
CDO_tvmaze_data_engineering_assignment/
├─ bronze/
│  ├─ bronze_ingestion.py                       # Bronze notebook (API ingestion → raw JSON → Delta)
├─ silver/
│  ├─ silver_transformation.py                  # Silver notebook (flattening, joins → fact table) 
├─ gold/
│  ├─ gold_aggregation.py                       # Gold notebook (aggregations, metrics)
├─ unit_tests/
│  ├─ data_quality_tests.py                     # Pytest unit tests for data validation
│  ├─ Failure Simulation screenshots.docx       # Evidence of failed test scenarios
├─ adf/
│  ├─ tvmaze_data_load.json                     # ADF pipeline definition
│  ├─ ADF_tvmaze_data_load.pptx                 # ADF documentation
│  └─ Execution_logs_screenshots.docx           # Production execution logs and screenshots
├─ SQL_scripts/
│  ├─ join_aggregartion.sql                     # SQL join and aggregation logic
│  ├─ window_functions.sql                      # SQL windowing operations
│  └─ PRE_Performancetuning_query.sql           # Pre‑optimization SQL
|  └─ POST_Performancetuning_query.sql          # Post‑optimization SQL
├─ bundle/
│  ├─ bundle.yaml                               # Databricks Asset Bundle definition
│  ├─ resources/
│  │  ├─ jobs/                                  # Job definitions for notebooks
│  │  └─ clusters/                              # Cluster definitions
│  ├─ notebooks/                                # Linked notebooks for deployment
│  └─ configs/                                  # Environment configs for deployment
├─ CICD/
│  └─ azure_pipeline.yml                        # CI/CD pipeline definition
|  └─ Deplyment_workflow.md                     # Deployment workflow documentation
|  └─ git_branching_strategy.md                 # Git branching model (feature -> dev -> acc -> main)
└─ README.md                                    # Project documentation

