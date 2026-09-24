# Configure Select AI with Azure OpenAI

## Introduction

In this lab, you allow the `LAKE_DEMO` schema to call the event's Azure OpenAI resource, store the Azure OpenAI key in a database credential, and create a Select AI profile restricted to approved workshop objects.

Estimated Time: 10 minutes

### Objectives

In this lab, you will:

- Grant outbound HTTP access to the Azure OpenAI host
- Create an Azure OpenAI credential
- Create a governed Select AI profile

## Task 1: Allow Access to Azure OpenAI

1. In SQL Developer, open a worksheet for the `ADMIN` connection.

2. Run the following block to allow the `LAKE_DEMO` schema to call the event's Azure OpenAI host:

    ```sql
    BEGIN
      DBMS_NETWORK_ACL_ADMIN.APPEND_HOST_ACE(
        host => 'hol-open-ai.openai.azure.com',
        ace  => xs$ace_type(
          privilege_list => xs$name_list('http'),
          principal_name => 'LAKE_DEMO',
          principal_type => xs_acl.ptype_db
        )
      );
    END;
    /
    ```

## Task 2: Create the Azure OpenAI Credential

1. Open a worksheet for the `LAKE_DEMO` connection.

2. In **View Login Info**, locate the Azure OpenAI API key supplied for the event. Copy the value, but do not share or save it in a script file.

3. Replace `<azure-openai-api-key>` in the following block with the supplied key, and then run the block:

    ```sql
    BEGIN
      DBMS_CLOUD.CREATE_CREDENTIAL(
        credential_name => 'AZURE_OPENAI_CRED',
        username        => 'azure_openai',
        password        => '<azure-openai-api-key>'
      );
    END;
    /
    ```

> **Note:** The placeholder prevents an API key from being stored in the workshop source. If **View Login Info** does not include the key, ask the event facilitator for the Azure OpenAI API key.

## Task 3: Verify the Approved Objects

The profile includes the external objects you created and three dimension tables pre-created in the `LAKE_DEMO` schema.

1. Run the following query:

    ```sql
    SELECT table_name
    FROM user_tables
    WHERE table_name IN (
      'CUSTOMER_EXT',
      'CUSTOMER_EXTENSION',
      'CUST_SALES_EXT',
      'CUSTOMER_SEGMENT',
      'GENRE'
    )
    UNION ALL
    SELECT view_name
    FROM user_views
    WHERE view_name IN (
      'MOVIES_EXT',
      'MOVIES_BY_GENRE'
    )
    ORDER BY 1;
    ```

2. Confirm that the query returns all seven object names. If a pre-created dimension table is missing, ask the event facilitator to verify the database assigned to you.

## Task 4: Create the Select AI Profile

1. Run the following block. Use the Azure OpenAI resource name—not its endpoint URL—for `azure_resource_name`.

    ```sql
    BEGIN
      DBMS_CLOUD_AI.CREATE_PROFILE(
        profile_name => 'LAKEHOUSE_AZURE_OPENAI',
        attributes   => q'~{
          "provider": "azure",
          "azure_resource_name": "hol-open-ai",
          "azure_deployment_name": "hollakehouse-nlq",
          "credential_name": "AZURE_OPENAI_CRED",
          "object_list": [
            {"owner": "LAKE_DEMO", "name": "CUSTOMER_EXT"},
            {"owner": "LAKE_DEMO", "name": "CUSTOMER_EXTENSION"},
            {"owner": "LAKE_DEMO", "name": "CUST_SALES_EXT"},
            {"owner": "LAKE_DEMO", "name": "CUSTOMER_SEGMENT"},
            {"owner": "LAKE_DEMO", "name": "GENRE"},
            {"owner": "LAKE_DEMO", "name": "MOVIES_EXT"},
            {"owner": "LAKE_DEMO", "name": "MOVIES_BY_GENRE"}
          ],
          "enforce_object_list": true,
          "comments": true,
          "additional_instructions": "Generate read-only Oracle SQL using only the allow-listed objects. Never generate DDL, DML, PL/SQL, or package calls."
        }~'
      );
    END;
    /
    ```

2. Confirm that the block completes successfully.

## Acknowledgements

- **Author** - Oracle Multicloud Team
- **Last Updated By/Date** - Oracle LiveLabs, September 2026
