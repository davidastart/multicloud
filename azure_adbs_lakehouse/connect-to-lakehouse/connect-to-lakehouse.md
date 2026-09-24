# Connect to Autonomous AI Database Lakehouse

## Introduction

In this lab, you download the wallet for your assigned Autonomous AI Database and create SQL Developer connections for the `ADMIN` and `LAKE_DEMO` users.

Estimated Time: 20 minutes

### Objectives

In this lab, you will:

- Download an instance wallet from Oracle AI Database@Azure
- Create an `ADMIN` connection in SQL Developer
- Create a `LAKE_DEMO` connection for the workshop tasks

## Task 1: Download the Database Wallet

1. From the Windows virtual machine, open a browser and sign in to the [Azure portal](https://portal.azure.com) with the event account.

2. In the Azure portal search bar, enter **Oracle AI Database@Azure**, and open the service.

    ![Search for Oracle AI Database at Azure](images/search-oracle-database-azure.png " ")

3. In the left menu, select **Oracle Autonomous AI Database**.

    ![Oracle Autonomous AI Database menu](images/autonomous-ai-database-menu.png " ")

4. Select the database assigned to your event account. Its numeric suffix should match your assigned user number.

    ![Select the assigned Autonomous AI Database](images/select-database.png " ")

5. Under **Settings**, select **Connections**, and then select **Download wallet**.

    ![Autonomous AI Database Connections page](images/database-connections.png " ")

6. Leave **Wallet type** set to **Instance wallet**. Enter and confirm a strong wallet password, and store it securely for the duration of the workshop.

7. Select **Download**.

    ![Download the instance wallet](images/download-wallet.png " ")

8. Save the wallet ZIP file in `C:\software`. Do not extract the ZIP file.

## Task 2: Create the ADMIN Connection

1. In the Windows virtual machine, open `C:\software\sqldeveloper`, and start the SQL Developer application.

    ![Start SQL Developer from the software directory](images/start-sql-developer.png " ")

2. In the **Connections** panel, select **New Connection**.

    ![Create a new SQL Developer connection](images/new-connection.png " ")

3. Enter these connection values, replacing `<database-name>` with the name of your assigned database:

    | Field | Value |
    | --- | --- |
    | Name | `ADMIN_<database-name>` |
    | Username | `ADMIN` |
    | Password | The ADMIN password from **View Login Info** |
    | Connection Type | `Cloud Wallet` |
    | Configuration File | `C:\software\Wallet_<database-name>.zip` |
    | Service | `<database-name>_high` |

    ![Select Cloud Wallet as the connection type](images/cloud-wallet-connection.png " ")

    ![Select the wallet file and high database service](images/select-wallet-and-service.png " ")

4. Select **Test** and confirm that **Status: Success** appears.

    ![Successful SQL Developer connection test](images/test-connection.png " ")

5. Select **Connect**. A SQL worksheet opens.

    ![SQL Developer worksheet connected as ADMIN](images/sql-worksheet.png " ")

## Task 3: Create the LAKE_DEMO Connection

1. Create another connection with these values:

    | Field | Value |
    | --- | --- |
    | Name | `LAKE_DEMO_<database-name>` |
    | Username | `LAKE_DEMO` |
    | Password | The LAKE_DEMO password from **View Login Info** |
    | Connection Type | `Cloud Wallet` |
    | Configuration File | `C:\software\Wallet_<database-name>.zip` |
    | Service | `<database-name>_high` |

2. Select **Test** and confirm that **Status: Success** appears.

3. Select **Connect**. Keep both connections available; later tasks identify which user must run each script.

## Acknowledgements

- **Author** - Oracle Multicloud Team
- **Last Updated By/Date** - Oracle LiveLabs, September 2026
