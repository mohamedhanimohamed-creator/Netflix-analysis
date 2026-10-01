# Analysis Insights

This document separates observations visible in the notebook from interpretation and data limitations. The analysis is based on the repository's supplied CSV snapshot, not Netflix's current catalog.

## Findings supported by the current notebook

### 1. The working table contains repeated title records

The notebook's displayed dataframe information reports **19,323 rows**. The sample output shows the same `show_id` repeated for a title under different `listed_in` values. This means the working table has been expanded by category, and its row count should not be described as the number of distinct Netflix titles.

**Why it matters:** Counting rows can overstate catalog size and distort any metric that is intended to describe titles. Use `show_id` (or another validated unique title key) for title-level counts. For category-level analysis, split multi-valued fields and count distinct titles per category.

### 2. Genre analysis needs category-level parsing

The notebook creates a “Top 10 Netflix Genres” chart using `Netflex['listed_in'].value_counts()`. In the source data, `listed_in` can contain comma-separated category labels. Counting the unsplit strings measures exact label combinations, not necessarily the frequency of each individual genre.

**Interpretation:** The visualization is a useful first look at how category values appear in the data, but it should not be presented as a definitive ranking of individual genres until the field is split into one category per row and distinct titles are counted.

### 3. The dataset supports catalog-composition analysis, not audience-preference claims

The available fields describe titles and their metadata: type, release year, country, rating, duration, categories, and synopsis. They do not include viewing hours, completion rates, user ratings, or user-level behavior.

**Interpretation:** The project can describe what is represented in this dataset, but cannot establish which titles audiences watched most, what viewers prefer, or how successful a title was.

## Questions the analysis is designed to explore

- How does the catalog divide between movies and TV shows?
- How are titles distributed across release years and catalog-addition dates?
- Which countries and categories appear most often?
- What maturity ratings are represented?
- How do movie runtimes differ from TV-show season counts?

These are exploratory questions. Numerical conclusions should be added only after the corresponding aggregation is run on distinct titles with multi-value fields handled consistently.

## Recommended improvements before treating the results as final

1. **Validate the unit of analysis.** Report both raw rows and unique `show_id` counts, and explain any row expansion.
2. **Parse multi-value columns.** Split `listed_in` and `country` into individual values before category frequency analysis.
3. **Separate movies from TV shows.** Analyze `duration` as minutes for movies and seasons for TV shows; do not compare these as one numeric measure.
4. **Handle missing values transparently.** Show missingness by column and state whether missing records are excluded or grouped.
5. **Distinguish release from acquisition.** Analyze `release_year` separately from `date_added`; neither is a proxy for viewership.
6. **Add quantified takeaways.** Include the actual counts, percentages, and date ranges next to each chart so readers can understand the scale and verify the claim.
7. **Improve reproducibility.** Restart the notebook kernel and run all cells in order before publishing, then remove stale outputs that no longer match the code.

## Bottom line

The notebook is a useful starting point for catalog EDA and visualization. Its most important analytical lesson so far is methodological: repeated rows and multi-valued metadata must be handled carefully before drawing conclusions about the number of titles or the prevalence of genres. Clear definitions of what each count represents will make the project's results much more credible.
