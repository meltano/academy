# [Meltano Academy](../README.md) > [Labs](./README.md) > End-to-End CI/CD with Meltano and GitHub

## Prereqs

### Prior Labs

This lab starts where the the [Extract-Load](./build_your_first_pipeline.md) and
[DBT Transformation](./data_transformation_with_dbt.md) labs finish. The starting
template for this lab includes completed results from both of these labs. While
you can complete this lab even if you did not complete the prior labs, certain
parts of the lab will make more sense if the prior labs have already been completed.

### GitHub Account

This lab requires you to have a GitHub account. Please create an account if you don't
have one already. You can request a password reset email from GitHub if you do not remember
your credentials.

### Snowflake Account

This lab assumes you have a Snowflake account you can use in your data pipeline. Other
SQL platforms can be used with some alteration of the steps and the profile definitions,
but this lab will assume you are using Snowflake.

## Step 1: Start a new Project

To start, you will create your own personal duplicate of the sample project. Navigate
to the template project here and then click on the green "Use this template" button.

- If prompted, select your personal username as the owner for your new project.
- For "Repository name" you can use any name you'd like, for example "AJ's CICD Lab"
- Select "Public" to share your lab with others, including the instructor for feedback.

## Step 2: Create a default CI/CD Pipeline

1. Click the "Actions" tab in your new project repo.
2. From the Actions tab, select the option to `set up a workflow yourself->`.
3. In the space provided, delete the existing template and paste in the below yaml text:

<details>
<summary>CI/CD Workflow Yaml Text</summary>

```yml
# This is a basic workflow to help you get started with Actions

name: CI

# Controls when the workflow will run
on:
  # Triggers the workflow on push or pull request events but only for the main branch
  push:
    branches: [ main ]
  pull_request:
    branches: [ main ]

  # Allows you to run this workflow manually from the Actions tab
  workflow_dispatch:

# A workflow run is made up of one or more jobs that can run sequentially or in parallel
jobs:
  # This workflow contains a single job called "build"
  build:
    # The type of runner that the job will run on
    runs-on: ubuntu-latest

    # Steps represent a sequence of tasks that will be executed as part of the job
    steps:
      # Checks-out your repository under $GITHUB_WORKSPACE, so your job can access it
      - uses: actions/checkout@v2

      # Runs a single command using the runners shell
      - name: Run a one-line script
        run: echo Hello, world!

      # Runs a set of commands using the runners shell
      - name: Run a multi-line script
        run: |
          echo Add other actions to build,
          echo test, and deploy your project.
```

</details>

4. Click the green "Start commit" button and then "Commit new file", keeping all default options
   to commit directly to `main` branch.

5. Click the "Actions" tab again and this time notice that there's now a CI/CD workflow job running.
    - Click on the new CI/CD job name to view its details.
    - Within a minute or two, you should see a green checkmark, indicating the CI build was successful.

## Step 3: Modify the workflow to use the Snowflake profile

1. Open workflow and find the line that begins with `meltano elt ...`.
2. Replace the text `target-jsonl` with `target-snowflake`. Commit your changes again, but this
   time save to a new branch and select the option to automatically open Pull Request. We will wait to merge the pull request until we are satisfied
   that the pipeline is working correctly.
3. Unless you've skipped ahead, your new pipeline should fail. The reason for this is that there are
   no available credentials for connecting to Snowflake. We'll fix this in the next step, but for now
   notice that the CI/CD failure is obvious and clear sign to an approver that there's more work to be
   done before merging to the main branch.

# Step 4: Add CI/CD Credentials and retry the job

1. Click on the `Settings` tab and then select `Secrets` from the left-hand navigation pane.
2. Select `New Repository Secret` and create a secret named (exactly) `TARGET_SNOWFLAKE_USERNAME` and enter your username in the space provided.
   - Note that after you've saved a repository secret, it cannot be viewed again from the Web UI.
     This is for your security.
3. Repeat these steps until all of the following secrets are set:
   - `TARGET_SNOWFLAKE_ACCOUNT`
   - `TARGET_SNOWFLAKE_DATABASE`
   - `TARGET_SNOWFLAKE_PASSWORD`
   - `TARGET_SNOWFLAKE_ROLE`
   - `TARGET_SNOWFLAKE_USERNAME`
   - `TARGET_SNOWFLAKE_WAREHOUSE`
4. Once all of the repository secrets are entered, go back to your failed job and select the
   option to re-run the failed job.

## Step 5: Add `dbt run` to your workflow

In this step, you'll add `dbt run` to the CI/CD workflow. This will ensure all transforms
are tested whenever the code is updated.

1. Open the workflow file you created in the first step and then select "Edit".
2. Paste the below text at the bottom of the file. This will add an additional step to
   have meltano execute `dbt run` at the end of the pipeline.

    ```yml
        - run: meltano invoke dbt:run
    ```

3. After committing the change to your development branch, you should see a new pipeline.
   This pipeline will additionally run `dbt run` after your EL pipeline is completed.

## Step 6: Review the PR and Merge

For this final step, navigate to your PR, click the "Files changed" tab and review the changes.
Now go to the "Conversation" tab and notice if you have a green checkmark. If the code looks good
and the green checkmark is displayed, go ahead now and click "Merge pull request". This will
merge all of the changes you have made on this branch back into the main branch.
