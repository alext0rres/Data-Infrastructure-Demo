AbbVie Data Engineering Demo

Overview: 
This project demonstrates an end-to-end data engineering pipeline designed to model complex pharmaceutical data using a graph-based approach.
It was built specifically in the context of AbbVie’s efforts to modernize data infrastructure and explore advanced data modeling techniques.

The pipeline ingests and transforms public FDA datasets into a graph-ready format, enabling intuitive traversal across interconnected entities such as drug products, ingredients, manufacturers, adverse events, and reports.

Data Sources:
NDC (National Drug Code) – openFDA
Contains structured metadata on drug products, including product names, active ingredients, manufacturers, and identifiers.

FAERS (FDA Adverse Event Reporting System) – openFDA
A semi-structured dataset of real-world adverse event reports linking drugs to reported outcomes.

These datasets were selected due to their highly relational nature, making them well-suited for graph modeling.

Architecture
Raw JSON (openFDA)
        ↓
Databricks (ETL + normalization)
        ↓
Graph-ready node & relationship tables
        ↓
Neo4j (graph modeling & traversal)

Key Steps:
1. Ingest and flatten nested JSON data (FAERS)
2. Normalize core entities (products, ingredients, manufacturers, events)
3. Create bridge tables to model many-to-many relationships
4. Generate graph-ready node and relationship datasets
5. Load into Neo4j for graph-based exploration

Graph Data Model:

Nodes:
- DrugProduct
- Ingredient
- Manufacturer
- Report
- AdverseEvent

Relationships:
- HAS_INGREDIENT → DrugProduct → Ingredient
- MANUFACTURED_BY → DrugProduct → Manufacturer
- MENTIONS_PRODUCT → Report → DrugProduct
- HAS_ADVERSE_EVENT → Report → AdverseEvent

This structure enables efficient multi-hop traversal across pharmaceutical entities.

Why Graph?:

Pharmaceutical data is inherently interconnected, with many-to-many relationships across products, ingredients, manufacturers, and outcomes. A graph model allows:
- Natural representation of complex relationships
- Efficient multi-hop traversal across entities
- More intuitive exploratory analysis compared to relational joins
- Example Analyses

Some example queries enabled by this model:
- Identify ingredients associated with the widest spread of adverse events
- Analyze manufacturer-level product and ingredient footprints
- Explore product-centered neighborhoods across ingredients, reports, and outcomes

Repository Contents
- notebooks/     → Databricks notebooks (.ipynb)
- datasets/          → Sample datasets (truncated for size)
- exports/       → Neo4j-ready CSVs (nodes & relationships)
- images/        → Graph schema and example outputs
- Demo Video

A short demo walkthrough of the pipeline and graph exploration can be viewed here:
[https://drive.google.com/file/d/1ZdUI-0dRA3F_Eyc7ihH16ChcfvExKJmU/view?usp=sharing]

Data can be sourced from openFDA:
[https://open.fda.gov/data/downloads/]

This project was built as a targeted demonstration of applying data engineering and graph modeling techniques to pharmaceutical data. 
It reflects a strong interest in the intersection of healthcare and modern data infrastructure, and was designed specifically with AbbVie’s technical direction in mind.

If helpful, I would be happy to walk through the project in more detail or provide a live demo.
