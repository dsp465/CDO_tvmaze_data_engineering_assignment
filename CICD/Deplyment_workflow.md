**Part1: Developer Workzone**
Developer creates feature/* branch from main branch.
Develops code and unit tests
Commits changes and pushes feature branch to dev 
Notebooks deployed to Dev Databricks workspace

**Part2: Promote to ACC**
Runs build and release pipeline
ACC environment uses ACC catalog,schema,cluster
ADF pipeline runs end‑to‑end integration tests (Bronze ,Silver and Gold)

**Part3: Promote to PROD**
CD pipeline deploys to Prod workspace
Only approved reviewers can merge into main
