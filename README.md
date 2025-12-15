# 💊 Drug Medication Database Analysis Project

A comprehensive data engineering and analytics project that analyzes pharmaceutical data using Snowflake's Medallion Architecture, AI-powered features, and interactive Streamlit visualizations.

## 👥 Team Members

- Nathan Arimilli
- Humphrey Hui
- Pranit Yadav

## 📋 Project Overview

This project implements an end-to-end data pipeline in snowflake for analyzing drug medication data from a Kaggle dataset containing 11.8K rows and 9 columns. The pipeline processes information about medicines, their compositions, uses, side effects, manufacturers, and customer reviews to provide actionable insights for healthcare decision-making.

## ✨ Key Features

### 🏗️ Medallion Architecture
- **Bronze Layer**: Raw data ingestion from the drug database
- **Silver Layer**: Cleaned and transformed data with standardized formats
- **Gold Layer**: Analytics-ready aggregated tables including:
  - Medicine Performance metrics
  - Manufacturer Performance analytics
  - Ingredient Performance insights

### 🤖 AI-Powered Features
- **AI SQL Columns**:
  - `AI_Recommendation`: Intelligent doctor recommendations based on medication data
  - `AI_Summary`: Concise summaries of medicine information
- **Cortex Search**: Advanced semantic search capabilities for finding relevant medications
- **Cortex Analyst**: Natural language querying of the database

### 📊 Interactive Visualizations
Built with Streamlit, featuring:
1. **Manufacturer Performance Analysis**
   - Quality score rankings
   - Review distribution analysis
   - Top performing manufacturers

2. **Medicine Performance Dashboard**
   - Top-performing medicines by customer satisfaction
   - Ingredient complexity correlation analysis
   - Downloadable CSV reports

3. **Ingredient Popularity & Performance**
   - Most common active ingredients
   - Usage patterns across medicines
   - Quality performance by ingredient

### 🔄 Data Pipeline Features
- **Incremental Load**: Efficient updates with only new data processing
- **Text Cleaning**: Advanced NLP preprocessing for medical text
  - Missing space correction
  - Structured phrase removal
  - Capital letter splitting
  - Fragment cleanup

## 🛠️ Technology Stack

- **Data Warehouse**: Snowflake
- **Programming**: Python, SQL
- **Visualization**: Streamlit
- **AI/ML**: Snowflake Cortex (Search & Analyst)
- **Development**: Jupyter Notebooks
- **Data Source**: Kaggle Drug Dataset

## 📊 Data Schema

### Input Data Columns
1. Medicine Name
2. Composition
3. Uses
4. Side Effects
5. Image URL
6. Manufacturer
7. Excellent Review %
8. Average Review %
9. Poor Review %

### Dimension Tables (Silver Layer)
- `Medicine_Name_Dim`
- `Manufacturer_Dim`
- `Composition`
- `Manufacturer`
- `Reviews`
- `SideEffects`
- `Uses`

### Analytics Tables (Gold Layer)
- `Medicine_Performance`
- `Manufacturer_Performance`
- `Ingredient_Performance`

## 🚀 Getting Started

### Prerequisites
```bash
# Python packages
pip install snowflake-connector-python
pip install streamlit
pip install pandas
pip install jupyter
```

### Snowflake Setup
1. Create a Snowflake account
2. Set up a database and schema
3. Configure warehouse compute resources
4. Enable Cortex features (Search and Analyst)

### Configuration
Update your Snowflake connection parameters:
```python
connection_parameters = {
    "account": "your_account",
    "user": "your_username",
    "password": "your_password",
    "warehouse": "your_warehouse",
    "database": "your_database",
    "schema": "your_schema"
}
```

## 📁 Project Structure
```
drug-medication-analysis/
├── README.md
├── Final_Code_Compilation.ipynb    # Main pipeline code
├── data/
│   └── raw/                        # Raw Kaggle dataset
├── sql/
│   ├── bronze/                     # Bronze layer DDL/DML
│   ├── silver/                     # Silver layer transformations
│   └── gold/                       # Gold layer aggregations
├── streamlit/
│   └── app.py                      # Streamlit dashboard
└── docs/
    └── presentation.pdf            # Project presentation
```

## 💻 Usage

### Running the Pipeline
```python
# Execute the Jupyter notebook
jupyter notebook Final_Code_Compilation.ipynb

# Or run specific stages
python -m pipeline.bronze_load
python -m pipeline.silver_transform
python -m pipeline.gold_aggregate
```

### Launching the Dashboard
```bash
streamlit run streamlit/app.py
```

### Using Cortex Search
```sql
-- Search for bacterial infection medications
SELECT * FROM TABLE(
    SNOWFLAKE.CORTEX.SEARCH_QUERY(
        'DB_TEAM_HNP.BRONZE.BRONZE_SEARCH',
        '{"query": "antibiotics for bacterial infections", "limit": 10}'
    )
) AS result;
```

### Using Cortex Analyst
```sql
-- Natural language query
SELECT * FROM TABLE(
    SNOWFLAKE.CORTEX.COMPLETE(
        'Based on this data, should doctors prescribe this for bacterial infections?',
        'MEDICINE_NAME', 'USES', 'SIDE_EFFECTS', 'EXCELLENT_REVIEW_PERCENTAGE'
    )
) LIMIT 10;
```

## 🔍 Key Insights

1. **Manufacturer Performance**: Tidal Laboratories Pvt Ltd ranks highest with a quality score of 0.712
2. **Most Popular Ingredient**: Metformin appears in 142 medicines
3. **Performance Correlation**: Medicine complexity (number of ingredients) shows interesting patterns with performance ratings
4. **Incremental Load**: System successfully handles new data with minimal processing overhead

## 📈 Future Enhancements

- [ ] Real-time data streaming from pharmacy systems
- [ ] Predictive modeling for drug efficacy
- [ ] Integration with FDA approval databases
- [ ] Mobile app for healthcare providers
- [ ] Enhanced NLP for side effect severity classification
- [ ] Drug interaction warning system

## 🤝 Contributing

Contributions are welcome! Please feel free to submit a Pull Request.

## 🙏 Acknowledgments

- Kaggle for providing the drug dataset
- Snowflake for the powerful data platform and Cortex AI capabilities
- Streamlit for the intuitive visualization framework

## 📞 Contact

For questions or feedback, please reach out to the team members listed above.

---

**Note**: This project was developed as part of an Information Management coursework to demonstrate modern data engineering practices and AI integration in healthcare analytics.
