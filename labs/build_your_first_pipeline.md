# [Meltano Academy](../README.md) > [Labs](./README.md) > Building Your First Data Pipeline

Adapted from: [Meltano Tutorial - Transform and Analyze Postgres Data](https://meltano.com/tutorials/postgres-with-postgres.html#intro)

## Prerequisites

Python, pip, and pipx should be installed on your computer.
You should have a code editor installed. (VS Code will be used in our examples.)
Windows users should have WSL2 installed. (May require a restart.)

For Snowflake access, you will require the following information:

```yml
      snowflake_account: slalom_training
      snowflake_database: SWIFT_DB
      snowflake_role: TRAINING_ROLE
      snowflake_schema: PUBLIC
      snowflake_username: SWIFT
      snowflake_warehouse: SWIFT_WH
```

## Step 1. Install Meltano and Initialize a new Meltano project

### Option A: Open a pre-built dev container

Navigate to the sample project, click `Open in VS Code`, and then select the option for opening in a Docker container.

### Option B: Install locally on your laptop

Install pipx if needed:

```bash
python -m pip install pipx
python -m pipx ensurepath
```

Install meltano:

```bash
> pipx install meltano
```

Confirm your version:

```bash
> meltano --version
```

### Step 2. 

```bash
# Create a Source folder if you haven't already
mkdir -p  ~/Source
cd ~/Source
# Initialize a new Meltano project folder
meltano init meltano-lab-project
cd meltano-lab-project
```

## Step 3. Installing the sample taps and targets

Install a tap for the National Grid ESO's Carbon Emissions Intensity API:

```bash
> meltano add extractor tap-carbon-intensity
```

Install a target that simply writes the data to a text file:

```bash
# Install the JSONL target:
> meltano add loader target-jsonl
# Create an output path:
> mkdir -p ./output
> meltano config target-jsonl set destination_path ./output
```

Run the pipeline and check that everything is working correctly:

```bash
> meltano elt tap-carbon-intensity target-jsonl
```

Congratulations! You have successfully tested your sample pipeline. Now let’s connect a real target.

## Step 4: Scheduling via Meltano Web GUI

```bash
> meltano ui start
# Once the server has started, click the URL provided or navigate by
# copy-pasting to a browser window: http://localhost:5000
```

Once you’ve opened the web UI, explore the available UI options to add new extractors, customize their settings, and add scheduled pipelines.

Create and test a new daily schedule for your Carbon Intensity extractor.

## Step 5. Install and configure your SQL data target

Every DataOps environment should have at least one modern data platform which supports the SQL language. For this example, we will use Snowflake as our SQL data platform.

Let’s add Snowflake as a target:

```bash
> meltano add target-snowflake
```

Open the Web GUI to update your target settings, or use the configuration guide here: https://hub.meltano.com/loaders/snowflake.html 

Test your new target to ensure credentials are correct and data is able to be loaded.

```bash
> meltano elt tap-carbon-intensity target-snowflake
```

## Step 6: Review the contents of `meltano.yml`

At this point, it is helpful to review the contents of meltano.yml since all of the changes you made in the UI or the CLI have all been stored there in the file. Also, if you had any typos along the way, many mistakes can be fixed by simply modifying the text in this file.

<details>
<summary>Example “Solution” File:</summary>

```yml
version: 1
send_anonymous_usage_stats: true
project_id: 5eb968ed-22cb-4b72-b9e1-f857b22c624f
plugins:
  extractors:
  - name: tap-carbon-intensity
    variant: meltano
    pip_url: git+https://gitlab.com/meltano/tap-carbon-intensity.git
  loaders:
  - name: target-jsonl
    variant: andyh1203
    pip_url: target-jsonl
    config:
      destination_path: ./output
  - name: target-snowflake
    variant: datamill-co
    pip_url: target-snowflake
    config:
      snowflake_account: slalom_training
      snowflake_database: SWIFT_DB
      snowflake_role: TRAINING_ROLE
      snowflake_schema: PUBLIC
      snowflake_username: SWIFT
      snowflake_warehouse: SWIFT_WH
  - name: target-bigquery
    variant: adswerve
    pip_url: git+https://github.com/adswerve/target-bigquery.git@v0.10.2
schedules:
- name: carbon-intensity-to-jsonl-daily
  extractor: tap-carbon-intensity
  loader: target-jsonl
  transform: skip
  interval: '@daily'
  start_date: 2021-07-12 21:36:43.505974
- name: carbon-intensity-to-snowflake
  extractor: tap-carbon-intensity
  loader: target-snowflake
  transform: skip
  interval: '@daily'
  start_date: 2021-07-12 21:52:25.147648
```

</details>


## Wrap Up

Congratulations! If you’ve gotten this far, you have successfully created your own data pipeline. You’ve also seen how to modify configuration files and launch the Meltano UI web application.
