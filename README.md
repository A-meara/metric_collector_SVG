# Score Aggregation Metric Collector

This module aggregates individual metric scores from multiple h5ad files into a unified CSV table for analysis.

## Purpose

In the omnibenchmark pipeline:
1. **Metrics stage** produces individual h5ad files with scores for each (dataset × method × metric) combination
2. **Metric collector** aggregates all these individual scores into a single table

This is analogous to the `joinStates` aggregation in the OpenProblems Nextflow workflow.

## Input

The module takes as input all files matching `metrics.scores` (from the metrics stage), which are h5ad files containing:
- `uns['dataset_id']`: Dataset identifier
- `uns['method_id']`: Method identifier
- `uns['metric_ids']`: List of metric names (e.g., `["correlation"]`)
- `uns['metric_values']`: List of corresponding metric values

## Output

A CSV file with columns:
- `dataset_id`: Dataset identifier
- `method_id`: Method identifier
- `metric_id`: Metric name
- `metric_value`: Metric score

## Example Output

```csv
dataset_id,method_id,metric_id,metric_value
mouse_brain_coronal,boostgp,correlation,0.856
mouse_brain_coronal,random_ranking,correlation,0.023
mouse_brain_coronal,true_ranking,correlation,1.000
```
