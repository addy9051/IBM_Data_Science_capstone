# SpaceX Falcon 9 Landing Prediction (IBM Data Science Capstone)

This repository contains my notebooks for the **IBM Data Science Capstone** project: predicting whether the **Falcon 9 first stage** will successfully land (a key driver of launch cost due to booster reuse).

## Repository structure

- `notebooks/`: Jupyter notebooks for data collection, wrangling, EDA/feature engineering, mapping, SQL analysis, and ML modeling.
- `README.md`: this file.

## Notebooks (recommended run order)

All notebooks live in `notebooks/`.

1. `jupyter_labs_spacex_data_collection_api_v2.ipynb`
   - **Goal**: collect SpaceX launch data from the SpaceX REST API and format it into a clean dataset.
   - **Output**: writes `dataset_part_1.csv` (Falcon 9 launches subset).

2. `labs_jupyter_spacex_Data_wrangling_v2.ipynb`
   - **Goal**: wrangle the dataset and create the **label** column (`Class`: 1 = successful landing, 0 = unsuccessful).
   - **Input**: reads `dataset_part_1.csv` (often via the course URL; can be switched to local).
   - **Output**: writes `dataset_part_2.csv`.

3. `jupyter_labs_eda_dataviz_v2.ipynb`
   - **Goal**: EDA + visualization (relationships between success and flight number, payload mass, launch site, orbit, yearly trend), then feature engineering with one-hot encoding.
   - **Input**: reads `dataset_part_2.csv` (often via the course URL; can be switched to local).
   - **Output**: writes `dataset_part_3.csv` (one-hot encoded features for modeling).

4. `lab_jupyter_launch_site_location_v2.ipynb`
   - **Goal**: interactive geospatial analysis with **Folium** (mark launch sites, visualize success/failure clusters, compute distances to nearby features).
   - **Input**: downloads `spacex_launch_geo.csv` (augmented dataset with latitude/longitude).
   - **Output**: interactive maps rendered inside the notebook.

5. `jupyter_labs_eda_sql_coursera_sqllite.ipynb`
   - **Goal**: load SpaceX dataset into **SQLite** and answer SQL questions (distinct launch sites, payload stats, landing outcomes, time filtering, ranking outcomes, etc.).
   - **Input**: reads `Spacex.csv` (course URL) and loads into SQLite.
   - **Output**: creates a local SQLite DB file `my_data1.db` (in the notebook working directory).

6. `SpaceX_Machine_Learning_Prediction_Part_5_v1.ipynb`
   - **Goal**: build and tune classification models (Logistic Regression, SVM, Decision Tree, KNN) using train/test split and hyperparameter search; evaluate using accuracy/confusion matrix.
   - **Input**: reads `dataset_part_3.csv` (often via the course URL; can be switched to local).
   - **Output**: trained models in-memory + evaluation metrics/plots in the notebook.

7. `jupyter_labs_webscraping.ipynb` (optional / alternative data source)
   - **Goal**: scrape Falcon 9 launch records from Wikipedia using BeautifulSoup and build a dataframe.
   - **Output**: writes `spacex_web_scraped.csv`.

## Setup

### Requirements (typical)

- Python 3.9+ (3.10/3.11 recommended)
- Common packages used across notebooks:
  - `pandas`, `numpy`
  - `requests`, `beautifulsoup4`
  - `matplotlib`, `seaborn`
  - `scikit-learn`
  - `folium` (maps)
  - `ipython-sql`, `sqlalchemy`, `prettytable` (SQL notebook)

### Install (pip)

From the repo root:

```bash
python -m venv .venv
.\.venv\Scripts\activate
python -m pip install --upgrade pip
python -m pip install pandas numpy requests beautifulsoup4 matplotlib seaborn scikit-learn folium ipython-sql sqlalchemy prettytable
```

## Running the notebooks

1. Start Jupyter (or open in VS Code / Cursor):

```bash
python -m pip install jupyter
jupyter lab
```

2. Open notebooks under `notebooks/` and run them in the order listed above.

## Notes on datasets / reproducibility

- Several notebooks currently read datasets from the IBM Skills Network course URLs (for consistency with the assignment environment).
- If you want everything to run **fully locally**, use the CSVs produced by earlier notebooks:
  - Run the API collection notebook to create `dataset_part_1.csv`
  - Run wrangling to create `dataset_part_2.csv`
  - Run EDA/feature engineering to create `dataset_part_3.csv`
  - Then update `pd.read_csv("https://...")` lines to `pd.read_csv("dataset_part_X.csv")` as needed.

