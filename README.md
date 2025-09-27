# **Spark RDD Project on Google Cloud (3-Node Cluster)**

**Overview:**

This project demonstrates the implementation of Spark RDDs on a 3-node cluster using Google Cloud Platform (GCP).
The main goal was to evaluate datasets related to:

1. NBA shot logs – finding comfortable shooting zones for players.

2. NYC Parking Violations – estimating ticket probability for black vehicles at specific street codes.

3. NYC Parking Violations (temporal analysis) – determining when tickets are most likely to be issued with different levels of parallelism.

The project leverages PySpark for distributed processing and showcases map-reduce transformations on real-world datasets.



**Technologies Used:**

1. Google Cloud Platform (GCP) – Cluster setup (3 VMs)

2. Apache Spark – Distributed data processing

3. PySpark – Python API for Spark

4. HDFS – Distributed file storage

5. K-Means (Spark MLlib) – Clustering algorithm

6. RDD Transformations & Actions – Core operations



📂**Project Structure:**

*_Task 1 – NBA Comfortable Zones_*
Dataset: NBA Shot Logs 2014–2015. Used K-Means clustering on [SHOT_DIST, CLOSE_DEF_DIST, SHOT_CLOCK] to find 4 comfortable shooting zones per player. Calculated hit rates per zone for: James Harden, Chris Paul, Stephen Curry, LeBron James.

**_Task 2 – Parking Ticket Probability_**
Dataset: NYC Parking Violations. Computed probability that a black vehicle parked at street codes [34510, 10030, 34050] receives a ticket.
Used conditional probability: P(\text{ticket} | \text{black vehicle on given streets}) = \frac{\text{# black vehicles ticketed}}{\text{total vehicles ticketed}}.

**_Task 3 – Ticket Issuance Time_**
Dataset: NYC Parking Violations. Found most frequent month-time pair for ticket issuance. Parallelism tested with Spark configurations: 2, 3, 4, 5. Compared execution times for different parallelization levels.



**Key Concepts:**

RDD (Resilient Distributed Dataset) = Immutable, partitioned collections of data processed across nodes.
Vector Assembler (Spark MLlib) = Combined multiple features into a single feature vector for K-Means input.
Broadcast Variables = Distributed references for street codes and vehicle color mappings.
MapReduce Pattern = Used for counting hits, calculating probabilities, and aggregating ticket frequencies.

How to Run: setup cluster on GCP; create a 3-node Spark cluster using GCP VMs; configure Spark and HDFS; load Data; upload datasets to HDFS or local cluster storage; run Tasks


# Example: Run with parallelism = 4
spark-submit --conf spark.default.parallelism=4 main.py

Outputs:
Task 1: Comfortable zones with max hit rate for each player.
Task 2: Probability of a black vehicle being ticketed.
Task 3: Most frequent (month-time) pair for ticket issuance + runtime comparison across parallelism levels.

Results:
Task 1: Identified most comfortable shooting zones for each player.
Task 2: Estimated probability for black vehicles at given street codes.
Task 3: Found peak ticket issuance time and showed how parallelism impacts execution speed.
