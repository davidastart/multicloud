# Get Started with the Azure Event Environment

## Introduction

In this lab, you retrieve the temporary event credentials, sign in to Azure, complete multifactor authentication (MFA), and connect to the assigned Windows virtual machine.

Estimated Time: 15 minutes

### Objectives

In this lab, you will:

- Retrieve your event credentials from LiveLabs
- Sign in to the Azure portal and configure MFA
- Download and open the RDP file for your assigned virtual machine

## Task 1: Retrieve Your Azure Event Credentials

1. On the LiveLabs workshop page, select **View Login Info**.

2. Locate the Azure event account details. Keep the panel open so you can copy the following values when prompted:

    - Azure user name
    - Azure password
    - Windows virtual machine password
    - Assigned user number or resource suffix

3. Open the [Azure portal](https://portal.azure.com) in a new browser tab.

    ![Microsoft Azure sign-in page](images/azure-sign-in.png " ")

4. Copy the Azure user name from **View Login Info**, paste it into the sign-in page, and select **Next**.

5. Copy the Azure password from **View Login Info**, paste it into the password field, and select **Sign in**.

> **Note:** These event credentials are temporary. Use only the resources assigned to your account.

## Task 2: Configure Multifactor Authentication

1. On the **More information required** page, select **Next**.

    ![Microsoft multifactor authentication introduction](images/mfa-introduction.png " ")

2. Install **Microsoft Authenticator** on your mobile device, and then select **Next** in the browser.

    ![Microsoft Authenticator installation prompt](images/install-authenticator.png " ")

3. On the **Set up your account** page, select **Next**.

    ![Set up the account in Microsoft Authenticator](images/set-up-authenticator.png " ")

4. In Microsoft Authenticator, select the QR-code icon or **Add account**, choose **Work or school account**, and scan the QR code displayed in your browser.

    ![QR-code icon in Microsoft Authenticator](images/authenticator-qr-icon.png " ")

5. When the browser displays a number, enter that number in Microsoft Authenticator and approve the request.

    ![Number displayed in the browser](images/number-match-browser.png " ")

    ![Number entry in Microsoft Authenticator](images/number-match-phone.png " ")

6. After the browser confirms that Microsoft Authenticator was added, select **Done**.

    ![Microsoft Authenticator added confirmation](images/authenticator-added.png " ")

7. If prompted to stay signed in, select **Don't show this again**, and then select **Yes**.

    ![Stay signed in prompt](images/stay-signed-in.png " ")

8. Confirm that the Azure portal opens.

    ![Azure portal home page](images/azure-portal.png " ")

## Task 3: Connect to the Windows Virtual Machine

1. In the Azure portal search bar, enter **Virtual machines**, and select **Virtual machines** from the results.

    ![Search for Virtual machines in Azure](images/search-virtual-machines.png " ")

2. Select the virtual machine whose name matches the user number shown in **View Login Info**.

    ![Select the assigned virtual machine](images/select-virtual-machine.png " ")

3. On the virtual machine page, expand **Connect**, select **Connect**, and locate **Connect using RDP file**.

    ![Connect to the virtual machine with RDP](images/connect-rdp.png " ")

4. Select **Download RDP File**. When the download completes, open the `.rdp` file.

5. If a security warning appears, confirm that you want to connect.

6. Enter `azureuser` as the user name. Copy the Windows virtual machine password from **View Login Info**, paste it into the password field, and select **OK**.

7. Accept the certificate warning if prompted. Keep the remote desktop session open for the remaining labs.

## Acknowledgements

- **Author** - Oracle Multicloud Team
- **Last Updated By/Date** - Oracle LiveLabs, September 2026
