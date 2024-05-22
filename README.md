# Airflow Introduction Practice

This repository is designed for practicing and getting introduced to Apache Airflow, a platform to programmatically author, schedule, and monitor workflows.

## Introduction

Apache Airflow is an open-source tool to help you automate workflows. It is used to manage, schedule, and monitor complex data pipelines. With Airflow, you can define workflows as directed acyclic graphs (DAGs) of tasks.

## Installation

To get started with Airflow, follow these steps:

1. **Clone the repository**:

   ```bash
   git clone https://github.com/seilylook/airflow-introduction.git
   ```

2. **Create a virtual environment**:

   ```bash
   python3 -m virtualenv venv
   source venv/bin/activate  # On Windows, use `venv\Scripts\activate`
   ```

3. **Install Airflow and dependencies**:

   ```bash
   pip install apache-airflow
   ```

4. **Initialize the Airflow database**:

   ```bash
   airflow db init
   ```

5. **Start the Airflow web server**:

   ```bash
   airflow webserver --port 8080
   ```

6. **Start the Airflow scheduler in a new terminal**:
   ```bash
   airflow scheduler
   ```

You can now access the Airflow web UI at `http://localhost:8080`.

## Quick Start

Here’s a quick guide to get you started with your first DAG (Directed Acyclic Graph).

1. **Create a DAG file**:

   ```python
   from airflow import DAG
   from airflow.operators.dummy import DummyOperator
   from datetime import datetime

   default_args = {
       'owner': 'airflow',
       'depends_on_past': False,
       'start_date': datetime(2023, 1, 1),
       'email_on_failure': False,
       'email_on_retry': False,
       'retries': 1,
   }

   dag = DAG(
       'example_dag',
       default_args=default_args,
       description='A simple tutorial DAG',
       schedule_interval='@daily',
   )

   start = DummyOperator(task_id='start', dag=dag)
   end = DummyOperator(task_id='end', dag=dag)

   start >> end
   ```

2. **Place your DAG file in the DAGs folder**:
   Copy the above DAG file to the `dags` directory in your Airflow installation path (e.g., `~/airflow/dags`).

3. **Access the DAG in the Airflow UI**:
   Go to `http://localhost:8080` and check the list of DAGs. You should see `example_dag` in the list.

## Usage

Airflow allows you to create and manage workflows using Python scripts. A typical workflow in Airflow is represented as a DAG (Directed Acyclic Graph) containing tasks. You can use various operators to define these tasks, such as:

- `BashOperator`
- `PythonOperator`
- `DummyOperator`

You can also define dependencies between tasks, set schedules, and configure retry policies.
