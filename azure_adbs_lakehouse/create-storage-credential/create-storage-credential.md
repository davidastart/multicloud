# Create the Azure Storage Credential

## Introduction

Autonomous AI Database uses a database credential to authenticate to private objects in Azure Blob Storage. In this lab, you create the credential and verify that the database can list the workshop files.

Estimated Time: 10 minutes

### Objectives

In this lab, you will:

- Create a `DBMS_CLOUD` credential for Azure Blob Storage
- Verify access to the workshop container

## Task 1: Create the Credential

1. In SQL Developer, open a worksheet for the `LAKE_DEMO` connection.

2. In **View Login Info**, locate the Azure Storage access key supplied for the event. Copy the value, but do not share or save it in a script file.

3. Replace `<azure-storage-access-key>` in the following block with the supplied access key, and then run the block:

    ```sql
    BEGIN
      DBMS_CLOUD.CREATE_CREDENTIAL(
        credential_name => 'AZURE_BLOB_CRED',
        username        => 'holstac',
        password        => '<azure-storage-access-key>'
      );
    END;
    /
    ```

> **Note:** The placeholder prevents an access key from being stored in the workshop source. If **View Login Info** does not include the key, ask the event facilitator for the Azure Storage access key.

## Task 2: Verify Access to Azure Blob Storage

1. Run the following query:

    ```sql
    SELECT object_name, bytes
    FROM DBMS_CLOUD.LIST_OBJECTS(
      credential_name => 'AZURE_BLOB_CRED',
      location_uri    => 'https://holstac.blob.core.windows.net/hol-lab/'
    )
    ORDER BY object_name;
    ```

2. Confirm that the result includes objects under the `data/` path. The exact number of rows can change as the event files are updated.

3. If the query returns an authentication error, confirm that you used the Azure Storage access key—not the Azure account or virtual machine password—and recreate the credential with the correct value.

## Acknowledgements

- **Author** - Oracle Multicloud Team
- **Last Updated By/Date** - Oracle LiveLabs, September 2026
