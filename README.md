# CDO_tvmaze_data_engineering_assignment
**Overview**

This repository contains a full end-to-end Data Engineering pipeline for TVMaze data using Databricks, PySpark, Delta Lake, and CI/CD workflows.
“The final code is in the feature/data_assignment branch.”
The project covers:

Bronze Layer – raw data ingestion from TVMaze API into Delta Lake.
Silver Layer – data transformations, JSON flattening, and fact table creation.
Gold Layer – aggregated tables for analytics (episodes per season, top cast, etc.).
Data Quality & Testing – unit tests using PySpark and Pytest.
CI/CD & DevOps – GitHub Actions pipeline for deployment, unit tests.
Databricks Asset Bundles (DAB) – parameterized deployment of notebooks, jobs, and clusters.

**Repository Structure**
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

**Setup Instructions**
git clone https://github.com/dsp465/CDO_tvmaze_data_engineering_assignment.git
cd CDO_tvmaze_data_engineering_assignment

Environment Configuration (dev / acc / prod)
Environment‑specific YAML files are stored under:
bundle/configs/
    dev.yaml
    acc.yaml
    prod.yaml
Each file defines:Unity Catalog catalog,schema,Volume paths (instead of ADLS),Serverless compute.

**Bronze Layer: API Raw Data Ingestion**
Ingests raw TVMaze API data into Unity Catalog Volumes and create Bronze Delta tables.
Fetches shows, episodes, and cast from TVMaze API.
Writes raw JSON to: /Volumes/tvmaze/bronze/raw/ --> /Volumes/tvmaze/bronze/raw/shows/ ,similarly for episodes and cast.
Bronze Delta Tables Created : tvmaze.bronze.tv_shows,tvmaze.bronze.episodes and tvmaze.bronze.cast.

**Silver Layer: Transformations and Fact table creation**
Clean, flatten, and standardize Bronze JSON into analytics‑ready tables.
Silver Delta tables created: tvmaze.silver.silver_shows,tvmaze.silver.silver_episodes,tvmaze.silver.silver_cast.
Fact table loaded: tvmaze.silver.fact_show_data.
Performance Techniques Used : Partitioning by show_id,Broadcast joins for small tables(cast) , OPTIMIZE and ZORDER (genre, season).
Demonstrated Before/after runtime comparison.

**Gold Layer: Aggregations & Metrics**
Generate business‑level aggregated metrics.
Gold table loaded: tvmaze.gold.gold_metrics

**Data Quality & Unit Tests**
Tests Required fields being NOT NULL,Runtime values not less than zero and Unique show names per id.
Failed test scenarios screenshots file added.

**ADF**
Since Azure subscription was not available,added json definition for pipeline flow.
Visual representation file added.
Execution logs screenshots file added.

**SQL scripts**
Performing joins and aggregations,
applying window functions
comparing pre and post‑optimization performance

**CI/CD**
Pipeline definition file added along with branching strategy and notbook deployment plan.

**Bundles**
Parameterized bundle for notebooks, jobs, clusters, and configs.
Please note, actual deployment is not being performed,but these commands show how it would work.
Validate: databricks bundle validate -t dev
Deploy: databricks bundle deploy -t dev
Run the workflow job: databricks bundle run tvmaze_job -t dev

These steps would be repeated for ACC and PROD using: -t acc , -t prod

**Deliverables**
Databricks notebooks (Bronze, Silver, Gold)
Spark Catalog Delta tables
Gold metrics queries
Pytest unit tests
GitHub Actions pipeline YAML
Databricks Asset Bundle (bundle.yaml + env configs)
Documentation & workflow explanation
