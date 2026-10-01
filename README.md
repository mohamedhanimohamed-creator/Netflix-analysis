# Netflix Catalog Analysis

An exploratory data analysis (EDA) project examining the Netflix titles catalog with Python. The notebook investigates the composition of the catalog, including content type, release year, country, maturity rating, duration, genres, and dates when titles were added.

## Project goals

- Explore how movies and TV shows are represented in the catalog.
- Examine the distribution of titles across years, countries, ratings, and genres.
- Visualize patterns in the available metadata.
- Identify data-quality issues that affect interpretation.

## Repository structure

```text
Netflix-analysis/
├── netflex.ipynb       # Exploratory analysis and visualizations
├── netflix_titles.csv  # Source dataset
├── INSIGHTS.md         # Findings, caveats, and interpretation
├── README.md           # Project documentation
└── LICENSE
```

## Dataset

The CSV contains catalog metadata such as:

| Column | Description |
|---|---|
| `show_id` | Catalog identifier |
| `type` | Movie or TV Show |
| `title` | Title name |
| `director`, `cast` | Creative contributors |
| `country` | Country or countries associated with the title |
| `date_added` | Date the title was added to the catalog |
| `release_year` | Original release year |
| `rating` | Content maturity rating |
| `duration` | Movie runtime or number of seasons |
| `listed_in` | Genre/category labels |
| `description` | Short synopsis |

The notebook's displayed expanded table contains 19,323 rows, while the original catalog's title IDs are repeated across category labels. Therefore, **row counts after expansion are not equivalent to unique title counts**. Analyses should use unique `show_id` values when counting titles and should explicitly explode multi-valued columns when analyzing individual categories.

## Tools and techniques

- **Python** for analysis
- **Pandas** for loading, cleaning, transforming, and aggregating tabular data
- **NumPy** for numerical operations
- **Matplotlib** and **Seaborn** for visual exploration
- **Jupyter Notebook** for an interactive, reproducible workflow

## Run the analysis

1. Clone the repository.
2. Install the dependencies:

   ```bash
   pip install pandas numpy matplotlib seaborn jupyter
   ```

3. Start Jupyter:

   ```bash
   jupyter notebook
   ```

4. Open `netflex.ipynb` and run the cells from top to bottom. Keep `netflix_titles.csv` in the same directory as the notebook.

## Key interpretation notes

- Catalog availability is not the same as audience demand or viewership. The dataset contains title metadata, not streaming hours, ratings from viewers, or engagement.
- `date_added` and `release_year` describe different events: a title's addition to the catalog does not mean it was released that year.
- Genre, country, cast, and director fields can contain multiple values. Split these fields before counting individual categories.
- Missing metadata should be handled explicitly rather than silently treated as a meaningful category.
- The dataset is a snapshot. Results describe the supplied file, not Netflix's live catalog or current regional availability.

## Findings

See [INSIGHTS.md](INSIGHTS.md) for the project's findings and the caveats needed to interpret them correctly.
