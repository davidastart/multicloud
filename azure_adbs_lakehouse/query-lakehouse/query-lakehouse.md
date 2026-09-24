# Query the Lakehouse with Select AI

## Introduction

In this lab, you activate the lakehouse profile, ask a natural-language question, inspect the generated SQL, and then run the approved query.

Estimated Time: 10 minutes

### Objectives

In this lab, you will:

- Activate and verify the Select AI profile
- Generate SQL without running it
- Review and run an approved generated query
- Explore additional lakehouse questions

## Task 1: Activate the Select AI Profile

1. In SQL Developer, open a worksheet for the `LAKE_DEMO` connection.

2. Activate the profile:

    ```sql
    BEGIN
      DBMS_CLOUD_AI.SET_PROFILE('LAKEHOUSE_AZURE_OPENAI');
    END;
    /
    ```

3. Verify the active profile:

    ```sql
    SELECT DBMS_CLOUD_AI.GET_PROFILE
    FROM DUAL;
    ```

4. Confirm that the result is `LAKEHOUSE_AZURE_OPENAI`.

## Task 2: Generate and Review SQL

1. Generate SQL for a business question without running the generated statement:

    ```sql
    SELECT DBMS_CLOUD_AI.GENERATE(
      prompt       => 'Show discounted revenue by customer market segment.',
      profile_name => 'LAKEHOUSE_AZURE_OPENAI',
      action       => 'showsql'
    ) AS generated_sql
    FROM DUAL;
    ```

2. Review the generated statement. Confirm that it:

    - Uses only objects in the approved profile
    - Contains a read-only `SELECT` statement
    - Joins columns that represent the requested business relationship

3. If the generated SQL is appropriate, run the same prompt with the `runsql` action:

    ```sql
    SELECT DBMS_CLOUD_AI.GENERATE(
      prompt       => 'Show discounted revenue by customer market segment.',
      profile_name => 'LAKEHOUSE_AZURE_OPENAI',
      action       => 'runsql'
    ) AS result
    FROM DUAL;
    ```

> **Note:** Generative AI output can vary. Always review generated SQL before using `runsql`.

## Task 3: Explore Additional Questions

1. Try a movie question with the package API:

    ```sql
    SELECT DBMS_CLOUD_AI.GENERATE(
      prompt       => 'List the top 10 drama movies by views.',
      profile_name => 'LAKEHOUSE_AZURE_OPENAI',
      action       => 'showsql'
    ) AS generated_sql
    FROM DUAL;
    ```

2. After the profile is active, you can also use the `SELECT AI SHOWSQL` syntax. Try one or more of these questions:

    ```sql
    SELECT AI SHOWSQL 'Show total actual sales revenue, transaction count, and average actual price by customer country and genre name, ordered by revenue descending.';

    SELECT AI SHOWSQL 'Compare total revenue, average transaction value, and transaction count by customer age group and gender.';

    SELECT AI SHOWSQL 'Show revenue, transaction count, average discount percent, and average actual price by customer segment name.';

    SELECT AI SHOWSQL 'Find the top 20 customers by total actual sales price for each genre and include customer name, email, country, genre, and transaction count.';

    SELECT AI SHOWSQL 'Compare discount type, average discount percent, and total revenue by income level and genre.';

    SELECT AI SHOWSQL 'Show the app, device, operating system, payment method, and genre combinations that generate the most revenue in each customer country.';

    SELECT AI SHOWSQL 'Show monthly revenue and transaction count by customer segment and genre using DAY_ID.';

    SELECT AI SHOWSQL 'Identify segments with the highest average credit balance, mortgage amount, income, and sales revenue.';

    SELECT AI SHOWSQL 'Compare promotion response rate, total revenue, average discount percent, and average actual price by genre and customer segment.';

    SELECT AI SHOWSQL 'For customers with insufficient funds incidents or late mortgage or rent payments, show transaction count, revenue, average discount, and preferred genre compared with other customers.';
    ```

3. For each prompt, review the generated SQL and identify the tables, views, joins, filters, and aggregations Select AI chose.

## Acknowledgements

- **Author** - Oracle Multicloud Team
- **Last Updated By/Date** - Oracle LiveLabs, September 2026
