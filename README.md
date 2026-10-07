# Customer Clustering

An unsupervised machine learning project that groups customers by their age, income and spending patterns.

The project covers data exploration, preprocessing, Principal Component Analysis (PCA) and comparison of clustering methods.

## Repository Files

| File | Description |
| --- | --- |
| [Customer_Clustering.ipynb](Customer_Clustering.ipynb) | Notebook containing the analysis, clustering code and saved results. |
| [Customer_Clustering.pptx](Customer_Clustering.pptx) | Presentation summarising the workflow and customer segments. |
| [Customer-Data.csv](Customer-Data.csv) | Customer dataset used in the project. |

## Dataset

The included dataset contains **200 customers and 5 columns**, with no missing values.

| Column | Description |
| --- | --- |
| `CustomerID` | Customer identifier |
| `Gender` | Customer gender |
| `Age` | Age in years |
| `Income (k$)` | Income in thousands of dollars |
| `How Much They Spend` | Spending score from 1 to 99 |

Two customers with the maximum income value of **$137,000** are removed, leaving **198 customers** for clustering.

## Project Workflow

1. Explore feature distributions and relationships.
2. Remove `CustomerID`.
3. Rename income and spending columns for easier use.
4. Remove the two maximum-income records.
5. Encode gender as `Male = 0` and `Female = 1`.
6. Standardise age, income and spending using `StandardScaler`.
7. Reduce the four inputs to two PCA components.
8. Compare clustering methods.
9. Use the elbow method and silhouette scores to choose the number of clusters.
10. Summarise the selected customer segments.

## Principal Component Analysis

The first two PCA components retain **71.84% of the total variance**.

- **PC1:** Mainly captures the difference between age and spending.
- **PC2:** Mainly captures income.
- Gender contributes little to these two components.

Clustering is performed in this two-dimensional PCA space.

## Models Compared

- K-Means
- Agglomerative Clustering
- DBSCAN
- Gaussian Mixture Model (GMM)

A Ward hierarchical dendrogram is also used to examine the cluster structure.

### Initial Comparison

| Model | Configuration | Silhouette Score |
| --- | --- | ---: |
| K-Means | 3 clusters | 0.4186 |
| Agglomerative Clustering | 3 clusters | 0.3669 |
| DBSCAN | `eps=0.5`, `min_samples=3` | 0.1838 |
| GMM | 3 components | 0.3919 |

### Cluster Count Search

The notebook compares **2 to 6 clusters** for K-Means, Agglomerative Clustering and GMM.

The highest recorded score for each method occurs at **2 clusters**.

| Model | Cluster Count | Recorded Silhouette Score |
| --- | ---: | ---: |
| K-Means | 2 | 0.423 |
| Agglomerative Clustering | 2 | 0.397 |
| GMM | 2 | 0.413 |

These values come from the notebook's saved search outputs. The K-Means search does not fix a random seed, so its scores may vary between runs.

## Selected Customer Segments

The final segmentation uses **K-Means with 2 clusters**, fitted with `random_state=42`.

The table shows standardised means, where positive values are above the dataset average and negative values are below it.

| Cluster | Age | Income | Spending | Profile |
| --- | ---: | ---: | ---: | --- |
| 0 | +0.71 | Approximately 0.00 | −0.70 | Older customers with average income and lower spending |
| 1 | −0.76 | Approximately 0.00 | +0.74 | Younger customers with average income and higher spending |

Age and spending provide the clearest differences between the selected segments.

## Possible Business Applications

- **Cluster 0:** Test value offers and practical product bundles.
- **Cluster 1:** Test loyalty rewards, premium offers and bundle upgrades.

These are campaign ideas to test. The clustering results do not prove customer preferences or likely campaign responses.

## Tools Used

- Python
- pandas and NumPy
- scikit-learn
- SciPy
- Matplotlib and Seaborn
- Jupyter Notebook

## How to Run

1. Download or clone the repository.
2. Install the required packages:

   ```bash
   python -m pip install pandas numpy scikit-learn scipy matplotlib seaborn notebook
   ```

3. Keep `Customer-Data.csv` beside the notebook.
4. Replace the existing Windows path and dataset filename in the data-loading cell with:

   ```python
   df = pd.read_csv("Customer-Data.csv")
   ```

5. Start Jupyter:

   ```bash
   jupyter notebook
   ```

6. Open `Customer_Clustering.ipynb` and run the cells in order.

## Limitations and Future Improvements

- The clustering uses only **198 customers** after cleaning.
- Two-component PCA leaves out **28.16% of the original variance**.
- Compare results with and without the maximum-income customers.
- Check cluster stability across random seeds and different feature selections.
- Review DBSCAN noise points separately when evaluating its results.
- Test campaign ideas before using the segments for business decisions.

## Author

**Yan Myoe Naing**  
Applied AI and Analytics, Singapore Polytechnic
