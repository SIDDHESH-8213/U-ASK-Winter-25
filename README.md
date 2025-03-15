# U-ASK: Unified Indexing and Query Processing for kNN Spatial-Keyword Queries

This repository contains an implementation of **U-ASK**, a technique for **kNN spatial-keyword queries with negative keyword predicates**. The project is based on the **ACM SIGSPATIAL 2022** paper and includes indexing strategies, batch query processing, and performance evaluation.

## Features
- **Spatial Indexing:** Uses R-tree for efficient spatial queries.
- **Keyword-Based Filtering:** Implements keyword matching with negative keyword predicates.
- **Batch Query Processing:** Allows processing multiple queries efficiently.
- **Performance Evaluation:** Compares against state-of-the-art algorithms.

##  Installation

### Prerequisites
Ensure you have **Python 3.8+** installed.

### Install Dependencies
Clone this repository and install the required Python libraries using:

```bash
git clone https://github.com/yourusername/U-ASK.git
cd U-ASK
pip install -r requirements.txt
```

If running in **Google Colab**, install dependencies using:

```bash
pip install rtree pandas numpy
```

### Required Libraries
This project requires the following libraries:
- `numpy`
- `pandas`
- `rtree`
- `collections`
- `math`
- `os`

## Dataset Preparation

This project expects a dataset with spatial objects stored in `.txt` format. Each line should follow the format:

```
object_id latitude longitude keyword_count keyword_1 weight_1 keyword_2 weight_2 ...
```

To use your dataset:
1. Place the dataset files inside a directory (e.g., `dataset/`).
2. Modify the dataset path inside the Jupyter Notebook (`U_ASK.ipynb`).
3. Run the `load_data_from_folder(folder_path)` function.

## Running the Experiments

### 1. Load Data
Modify the dataset folder path in the notebook and run:

```python
dataset_folder = "dataset/"
dataset = load_data_from_folder(dataset_folder)
```

### 2. Build R-Tree Index
Create an R-tree index for spatial data:

```python
from rtree import index

idx = index.Index()
for obj in dataset:
    idx.insert(obj[0], (obj[1], obj[2], obj[1], obj[2]))
```

### 3. Execute kNN Queries
Run kNN spatial queries:

```python
def knn_query(lat, lon, k):
    nearest = list(idx.nearest((lat, lon, lat, lon), k))
    return nearest

# Example query
results = knn_query(34.0522, -118.2437, 5)
print(results)
```

### 4. Batch Processing for Performance Evaluation
Run multiple queries and evaluate performance:

```python
query_results = []
for q in queries:
    result = knn_query(q[0], q[1], q[2])
    query_results.append(result)
```
