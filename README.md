# TV Audience Analytics with Apache Spark

Analysis of television viewing activity and household demographics using PySpark on Databricks. This project combines two assignments from Technion's Distributed Database Management course, covering distributed queries, audience segmentation, and streaming aggregation.

## Explore the project

Open [the notebook](tv_audience_analytics.ipynb) to follow the analysis and inspect the saved tables and PCA visualization. Results were produced in the original university Databricks environment. The two parts use separate course datasets and were not rerun as one continuous workflow.

## Part 1 — Large-Scale Viewing Analysis

The saved input counts include **34.3 million viewing events**, **13.2 million daily program records**, **203.6 million device-reference records**, and **357,721 demographic records**. These are row counts, not unique households or devices.

- Analyze genre popularity, household viewing activity, and prime-time viewing by television market.
- Apply ten coursework rules to score program records and summarize results by title.
- Rank markets using household income and net-worth attributes, then calculate relative softmax weights.

The implementation uses Spark DataFrame transformations, joins, broadcast joins, duplicate handling, and distributed aggregations.

## Part 2 — Audience Segmentation and Streaming

- Scale numerical demographic attributes and one-hot encode categorical features.
- Visualize household features with PCA and fit K-means with six clusters on the full feature vectors.
- Compare station viewing shares across clusters and subsets selected by distance from each cluster centroid.
- Read Kafka events with Spark Structured Streaming and incrementally maintain station counts in Delta Lake.
- Save cumulative batch results showing station preferences within each cluster's selected subset relative to the overall stream.

The six-cluster choice is based on visual inspection of the PCA projection, rather than quantitative model selection. Station comparisons measure shares of viewing events, not equal-weight household preferences.

## Technology

Python · PySpark · Spark MLlib · Spark Structured Streaming · Kafka · Delta Lake · Databricks · Matplotlib

## Data and execution

The original datasets and university infrastructure are not included. Running the analysis requires access to compatible data, a configured Spark environment, and the storage and Kafka connections used by the streaming section. Databricks-specific utilities are used in the original code.

The notebook is presented with saved results for review. Its original setup includes cells that stop active streaming queries and delete demonstration checkpoint and Delta directories; these cells are not needed to view the results.

## Scope and limitations

This is a coursework project demonstrating analysis of large stored datasets and micro-batch stream processing. It is not a production deployment or a throughput benchmark.

The streaming pipeline processes viewing events from Kafka in micro-batches, updates cumulative station counts in Delta Lake, and compares station preferences across household clusters. Results are saved after each batch to track how audience patterns change as new events arrive.
