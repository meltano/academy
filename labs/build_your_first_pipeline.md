# [Meltano Academy](../README.md) > [Labs](./README.md) > Building Your First Data Pipeline

Adapted from: [Meltano Tutorial - Transform and Analyze Postgres Data](https://meltano.com/tutorials/postgres-with-postgres.html#intro)

## Prerequisites:

Python, pip, and pipx should be installed on your computer.
You should have a code editor installed. (VS Code will be used in our examples.)
Windows users should have WSL2 installed. (May require a restart.)

## Step 1. Install Meltano

```bash
> pipx install meltano
```

Confirm your version:

```bash
> meltano --version
```

## Step 2. Installing the sample taps and targets

Install a tap for the National Grid ESO's Carbon Emissions Intensity API:

```bash
> meltano add extractor tap-carbon-intensity
```

Install a target that simply writes the data to a text file:

```bash
> meltano add loader target-jsonl
```

Test that everything is working correctly:

```bash
> meltano elt tap-carbon-intensity target-jsonl
```

Congratulations! You have successfully tested your sample pipeline. Now let’s connect a real target.

## Step 3: Scheduling via Meltano Web GUI

```bash
> meltano ui serve
> open localhost:8080
```

Once you’ve opened the web UI, explore the available UI options to add new extractors, customize their settings, and add scheduled pipelines.

Create and test a new daily schedule for your extractor.

## Step 4. Install and configure your SQL data target

Every DataOps environment should have at least one modern data platform which supports the SQL language. For this example, we will use Snowflake as our SQL data platform.

Let’s add Snowflake as a target:

```bash
> meltano add target-snowflake
```

Open the Web GUI to update your target settings, or use the configuration guide here: https://hub.meltano.com/loaders/snowflake.html 

Test your new target to ensure credentials are correct and data is able to be loaded.

```bash
> `meltano elt tap-carbon-intensity target-snowflake
```

## Step 5: Review the contents of `meltano.yml`

At this point, it is helpful to review the contents of meltano.yml since all of the changes you made in the UI or the CLI have all been stored there in the file. Also, if you had any typos along the way, many mistakes can be fixed by simply modifying the text in this file.

<details>
<summary>Example “Solution” File:</summary>

```bash
… <TODO:> Paste Sample `meltano.yml` here for reference 
```

</details>


## Wrap Up

Congratulations! If you’ve gotten this far, you have successfully created your own data pipeline. You’ve also seen how to modify configuration files and launch the Meltano UI web application.
