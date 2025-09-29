# llms-evaluation-msbi
A Microsoft Business Intelligence (MSBI) solution for evaluating and benchmarking Large Language Models (LLMs) using real-world benchmark data. This project implements a complete BI pipeline with SSIS (ETL), SSAS (OLAP Cube), and Power BI visualizations to centralize, structure, and analyze the performance of open-source LLMs.

## Table of Contents
1. [Project Overview](#project-overview)
2. [Authors & Organization](#authors--organization)
3. [Motivation & Problem Statement](#motivation--problem-statement)
4. [Objectives](#objectives)
5. [Tech Stack](#tech-stack)
6. [Architecture & Components](#architecture--components)
7. [Data Warehouse Modeling & Granularity Matrix](#data-warehouse-modeling--granularity-matrix)
8. [ETL Process (SSIS)](#etl-process-ssis)
9. [OLAP Cube (SSAS)](#olap-cube-ssas)
10. [Power BI Reports & KPIs](#power-bi-reports--kpis)
11. [Video](#Video)

## 1. Project Overview
The project addresses the challenge of evaluating and benchmarking Large Language Models (LLMs) by centralizing, structuring, and analyzing their performance data. Evaluation results are currently scattered across CSV files, model cards, and scientific articles, making comparison and analysis difficult. The solution involves building a dedicated Data Warehouse, automating ETL processes, and enabling multidimensional analysis and visualization using Microsoft BI tools (SSIS, SSAS, Power BI). The project enables standardized, reproducible, and dynamic analysis of LLM performance across various benchmarks and dimensions.

## 2. Authors & Organization
This project was realized by Rachid Benyakhlef and Amine Ez-zahrouy, under the supervision of Mme. Benhiba, as part of a school project at ENSIAS (National School of Computer Science and Systems Analysis).

## 3. Motivation & Problem Statement
The rapid development and diversity of LLMs have made their evaluation increasingly complex. Results are often dispersed and lack standardization, leading to difficulties in comparison, traceability, and reproducibility. This project addresses these challenges by providing a structured and centralized approach for analyzing LLM performance, enabling reliable and efficient benchmarking for researchers and analysts.

## 4. Objectives
The main objectives of this project are:
- Consolidate and structure LLM evaluation results in a dedicated Data Warehouse.
- Enable comparative and multidimensional analysis of model performance across various axes (benchmark, generation, evaluation type, size, etc.).
- Automate the extraction, transformation, and loading (ETL) of raw data into the Data Warehouse.
- Ensure traceability, standardization, and reproducibility of analyses.
- Facilitate data exploration and retrieval through the implementation of analytical cubes and dynamic visualizations.

## 5. Tech Stack
The solution is built on the following technologies:
- Microsoft SQL Server (database and data warehouse)
- SQL Server Integration Services (SSIS) for ETL processes
- SQL Server Analysis Services (SSAS) for OLAP cubes
- Power BI for data visualization and reporting

## 6. Architecture & Components
The architecture consists of several integrated components:
 - Data sources (CSV, Excel) are cleaned and prepared before loading.
 - A staging area in SQL Server stores raw data for initial processing.
 - SSIS handles ETL workflows, extracting, transforming, and loading data into the Data Warehouse.
 - The Data Warehouse uses a star schema with fact and dimension tables for efficient analysis.
 - SSAS builds OLAP cubes from the warehouse, enabling multidimensional queries and aggregations.
 - Power BI connects to the OLAP cubes for dynamic reporting and visualization.
This pipeline ensures data quality, integrity, and supports advanced analytics and decision-making.

## 7. Data Warehouse Modeling & Granularity Matrix

Before implementing the ETL process, a thorough modeling phase was conducted to define the structure and analytical capabilities of the Data Warehouse. This phase involved identifying key facts (measures) and analytical dimensions, which form the foundation for multidimensional analysis.

### Identification of Facts and Dimensions

**Key Measures and KPIs (Facts):**
- **Benchmark Value:** Raw score obtained by a model on a specific benchmark.
- **Benchmark Normalized Score:** Standardized score for cross-benchmark comparison.
- **Model Average Score:** Average performance of a model across all tasks.
- **Metadata Hub Hearts:** Popularity metric (e.g., number of "likes" on Hugging Face).
- **Metadata CO2 Cost:** Estimated environmental cost of model training.
- **Metadata Params Billions:** Model size (number of parameters in billions).

**Analytical Dimensions:**
- **Model (Dim Modele):** Tracks evolution and characteristics of each model (name, generation, type, architecture, etc.).
- **Benchmark (Dim Benchmark):** Analyzes results by evaluation task.
- **Date (Dim Date):** Enables temporal analysis (submission, publication dates, etc.).
- **Technical Characteristics (Dim Caracteristiques):** Explores specific technical attributes (chat template, merged, flagged, provider, etc.).
- **Metadata (Dim Metadonnees):** Contextual information such as license, generation, provider, etc.

These facts and dimensions were used to construct the granularity matrix, which determines the level of detail for each fact table and guides the final star schema design.

### Granularity Matrix Design

The granularity matrix defines the intersection of dimensions and measures, specifying the grain of each fact table. This ensures that analytical queries are both flexible and performant.

- **Fact ResultatsBenchmark:** Detailed results per model, per benchmark, per date, with associated technical characteristics and metadata.
- **Fact ModeleAggregate:** Aggregated measures per model, such as average scores, popularity, and environmental cost.

The star schema and granularity matrix were visualized and documented (see `images/shemaetoile.png` and `images/Matrice_de_granularité.png`).

This modeling phase established a robust foundation for the subsequent ETL implementation and analytical workflows.

## 8. ETL Process (SSIS)
The ETL process is implemented using SSIS to automate data integration and transformation. Key steps include:
- Data cleaning and preparation using Python (pandas) before loading into SQL Server.
- Importing cleaned data into a staging area for initial validation.
- SSIS workflows extract, transform, and load data into dimension and fact tables, ensuring referential integrity.
- Lookup operations link facts to dimensions, and aggregations are performed for summary tables.
- Special handling for slowly changing dimensions (SCD) to track historical changes.
This robust ETL pipeline ensures high data quality, consistency, and supports efficient updates and analysis.

## 9. OLAP Cube (SSAS)
The OLAP cube is built using SSAS and integrates data from the Data Warehouse for advanced multidimensional analysis. The cube includes:
- Dimensions: Model, Benchmark, Date, Characteristics, Metadata
- Measures: Raw benchmark scores, normalized scores, average model scores, popularity (hearts), environmental cost, and model size
This structure enables users to perform cross-dimensional analysis, compare model performance over time, and generate aggregated KPIs for decision-making. The cube supports flexible slicing, dicing, and drill-down operations for in-depth insights.

## 10. Power BI Reports & KPIs
Power BI is used to create interactive dashboards and reports based on data from the SSAS OLAP cube. Key features include:
- Dynamic visualizations for comparing model performance across benchmarks, generations, and other dimensions
- Calculation and display of KPIs such as average scores, normalized scores, popularity, and environmental impact
- Drill-down and filtering capabilities for detailed analysis
These dashboards help users interpret results, identify top-performing models, and support data-driven decision-making.

## 11. Video

