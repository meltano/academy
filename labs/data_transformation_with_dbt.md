# [Meltano Academy](../README.md) > [Labs](./README.md) > Data Transformation with dbt and Snowflake

This lab will walk you through the process of building a dbt Transformation pipeline on Snowflake.

## Prereqs

Before starting this lab, we recommend you complete the [first](./build_your_first_pipeline.md) and [second](./build_your_own_tap.md) labs in this course. These will ensure you have raw data loaded into Snowflake and ready for data transformation.

## Step 1: Configure your Snowflake profile in dbt

Before you can start working with dbt, you'll need to configure your dbt profiles file. This file contains the information dbt needs in order to connect to Snowflake and run queries on your behalf.

## Step 2: Create your first SELECT transformation file in SQL and test

To start with, create a very simple SELECT statement and save it to your project as a new file,
called `us_west_accounts.sql`:

```sql
-- us_west_accounts.sql: query for just accounts in us-west region.
SELECT *
FROM raw_sfdc.accounts
where region = 'us-west'
```

Now, immediately execute `dbt run` and then debug any errors that you see.

## Step 3: Create your source.yml definitions

You've got a simple working project now, but it isn't very flexible or dynamic. What if you want
to support multiple test or production environments? Let's add a simple `source.yml` file:

```yml
version: 2  # Version number of this config, we are currently using the "v2" dialect.
sources:
  - name: sfdc
    database: raw_db
    schema: sfdc
    tables:
      - name: accounts  # corresponds to 'raw_db.sfdc.accounts'
# Your config can have multiple sources
# - name: stripe
#   tables:
#     - name: payments
```

## Step 4: Replace dependencies with `source()` or `ref()` in Jinja templates

Now that you have a working pipeline and some metadata about your sources, we need to tell
dbt how to sequence dependencies and how
to deal with parameterized or disposable environments. This is performed by using one of two
Jinja templating functions: `source()` for upstream source tables (external to the project) 
and `ref()` for all other tables (internal to the project).

So, given the sample query you created in Step 1, we can rewrite as:

```sql
-- us_west_accounts.sql: query for just accounts in us-west region.
SELECT *
FROM {{ source("sfdc", "accounts") }}  -- dynamically locate the 'accounts' table in the 'sfdc' source
where region = 'us-west'
```

And then, to write a second transform which summarizes all the accounts in
the 'us-west' region, we'd write a second transform. This time we use `ref()`
syntax instead of `source()` since we're referencing another SQL file in our own project.

```sql
-- us_west_accounts_summary.sql: summarize just the accounts in us-west region.
SELECT *
FROM {{ ref("us_west_accounts") }} -- Same as file name, excluding the `.sql` suffix.
```

### Retest and debug

Now that you've updated your queries to reference each other, dbt is able to automatically
sequence your jobs in the correct order. Test that this is working now by executing `dbt run`
just as you did in `Step 1`.

If any errors are reported, check to see if your syntax is correct and if you've correctly
wrapped the jinja functions in double-curly brackets (`{{...}}`)

## Step 4: Add some tests

We're now ready to test that our data is correct. Let's add some validations to make sure
our primary key is never null and never duplicated. Here are some sample tests you can adapt
to your use case:

<!-- `schema.yml` -->

```yml
version: 2

models:
  - name: us_west_accounts
    columns:
      - name: account_id
        tests:
          - unique
          - not_null
      - name: region
        tests:
          - accepted_values:
              values: ['us-west']
      - name: is_prospect
        tests:
          - accepted_values:
              values: ['Y', 'N']
      - name: customer_id
        tests:
          - relationships:
              to: ref('customers')
              field: id
```

Note: Out of the box, dbt ships with four generic tests already defined: `unique`, `not_null`, `accepted_values`, and `relationships`.

For this exercise, first create some assertions ("tests") which you know are supposed to be
true and then run `dbt test` to confirm your assumptions. If those tests all pass successfully,
add new tests or modify your test so that they fail on purpose. Rerun `dbt test` and observe the
results.

## Wrap Up

Congratulations! If you’ve gotten this far, you have successfully created your own data transfomration layer using dbt. You’ve also seen how to modify configuration files and launch the Meltano UI web application.

## Additional Resources

- DBT Getting Started Tutorial: https://docs.getdbt.com/tutorial/setting-up
