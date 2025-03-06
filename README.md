# DataProq Cluster Automation with Apache Airflow

## Overview
This project automates the creation of a DataProc cluster, executes a Spark job on it, and then deletes the cluster upon successful execution. The workflow is managed using Apache Airflow.

## Objective
The main objective is to:
1. Create a DataProc cluster.
2. Execute a Spark job that processes employee and department data.
3. Write the output data to a GCP bucket.
4. Delete the cluster after successful job execution.

## Data Description
- The GCP bucket `/data` contains two files:
  - `emp_data.csv` (Employee data)
  - `dept_data.csv` (Department data)
- The Spark job reads these files, filters employee data, performs a join operation with department data, and writes the processed data to the `/output` folder in the GCP bucket.

## Workflow Steps in Apache Airflow

1. **Import Required Libraries**
   - Required libraries are imported into the Airflow DAG script.

2. **Define Default Arguments**
   - The `default_args` dictionary is declared to specify DAG configurations such as retries and timeouts.

3. **Initialize DAG Object**
   - A DAG object is created using the `DAG()` function.

4. **Set Up Configuration Variables**
   - `cluster_name`, `project_id`, `region`, and cluster configuration are specified.

5. **Task 1: Create Cluster**
   - `DataProcCreateClusterOperator` is used to create the cluster.

6. **Task 2: Submit Spark Job**
   - `DataProcSubmitPySparkJobOperator` is used to submit the Spark job.
   - The bucket path where the Spark job script is located is specified.

7. **Task 3: Delete Cluster**
   - `DataProcDeleteClusterOperator` is used to delete the cluster after job execution.

8. **Define Execution Flow**
   - Tasks are executed in the following order:
     ```
     create_cluster >> submit_pyspark_job >> delete_cluster
     ```

## Technologies Used
- **Google Cloud Platform (GCP)**: For DataProc cluster and storage
- **Apache Airflow**: For workflow orchestration
- **Apache Spark**: For data processing
- **Python**: For scripting DAG and Spark job

## Execution Instructions
1. Deploy the Airflow DAG in your Airflow environment.
2. Ensure that the necessary permissions are granted for Airflow to interact with GCP resources.
3. Trigger the DAG manually or schedule it as per requirements.
4. Monitor the execution through the Airflow UI.

## Expected Output
- The final processed data is written to the `/output` folder in the GCP bucket after filtering and joining operations.
- The cluster is deleted after successful job execution.

## Conclusion
This project efficiently automates data processing using GCP DataProc and Apache Airflow, ensuring optimal resource usage by dynamically creating and deleting clusters as needed.

