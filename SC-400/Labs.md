  

# Lab Setup: Preparing Your Environment for Administration

In this lab, you'll configure and prepare your environment for administration tasks. You'll activate necessary features, set up administrative permissions, and ensure proper configuration of key elements.

**Tasks:**

- Set user passwords for lab exercises
- Enable Audit in the Microsoft Purview portal
- Enable Search by Name in Microsoft Teams
- Enable information barriers in SharePoint Online and OneDrive

## Task - Set user passwords for lab exercises

In this task, you'll set passwords for the user accounts needed for the labs.

- [ ] Log into Client 1 VM (SC-400-CL1) as the **SC-400-CL1\admin** account. The password should be provided by your lab hosting provider.
- [ ] Open **Microsoft Edge** and navigate to `**https://admin.microsoft.com**` and log into the Microsoft Purview portal as the MOD Administrator, `admin@WWLx549660.onmicrosoft.com`
- [ ] On the left navigation pane, expand **Users** then select **Active users**.
- [ ] Select the checkbox to the left of **Joni Sherman**, **Lynne Robbins**, and **Megan Bowen**.
    
    These accounts will be used through the lab exercises.
    
    [![](https://raw.githubusercontent.com/riswinto/SC-400T00A-Microsoft-Information-Protection-Administrator/master/Instructions/Media/user-accounts.png)](https://raw.githubusercontent.com/riswinto/SC-400T00A-Microsoft-Information-Protection-Administrator/master/Instructions/Media/user-accounts.png)
    
- [ ] Select the **Reset password** button from the top, navigation ribbon to reset all three passwords.
    
    [![](https://raw.githubusercontent.com/riswinto/SC-400T00A-Microsoft-Information-Protection-Administrator/master/Instructions/Media/reset-password-button.png)](https://raw.githubusercontent.com/riswinto/SC-400T00A-Microsoft-Information-Protection-Administrator/master/Instructions/Media/reset-password-button.png)
    
- [ ] In the **Reset Password** flyout page on the right, ensure all options are deselected.
    
    This will ensure that you can select a password for the three users being used for exercises, and that these passwords won't need to be reset when you first sign in.
    
- [ ] In the **Password** field, enter a password you can remember to reset the user passwords to be used in future exercises.
- [ ] At the bottom of the **Reset password** flyout page, select the **Reset password** button.
- [ ] On the **Passwords have been reset** page, you should see the three user accounts that have been reset. At the bottom of this flyout page, select **Close**.

You have successfully reset passwords for lab exercises.

## Task - Enable Audit in the Microsoft Purview portal

In this task, you'll enable Audit in the Microsoft Purview portal to monitor portal activities.

- [ ] You should still be logged into Client 1 VM (SC-400-CL1) as the **SC-400-CL1\admin** account and logged into Microsoft 365 with the MOD Administrator account.
- [ ] In Microsoft Edge, navigate to the Microsoft Purview portal, `https://purview.microsoft.com`, and log in.
- [ ] A message about the new Microsoft Purview portal will appear on the screen. Select the option to agree with the terms of data flow disclosure and the privacy statement, then select **Try now**.
    
    [![](https://raw.githubusercontent.com/riswinto/SC-400T00A-Microsoft-Information-Protection-Administrator/master/Instructions/Media/welcome-purview-portal.png)](https://raw.githubusercontent.com/riswinto/SC-400T00A-Microsoft-Information-Protection-Administrator/master/Instructions/Media/welcome-purview-portal.png)
    
- [ ] Select **Solutions** from the left sidebar, then select **Audit**.
- [ ] On the **Search** page, select the **Start recording user and admin activity** bar to enable audit logging.
    
    [![](https://raw.githubusercontent.com/riswinto/SC-400T00A-Microsoft-Information-Protection-Administrator/master/Instructions/Media/enable-audit-button.png)](https://raw.githubusercontent.com/riswinto/SC-400T00A-Microsoft-Information-Protection-Administrator/master/Instructions/Media/enable-audit-button.png)
    
- [ ] Once you select this option, the blue bar should disappear from this page.

You have successfully enabled auditing in Microsoft 365.

## Task - Enable search by name in Microsoft Teams

In this task, you'll enable the **Search by name** feature in Microsoft Teams for easy user location. This is needed for configuring information barriers in a later exercise.

- [ ] You should still be logged into Client 1 VM (SC-400-CL1) as the **SC-400-CL1\admin** account and logged into Microsoft 365 with the MOD Administrator account.
- [ ] In **Microsoft Edge**, navigate to `**https://admin.teams.microsoft.com**`.
- [ ] In the left navigation pane, under the **Teams** dropdown, select **Teams settings**.
    
    [![](https://raw.githubusercontent.com/riswinto/SC-400T00A-Microsoft-Information-Protection-Administrator/master/Instructions/Media/teams-settings.png)](https://raw.githubusercontent.com/riswinto/SC-400T00A-Microsoft-Information-Protection-Administrator/master/Instructions/Media/teams-settings.png)
    
- [ ] Scroll down to **Search by name** section and toggle the **Scope directory search using an Exchange address book policy** to **On**.
- [ ] Select **Save** at the bottom of the page.
- [ ] On the **Changes might take some time to take effect** dialogue, select **Confirm**.

You have successfully enabled the search by name feature in Microsoft Teams for information barriers.

## Task - Enable information barriers in SharePoint Online and OneDrive

In this task, you'll enable information barriers in SharePoint Online and OneDrive to ensure secure collaboration.

- [ ] You should still be logged into Client 1 VM (SC-400-CL1) as the **SC-400-CL1\admin** account.
- [ ] Open an elevated PowerShell window by selecting the Windows button with the right mouse button and then select **Windows PowerShell (Admin)**.
- [ ] Confirm the **User Account Control** window with **Yes**.
- [ ] Run the following cmdlet to install the latest version of the SharePoint Online PowerShell module:
    
    ```PowerShell
    powershell
    Install-Module -Name Microsoft.Online.SharePoint.PowerShell
    ```
    
- [ ] If prompted to install the PowerShell NuGet provider, enter **Y** to install the provider.
- [ ] If prompted to install from an untrusted repository, enter **Y** to install the module from the PSGallery.
- [ ] Run the following cmdlet to connect to the admin center for SharePoint Online:
    
    ```PowerShell
    powershell
     Connect-SPOService -Url https://WWLx549660-admin.sharepoint.com
    ```
    
    > Note: Be sure to update ZZZZZZ. ZZZZZZ is your unique tenant ID provided by your lab hosting provider.
    
- [ ] Login with the MOD Administrator password provided by your lab hosting provider.
- [ ] To enable information barriers in SharePoint and OneDrive, run the following command:
    
    ```PowerShell
    powershell
    Set-SPOTenant -InformationBarriersSuspension $false
    ```
    
- [ ] Close the PowerShell window once this is complete.

You have successfully enabled information barriers in SharePoint Online and OneDrive.

# Lab 1 - Exercise 1 - Manage compliance roles

As the recently hired Compliance Administrator for Contoso Ltd., you (Joni Sherman) need to ensure the new Microsoft 365 tenant complies with various legal and regulatory standards. Contoso Ltd. is expanding, and your role is crucial in maintaining compliance across different regions.

**Tasks**:

- [ ] Assign compliance roles
- [ ] Explore the Microsoft Purview portal

## Task 1 – Assign compliance roles

In this task, you'll assign the Compliance Admin role to Joni Sherman.

- [ ] Log into the Client 1 VM (SC-400-CL1) as the **SC-400-CL1\admin** account. The password should be provided by your lab hosting provider.
- [ ] Open **Microsoft Edge** and navigate to the Microsoft Purview portal, `https://admin.microsoft.com`, and log in as **MOD Administrator**, `admin@WWLx549660.onmicrosoft.com` Admin's password should be provided by your lab hosting provider.
- [ ] On the left sidebar, expand **Users** then select **Active users**.
- [ ] On the **Active users** page, search for `Joni`, then select **Joni Sherman**.
- [ ] The properties for Joni's account is displayed in a right, flyout panel. Select **Manage roles** on the flyout panel.
- [ ] On the **Manage admin roles** panel, select the option for **Admin center access**, then scroll down to expand **Show all by category**.
- [ ] Under the **Security & Compliance** category, select the checkbox for **Compliance Administrator**, then select **Save changes** at the bottom of the flyout panel.
- [ ] You should receive a message stating **Admin roles updated**.
- [ ] On the **Manage admin roles** page, select the **X** on the top right corner of the flyout panel to close the panel.
- [ ] Sign out of the MOD Administrator account by selecting the **MA** icon in the top right, then select **Sign out**.
    
    [![](https://raw.githubusercontent.com/riswinto/SC-400T00A-Microsoft-Information-Protection-Administrator/master/Instructions/Media/sign-out.png)](https://raw.githubusercontent.com/riswinto/SC-400T00A-Microsoft-Information-Protection-Administrator/master/Instructions/Media/sign-out.png)
    

You have successfully assigned Joni Sherman the Compliance Administrator role, which is required to perform the different exercises of this lab.

## Task 2 – Explore the Microsoft Purview portal

In this task, you'll sign in as Joni Sherman to explore the Microsoft Purview portal.

- [ ] You should still be logged into your Client 1 VM (SC-400-CL1) as the **SC-400-CL1\admin** account.
- [ ] In **Microsoft Edge**, navigate to `**https://purview.microsoft.com**`.
- [ ] When the **Pick an account** window is displayed, select **Use another account**.
- [ ] When the **Sign in** window is displayed, sign in as `JoniS@WWLx549660.onmicrosoft.com` Joni's password was set in a previous exercise.
- [ ] Get yourself familiar with the new Microsoft Purview Portal. When you are done, leave the browser window open.

You have successfully switched to Joni Sherman's account and are now ready to start the lab.

# Lab 1 - Exercise 2 - Manage sensitive information types

Contoso Ltd. previously had issues with employees accidentally sending out personal information from customers when working on support tickets in the ticketing solution. To prevent this, you need to create a custom sensitive information type to identify employee IDs in emails and documents.

**Tasks**:

- [ ] Create custom sensitive information types
- [ ] Create EDM-based classification information type
- [ ] Create EDM-based classification data source
- [ ] Create keyword dictionary
- [ ] Test custom sensitive information types

## Task 1 – Create custom sensitive information types

In this task, you'll create a new custom sensitive information type that recognizes the pattern of employee IDs near the keywords "Employee" and "ID".

- [ ] You should still be logged into Client 1 VM (SC-400-CL1) as the **SC-400-CL1\admin** account.
- [ ] In **Microsoft Edge**, navigate to `**https://purview.microsoft.com**` and log into the Microsoft Purview portal as `JoniS@WWLx549660.onmicrosoft.com` Joni's password was set in a previous exercise.
- [ ] On the left sidebar, select **Solutions** then select **Information Protection**.
- [ ] On the left sidebar, expand **Classifiers** then select **Sensitive info types**.
- [ ] On the **Sensitive info types** page, select **+ Create sensitive info type** to start the sensitive information type configuration.
- [ ] On the **Name your sensitive info type** page, enter:
    - **Name**: `Contoso Employee IDs`
    - **Description**: `Pattern for Contoso employee IDs.`
- [ ] Select **Next**.
- [ ] On the **Define patterns for this sensitive info type** page, select **Create pattern**.
- [ ] On the **New pattern** flyout panel on the right, select **+ Add primary element** > **Regular expression**.
- [ ] On the **+ Add a regular expression​** flyout panel on the right, enter:
    - **ID**: `Contoso IDs`
    - **Regular expression**: `[A-Z]{3}[0-9]{6}`
    - Select the radio button for _String match_
- [ ] Select **Done** at the bottom of the flyout panel.
- [ ] Back on the **New pattern** flyout panel, under **Supporting elements**, select **+ Add supporting elements or group of elements** drop-down menu and select **Keyword list**.
- [ ] On the **Add a keyword list** flyout panel on the right, enter:
    
    - **ID**: `Employee ID keywords`
    - **Case insensitive**:
    
    ```Plain
    text
    Employee
    ID
    ```
    
    - Select the radio button for _Word match_
- [ ] Select **Done** at the bottom of the flyout panel.
- [ ] Back on the **New pattern** flyout panel, under **Character proximity**, decrease the **Detect primary AND supporting elements** value to `100` characters.
- [ ] Select the **Create** button at the bottom of the flyout panel.
- [ ] Back on the **Define patterns for this sensitive info type** page select **Next**.
- [ ] On the **Choose the recommended confidence level to show in compliance policies** page use the default value and select **Next**.
- [ ] On the **Review settings and finish** page review the settings and select **Create**. When successfully created select **Done**.
- [ ] Sign out of Joni's account by selecting the profile picture of Joni Sherman in the top right. Select **Sign out**, then close the browser window.
- [ ] Close the browser window then open a new browser window.

You have successfully created a new sensitive information type to identify employee IDs in the pattern of three uppercase characters, six numbers, and the keywords 'Employee' or 'IDs' within a range of 100 characters.

## Task 2 – Create EDM-based classification information type

In this task, you'll create an Exact Data Match (EDM) based classification with a database schema of employee data.

- [ ] You should still be logged into Client 1 VM (SC-400-CL1) as the **SC-400-CL1\admin** account.
- [ ] Open **Microsoft Edge** then navigate to `**https://admin.microsoft.com**`.
- [ ] When the **Pick an account** page is displayed, select **Use another account** and sign in as **MOD Administrator** `admin@WWLx549660.onmicrosoft.com` Admin's password should be provided by your lab hosting provider.
- [ ] From the left pane, expand **Teams & groups** then select **Active teams & groups**.
- [ ] On the **Active teams and groups** page, on the top navigation ribbon, select **Security groups** then select **+ Add a security group**.
    
    [![](https://raw.githubusercontent.com/riswinto/SC-400T00A-Microsoft-Information-Protection-Administrator/master/Instructions/Media/add-security-group.png)](https://raw.githubusercontent.com/riswinto/SC-400T00A-Microsoft-Information-Protection-Administrator/master/Instructions/Media/add-security-group.png)
    
- [ ] On the **Set up the basics** screen, enter the following:
    - **Name**: `EDM_DataUploaders`
    - **Description**: `People who upload data for EDM.`
- [ ] Select **Next**.
- [ ] On the **Edit settings** page, leave the default settings, then select **Next**.
- [ ] On the **Review and finish adding group** page, review your settings and select **Create group**.
- [ ] On the **EDM_DataUploaders group created** page, select **Close**.
- [ ] Back on the **Active teams and groups** page, ensure the **Security** tab is selected from the top navigation ribbon, then select the **Refresh** button to display the newly created security group. Select the **EDM_DataUploaders** group from the list to open the **EDM_DataUploaders** flyout panel on the right.
- [ ] Select the **Members** tab then select **View all and manage members**.
- [ ] On the **Members** page select **+ Add members**.
- [ ] On the **Add members** page, select the checkbox to the left of **Joni Sherman**, then select the **Add (1)** button at the bottom of the flyout panel.
- [ ] Verify **Joni Sherman** is listed below **Members**, then close the flyout panel by selecting the **X** on the top right of the flyout panel.
- [ ] Sign out of the Mod Administrator account by selecting the MA icon on the top right of the window, then selecting **Sign out**.
- [ ] Close the browser window and open a new one.
- [ ] Navigate to the Microsoft Purview portal at `https://purview.microsoft.com`.
- [ ] When the **Pick an account** page is displayed, select **Joni Sherman** and sign in.
- [ ] Navigate to **Information Protection** by selecting **Solutions** > **Information Protection** from the left sidebar.
- [ ] On the **Information Protection** page, expand **Classifiers** then select **EDM classifiers**.
- [ ] On the **EDM classifiers** page, select **+ Create EDM classifier**.
- [ ] Examine the **Familiarize yourself with the steps needed to put your classifier to work** to understand the workflow for creating EDM classifiers, then select **Create EDM classifier**.
- [ ] On the **Name and describe your EDM classifier** page, enter:
    - **Name**: `employeedb`
    - **Description**: `Employee Database schema`
- [ ] Select **Next**.
- [ ] On the **Choose a method for defining your schema** page, select **Manually define your data structure**, then select **Next**.
- [ ] On the **Define columns that contain the data you want to detect**, enter these columns:
    
    - `Name`
    - `BirthDate`
    - `StreetAddress`
    - `EmployeeID`
    
    You should have four columns. You'll need to select the **+ Add column** button to add new fields for new columns.
    
    [![](https://raw.githubusercontent.com/riswinto/SC-400T00A-Microsoft-Information-Protection-Administrator/master/Instructions/Media/edm-columns.png)](https://raw.githubusercontent.com/riswinto/SC-400T00A-Microsoft-Information-Protection-Administrator/master/Instructions/Media/edm-columns.png)
    
- [ ] Select **Next**.
- [ ] On the **Select primary elements** page, for the **EmployeeID** column, expand the **Match mode** dropdown here **Single-token** is displayed, and select the **+** (plus sign) for **Choose a SIT**.
    
    [![](https://raw.githubusercontent.com/riswinto/SC-400T00A-Microsoft-Information-Protection-Administrator/master/Instructions/Media/match-mode-sensitive-info-type.png)](https://raw.githubusercontent.com/riswinto/SC-400T00A-Microsoft-Information-Protection-Administrator/master/Instructions/Media/match-mode-sensitive-info-type.png)
    
- [ ] On the **Choose a sensitive info type for "EmployeeID"** flyout panel on the right, in the search bar, search for `Contoso`.
- [ ] The **Contoso Employee IDs** sensitive info type created in a previous task should be displayed. Select the checkbox to the left of this sensitive info type, then select **Save**.
- [ ] Back on the **Select primary elements** page, select the checkbox to the right of **EmployeeID** to identify this field as a **Primary element**.
    
    [![](https://raw.githubusercontent.com/riswinto/SC-400T00A-Microsoft-Information-Protection-Administrator/master/Instructions/Media/employee-id-primary-element.png)](https://raw.githubusercontent.com/riswinto/SC-400T00A-Microsoft-Information-Protection-Administrator/master/Instructions/Media/employee-id-primary-element.png)
    
- [ ] Select **Next**.
- [ ] On the **Configure settings for data in selected columns**, ensure the toggle is set to **Yes** for **Use the same settings for all columns**.
- [ ] Select the checkbox for **Ignore delimiters and punctuation for data in all columns**.
- [ ] Select the dropdown for **Choose delimiters and punctuation to ignore** dropdown and select _Hyphen_, _Period_, _Space_, _Open parenthesis_ and _Close parenthesis_, then select **Next**.
- [ ] On the **Configure detection rules for primary elements**, leave the default configuration, then select **Next**.
- [ ] On the **Review settings and finish** page, select **Submit**.
- [ ] On the **You successfully created an EDM classifier** page, be sure to copy and paste the **Schema name** to use in the next task.
    
    [![](https://raw.githubusercontent.com/riswinto/SC-400T00A-Microsoft-Information-Protection-Administrator/master/Instructions/Media/edm-copy-schema-name.png)](https://raw.githubusercontent.com/riswinto/SC-400T00A-Microsoft-Information-Protection-Administrator/master/Instructions/Media/edm-copy-schema-name.png)
    
- [ ] Once you've captured the schema name, select **Done**.
- [ ] Leave the browser open with the Microsoft Purview portal.

You have successfully created a new EDM-based classification sensitive information type for identifying employee data from a database file source.

## Task 3 – Create EDM-based classification data source

In this task, you'll hash and upload the actual data for the EDM-based classification sensitive information type via the EDM Upload Agent tool.

- [ ] You should still be logged into Client 1 VM (SC-400-CL1) as the **SC-400-CL1\admin** account, and you should be logged into Microsoft 365 as **Joni Sherman**.
- [ ] In **Microsoft Edge**, navigate to `**https://go.microsoft.com/fwlink/?linkid=2088639**` to download the EDM upload agent.
- [ ] Once the download is complete, select **Open file** in the Microsoft Edge browser window to open the **Microsoft Exact Data Match Upload Agent Setup** wizard.
- [ ] On the **Welcome to the Microsoft Exact Data Match Upload Agent Setup Wizard** page, select **Next**.
- [ ] On the **End-User License Agreement** page, select the **I accept the terms in the License Agreement** checkbox, then select **Next**.
- [ ] On the **Destination Folder** page, don't change the default destination path, then select **Next**.
- [ ] On the **Ready to install Microsoft Exact Data Match Upload Agent** page, select **Install**.
- [ ] If the **User Account Control** window pops up, select **Yes** to allow this application to make changes to your device.
- [ ] When the installation finishes, select **Finish** on the **Completed the Microsoft Exact Data Match Upload Agent Setup Wizard** page.
- [ ] In your task bar, search for `Notepad` in the search field. Select the **Notepad** app from the **Best match** section of the search.
- [ ] In Notepad, enter:
    
    ```Plain
    text
    Name,Birthdate,StreetAddress,EmployeeID
    Joni Sherman,01.06.1980,1 Main Street,CSO123456
    Lynne Robbins,31.01.1985,2 Secondary Street,CSO654321
    ```
    
- [ ] In Notepad, select **File** and **Save As** to save the file.
- [ ] Select **Documents** from the left side pane and enter `EmployeeData.csv` as the **File name**, then select **Save**.
- [ ] Close the Notepad window.
- [ ] right click the Windows symbol in the task bar and select **Terminal (Admin)**.
- [ ] If the **User Account Control** window pops up, select **Yes** to allow this application to make changes to your device.
- [ ] In the terminal window, navigate to the EDM Upload Agent directory:
    
    ```PowerShell
    powershell
    cd "C:\Program Files\Microsoft\EdmUploadAgent"
    ```
    
- [ ] Authorize with your account to upload the database to your tenant by running this cmdlet:
    
    ```PowerShell
    powershell
    .\EdmUploadAgent.exe /Authorize
    ```
    
- [ ] When the **Pick an account** window is displayed, sign in as `JoniS@WWLx549660.onmicrosoft.com` Joni's password was set in a previous exercise.
- [ ] Back in the terminal window, download the database schema definition of the EDM-based classification sensitive information type by running this script in PowerShell. For the **DataStoreName**, this is where you'll use the schema name saved from the previous task.
    
    ```PowerShell
    powershell
    .\EdmUploadAgent.exe /SaveSchema /DataStoreName employeedbSchema /OutputDir "C:\Users\Admin\Documents\"
    ```
    
    You should get a message that the command completed successfully.
    
    > Note: If the last command fails, it possibly takes more time until the EDM_DataUploaders group membership is applied. It can take up to one hour until it is possible to download the schema file. If it fails proceed to the next task and return to this step later.
    
- [ ] Hash the database file and upload it to the EDM-based classification sensitive information type by running the following script in PowerShell:
    
    ```PowerShell
    powershell
    .\EdmUploadAgent.exe /UploadData /DataStoreName employeedbSchema /DataFile "C:\Users\Admin\Documents\EmployeeData.csv" /HashLocation "C:\Users\Admin\Documents\" /Schema "C:\Users\Admin\Documents\employeedbSchema.xml"
    ```
    
    You should get a message that the command completed successfully.
    
- [ ] Check the upload progress with this command:
    
    ```PowerShell
    powershell
    .\EdmUploadAgent.exe /GetSession /DataStoreName employeedbSchema
    ```
    
- [ ] In the terminal window, once the status is **Completed**, your EDM data is ready for use.
    
    Alternatively, you can also refresh the **EDM classifiers** window in the Microsoft Purview portal to check the status of the hash. Once the status is set to **Index complete** the hash is complete.
    
    > Note: This process time, and you might have to run the GetSession script or refresh the EDM classifiers page a few times before the status shows the hash is complete.
    
    [![](https://raw.githubusercontent.com/riswinto/SC-400T00A-Microsoft-Information-Protection-Administrator/master/Instructions/Media/edm-hash-completed.png)](https://raw.githubusercontent.com/riswinto/SC-400T00A-Microsoft-Information-Protection-Administrator/master/Instructions/Media/edm-hash-completed.png)
    
    [![](https://raw.githubusercontent.com/riswinto/SC-400T00A-Microsoft-Information-Protection-Administrator/master/Instructions/Media/edm-hash-completed-ui.png)](https://raw.githubusercontent.com/riswinto/SC-400T00A-Microsoft-Information-Protection-Administrator/master/Instructions/Media/edm-hash-completed-ui.png)
    
- [ ] Close the PowerShell window.

You have successfully hashed and uploaded a database file for an EDM-based classification sensitive information type.

## Task 4 – Create keyword dictionary

Several violations of personal information leakage happened when users sent out emails after colleagues reported on sick leave. When that happened the reason for illness or disease was sent out. We don't want that to happen. In this task, you'll create a keyword dictionary to prevent personal information leakage in emails.

- [ ] You should still be logged into Client 1 VM (SC-400-CL1) as the **SC-400-CL1\admin** account, and you should be logged into Microsoft 365 as **Joni Sherman**.
- [ ] The Microsoft Purview portal should still be to the EDM classifiers page in Microsoft Edge. If not, in Microsoft Edge, navigate to `https://purview.microsoft.com` > **Solutions** > **Information protection**.
- [ ] In the left sidebar, expand **Classifiers** then select **Sensitive info types**.
- [ ] Select **+ Create sensitive info type** to open the configuration for a new sensitive information type.
- [ ] On the **Name your sensitive info type** page, enter:
    - **Name**: `Contoso Diseases List`
    - **Description**: `List of possible diseases of employees`.
- [ ] Select **Next**.
- [ ] On the **Define patterns for this sensitive info type** page, select **+ Create pattern**.
- [ ] On the **New pattern** flyout panel on the right, under **Primary element** select **+ Add primary element**, then select **Keyword dictionary**.
- [ ] On the **Add a keyword dictionary** page enter:
    
    - **Name**: `Diseases Dictionary`
    - **Keywords**:
    
    ```Plain
    text
    flu
    influenza
    cold
    bronchitis
    otitis
    ```
    
- [ ] Select **Done** at the bottom of the flyout panel.
- [ ] Back on the **New pattern** page, under **Supporting elements**, select **+ Add supporting elements or group of elements**, then select **Keyword list** to add additional support for the keyword dictionary.
- [ ] On the **Add a keyword list** page enter:
    
    - **ID**: `Employee absence`
    - **Case insensitive**:
    
    ```Plain
    text
    employee
    absence
    reason
    ```
    
- [ ] Select **Done** at the bottom of the flyout panel.
- [ ] Back on the **New pattern** page, review the configuration and select **Create**.
- [ ] Back on the **Define patterns for this sensitive info type** select **Next**.
- [ ] On the **Choose the recommended confidence level to show in compliance policies**, leave the default value, then select **Next**.
- [ ] On the **Review settings and finish** page, review your settings and select **Create**. Once your sensitive info type is created, select **Done** on the **Your sensitive info type is created** page.
- [ ] Leave the browser window in the Microsoft Purview portal open.

You have successfully created a new sensitive information type based on a keyword dictionary and added more keywords to decrease the false positive rate.

## Task 5 – Test custom sensitive information types

Custom sensitive information types should always be tested before using them in policies otherwise data loss or leakage may occur due to a malfunctioning custom search pattern. In this task, you'll test the custom sensitive information types to ensure they recognize the desired patterns.

- [ ] You should still be logged into Client 1 VM (SC-400-CL1) as the **SC-400-CL1\admin** account, and you should be logged into Microsoft 365 as **Joni Sherman**.
- [ ] In your task bar, search for `Notepad` in the search field. Select the **Notepad** app from the **Best match** section of the search.
- [ ] In Notepad, enter:
    
    ```Plain
    text
    Employee Joni Sherman EMP123456 is absent because of the flu/influenza.
    ```
    
- [ ] Select **File** > **Save As**.
- [ ] Select **Documents** on the left side pane and enter `SickTestData` as the **File name**, then select **Save**.
- [ ] Close the Notepad window.
- [ ] Back in **Microsoft Edge**, Microsoft Purview portal should still be open on the Sensitive info types page.
- [ ] In the **Search** bar on the upper right, enter `Contoso` and press Enter.
- [ ] Select **Contoso Employee IDs**.
- [ ] Select **Test**.
- [ ] On the **Upload file to test "Contoso Employee IDs"** flyout panel on the right, select **Upload file**.
- [ ] Select **Documents** from the left pane, select the _SickTestData.txt_ file, then select **Open**.
- [ ] Select **Test** to start the analysis.
- [ ] On the **Match results** page, review the matches, then select **Finish** to end the test.
- [ ] Navigate back to **Sensitive info types** and search for `Contoso` again.
- [ ] This time select the **Contoso Diseases List** sensitive info type, then select **Test**.
- [ ] On the **Upload file to test "Contoso Diseases List"** flyout panel on the right, select **Upload file**.
- [ ] On the **Upload file to test** pane, select **Upload file**.
- [ ] Select **Documents** from the left pane, select the _SickTestData.txt_ file, then select **Open**.
- [ ] Select **Test** to start the analysis.
- [ ] On the **Match results** page, review the matches, then select **Finish** to end the test.

You have successfully tested the two custom sensitive information types and validated the search pattern recognizes the desired patterns.

# Lab 1 - Exercise 3 - Manage Microsoft Purview Message Encryption

To ensure secure communication within Contoso Ltd., you need to configure and test Microsoft Purview Message Encryption. This includes modifying the default template and creating a new branding template for the finance department.

**Tasks**:

- [ ] Verify Azure RMS functionality
- [ ] Modify default branding template
- [ ] Test default branding template
- [ ] Create custom branding template
- [ ] Test the custom branding template

## Task 1 – Verify Azure RMS functionality

In this task, you'll verify the correct Azure RMS functionality of your tenant.

- [ ] You should still be logged into Client 1 VM (SC-400-CL1) as the **SC-400-CL1\admin** account.
- [ ] Open an elevated PowerShell window by right clicking the Windows button in the task bar, then select **Terminal (Admin)**.
- [ ] Confirm the **User Account Control** window with **Yes**.
- [ ] Run the **Install-Module** cmdlet in the terminal window to install the latest Exchange Online PowerShell module version:
    
    ```PowerShell
    powershell
    Install-Module ExchangeOnlineManagement
    ```
    
- [ ] Confirm the NuGet provider security dialog with **Y** for Yes and press **Enter**. This process might take some time to complete.
- [ ] Confirm the Untrusted repository security dialog with **Y** for Yes and press **Enter**. This process may take some time to complete.
- [ ] Run the **Set-ExecutionPolicy** cmdlet to change your execution policy and press **Enter**
    
    ```PowerShell
    powershell
    Set-ExecutionPolicy -ExecutionPolicy RemoteSigned -Scope CurrentUser
    ```
    
- [ ] Close the PowerShell window.
- [ ] Open a regular PowerShell window, without elevation, right clicking the Windows button in the task bar, then select **Terminal**.
- [ ] Run the **Connect-ExchangeOnline** cmdlet to use the Exchange Online PowerShell module and connect to your tenant:
    
    ```PowerShell
    powershell
    Connect-ExchangeOnline
    ```
    
- [ ] When the **Sign in** window is displayed, sign in as `JoniS@WWLx549660.onmicrosoft.com` You will use the password you reset Joni's to in a previous lab.
- [ ] Run the **Get-IRMConfiguration** cmdlet to verify Azure RMS and IRM is activated in your tenant:
    
    ```PowerShell
    powershell
    Get-IRMConfiguration | fl AzureRMSLicensingEnabled
    ```
    
    The **AzureRMSLicensingEnabled** result should be **True**.
    
- [ ] Run the **Test-IRMConfiguration** cmdlet to test the Azure RMS templates used for Office 365 Message Encryption with user **Megan Bowen**:
    
    ```PowerShell
    powershell
    Test-IRMConfiguration -Sender MeganB@contoso.com -Recipient MeganB@contoso.com
    ```
    
    [![](https://raw.githubusercontent.com/riswinto/SC-400T00A-Microsoft-Information-Protection-Administrator/master/Instructions/Media/irm-validation.png)](https://raw.githubusercontent.com/riswinto/SC-400T00A-Microsoft-Information-Protection-Administrator/master/Instructions/Media/irm-validation.png)
    
    Verify all tests are in the status PASS and no errors are shown.
    
- [ ] Leave the PowerShell window open.

You have successfully installed the Exchange Online PowerShell module, connected to your tenant, and verified the correct functionality of Azure RMS.

## Task 2 – Modify default branding template

There is a requirement in your organization to restrict trust for foreign identity providers, such as Google or Facebook. Because these social IDs are activated by default for accessing messages protected with message encryption, you need to deactivate the use of social IDs for all users in your organization.

- [ ] You should still be logged into your Client 1 VM (SC-400-CL1) as the **SC-400-CL1\admin** account and there should still be an open PowerShell window with Exchange Online connected.
- [ ] Run the **Get-OMEConfiguration** cmdlet to view the default configuration:
    
    ```PowerShell
    powershell
    Get-OMEConfiguration -Identity "OME Configuration" | fl
    ```
    
    Review the settings and confirm that the SocialIdSignIn is set to **True**.
    
    [![](https://raw.githubusercontent.com/riswinto/SC-400T00A-Microsoft-Information-Protection-Administrator/master/Instructions/Media/socialidsignin-value-true.png)](https://raw.githubusercontent.com/riswinto/SC-400T00A-Microsoft-Information-Protection-Administrator/master/Instructions/Media/socialidsignin-value-true.png)
    
- [ ] Run the **Set-OMEConfiguration** cmdlet to restrict the use of social IDs for accessing messages from your tenant protected with OME:
    
    ```PowerShell
    powershell
    Set-OMEConfiguration -Identity "OME Configuration" -SocialIdSignIn:$false
    ```
    
- [ ] Confirm the warning message for customizing the default template by entering **Y** for Yes then press **Enter**.
- [ ] Run the **Get-OMEConfiguration** cmdlet to check the default configuration again and validate:
    
    ```PowerShell
    powershell
    Get-OMEConfiguration -Identity "OME Configuration" | fl
    ```
    
    [![](https://raw.githubusercontent.com/riswinto/SC-400T00A-Microsoft-Information-Protection-Administrator/master/Instructions/Media/socialidsignin-value-false.png)](https://raw.githubusercontent.com/riswinto/SC-400T00A-Microsoft-Information-Protection-Administrator/master/Instructions/Media/socialidsignin-value-false.png)
    
    Notice the result should show the SocialIDSignIn is set to **False**. Leave the PowerShell window and client open.
    

You have successfully deactivated the usage of foreign identity providers, such as Google and Facebook in Office 365 Message Encryption.

## Task 3 – Test default branding template

You must confirm that no social IDs dialog is displayed for external recipients when receiving a message protected with Office 365 Message Encryption from users of your tenant and they need to use the OTP at any time accessing the encrypted content.

- [ ] You should still be logged into your Client 1 VM (SC-400-CL1) as the **SC-400-CL1\admin**.
- [ ] Open **Microsoft Edge** in an InPrivate window by right clicking Microsoft Edge from the task bar and selecting **New InPrivate window**.
- [ ] Navigate to `**https://outlook.office.com**` and log into Outlook on the web as `LynneR@WWLx549660.onmicrosoft.com` Lynne's password was set in a previous exercise.
- [ ] On the **Stay signed in?** dialog box, select the checkbox for **Don't show this again** then select **No**.
- [ ] In Outlook on the web, select **New mail**.
- [ ] In the **To** line enter your personal or other third-party email address that isn't in the tenant domain. Enter `**Secret Message**` in the subject line and `**My super-secret message.**` in the body of the email.
- [ ] From the top pane, select **Options** then **Encrypt** to encrypt the message. Once you've successfully encrypted the message, you should see a notice that says "Encrypt: This message is encrypted. Recipients can't remove encryption."
    
    [![](https://raw.githubusercontent.com/riswinto/SC-400T00A-Microsoft-Information-Protection-Administrator/master/Instructions/Media/OptionsEncrypt.png)](https://raw.githubusercontent.com/riswinto/SC-400T00A-Microsoft-Information-Protection-Administrator/master/Instructions/Media/OptionsEncrypt.png)
    
- [ ] Select **Send** to send the message. Leave the Outlook window open.
- [ ] Sign into your personal email account in a new window and open the message from Lynne Robbins. If you sent this email to a Microsoft account (like @outlook.com) the encryption might be processed automatically, and you'll see the message automatically. If you sent the email to another email service like (@gmail.com), you might have to perform the next steps to process the encryption and read the message.
    
    > Note: You might need to check your junk or spam folder for the message from Lynne Robbins.
    
- [ ] Select **Read the message**.
- [ ] Without having social IDs activated, there is no button to authenticate with your non-Microsoft account.
- [ ] Select **Sign in with a One-time passcode** to receive a limited time passcode.
- [ ] Go to your personal email portal and open the message with subject **Your one-time passcode to view the message**.
- [ ] Copy the passcode, paste it into the OME portal and select **Continue**.
- [ ] Review the encrypted message.

You have successfully tested the modified default OME template with deactivated social IDs.

## Task 4 – Create custom branding template

Protected messages sent by your organizations finance department require special branding, including customized introduction and body texts and a Disclaimer link in the footer. The finance messages shall also expire after seven days. In this task, you will create a new custom OME configuration and create a transport rule to apply the OME configuration to all mail sent from the finance department.

- [ ] You should still be logged into your Client 1 VM (SC-400-CL1) as the **SC-400-CL1\admin**, and there should still be an open PowerShell window with Exchange Online connected.
- [ ] Run the **New-OMEConfiguration** cmdlet to create a new configuration:
    
    ```PowerShell
    powershell
    New-OMEConfiguration -Identity "Finance Department" -ExternalMailExpiryInDays 7
    ```
    
- [ ] Confirm the warning message for customizing the template with **Y** for Yes and press **Enter**.
- [ ] Run the **Set-OMEConfiguration** cmdlet with the _IntroductionText_ parameter to change the introduction text:
    
    ```PowerShell
    powershell
    Set-OMEConfiguration -Identity "Finance Department" -IntroductionText " from Contoso Ltd. finance department has sent you a secure message."
    ```
    
- [ ] Confirm the warning message for customizing the template with **Y** for Yes and press **Enter**.
- [ ] Run the **Set-OMEConfiguration** cmdlet with the _EmailText_ parameter to change the body email text:
    
    ```PowerShell
    powershell
    Set-OMEConfiguration -Identity "Finance Department" -EmailText "Encrypted message sent from Contoso Ltd. finance department. Handle the content responsibly."
    ```
    
- [ ] Confirm the warning message for customizing the template with **Y** for Yes and press **Enter**.
- [ ] Run the **Set-OMEConfiguration** cmdlet with the _PrivacyStatementURL_ parameter to change the disclaimer URL to point to Contoso's privacy statement site:
    
    ```PowerShell
    powershell
    Set-OMEConfiguration -Identity "Finance Department" -PrivacyStatementURL "https://contoso.com/privacystatement.html"
    ```
    
- [ ] Confirm the warning message for customizing the template with **Y** for Yes and press **Enter**.
- [ ] Run the **TransportRule** cmdlet to create a mail flow rule, which applies the custom OME template to all messages sent from the finance team. This process might take a few seconds to complete.
    
    ```PowerShell
    powershell
    New-TransportRule -Name "Encrypt all mails from Finance team" -FromScope InOrganization -FromMemberOf "Finance Team" -ApplyRightsProtectionCustomizationTemplate "Finance Department" -ApplyRightsProtectionTemplate Encrypt
    ```
    
- [ ] Run the **Get-OMEConfiguration** cmdlet to verify changes.
    
    ```PowerShell
    powershell
    Get-OMEConfiguration -Identity "Finance Department" | Format-List
    ```
    
- [ ] Close the PowerShell window after reviewing the results

You have successfully created a new transport rule that applies the custom branding template automatically, when a member of the finance department sends a message to external recipients.

## Task 5 – Test the custom branding template

To validate the new custom configuration, you need to use the account of Lynne Robbins again, who is a member of the finance team.

- [ ] Go back to **Microsoft Edge** with the InPrivate Outlook on the web window where you should still be logged in as **Lynne Robbins**.
- [ ] Select **New mail** from the upper left side part of Outlook on the web.
- [ ] In the **To** line enter your personal or other third-party email address that isn't in the tenant domain. Enter `**Finance Report**` in the subject line and enter `**Secret finance information.**` in the body of the email.
- [ ] Select **Send** to send the message, then close the InPrivate window where you're logged in as Lynne.
- [ ] Sign into your personal email account and open the message from Lynne Robbins.
- [ ] You should see a message from Lynne Robbins that looks like the image below. Select **Read the message**.
    
    [![](https://raw.githubusercontent.com/riswinto/SC-400T00A-Microsoft-Information-Protection-Administrator/master/Instructions/Media/EncryptedEmail.png)](https://raw.githubusercontent.com/riswinto/SC-400T00A-Microsoft-Information-Protection-Administrator/master/Instructions/Media/EncryptedEmail.png)
    
- [ ] The customized configuration has social IDs activated, because both options are available. Select **Sign in with a One-time passcode** to receive a limited time passcode.
- [ ] Go to your personal email portal and open the message with subject **Your one-time passcode to view the message**.
- [ ] Copy the passcode, paste it into the portal and select **Continue**.
- [ ] Review the encrypted message with custom branding. Close the window with your email account open.

You have successfully tested the new customized template.

# Lab 1 - Exercise 4 - Manage sensitivity labels

Joni Sherman, the System Administrator for Contoso Ltd., is implementing a sensitivity labeling plan to ensure that all employee documents in the HR department are appropriately labeled according to the company's information protection policies. Contoso Ltd. is based in Rednitzhembach, Germany, and aims to comply with internal data handling standards and regional regulations.

**Tasks**:

- [ ] Enable support for sensitivity labels
- [ ] Create sensitivity labels
- [ ] Publish sensitivity labels
- [ ] Apply sensitivity labels
- [ ] Configure auto labeling

## Task 1 – Enable support for sensitivity labels

In this task, you'll install the necessary modules and enable support for sensitivity labels on your tenant.

- [ ] You should still be logged into Client 1 VM (SC-400-CL1) as the **SC-400-CL1\admin** account.
- [ ] Open an elevated PowerShell window by right clicking the Windows button in the task bar, then select **Terminal (Admin)**.
- [ ] Confirm the **User Account Control** window with **Yes** and press Enter.
- [ ] Run the **Install-Module** cmdlet to install the latest MS Online PowerShell module version:
    
    ```PowerShell
    powershell
    Install-Module -Name MSOnline
    ```
    
- [ ] Confirm the Nuget security dialog and the Untrusted repository security dialog with **Y** for Yes and press Enter. This might take a while to complete processing.
- [ ] Run the **Install-Module** cmdlet to install the latest SharePoint Online PowerShell module version:
    
    ```PowerShell
    powershell
    Install-Module -Name Microsoft.Online.SharePoint.PowerShell
    ```
    
- [ ] Confirm the Untrusted repository security dialog with **Y** for Yes and press Enter.
- [ ] Run the **Connect-MsolService** to connect to the MS Online service:
    
    ```PowerShell
    powershell
    Connect-MsolService
    ```
    
- [ ] In the **Sign into your account** form, sign in as **Joni Sherman** `JoniS@WWLx549660.onmicrosoft.com` Joni's password was set in a previous exercise.
- [ ] After signing in, navigate back to the terminal window.
- [ ] Run the **Get-Msoldomain** cmdlet and save the domain as a variable:
    
    ```PowerShell
    powershell
    $domain = get-msoldomain
    ```
    
- [ ] Use the _$domain_ variable created in the previous step to create a new variable for _$adminurl_:
    
    ```PowerShell
    powershell
    $adminurl = "https://" + $domain.Name.split('.')[0] + "-admin.sharepoint.com"
    ```
    
- [ ] Run the **Connect-SPOService** cmdlet using the _$adminurl_ variable created in the previous step:
    
    ```PowerShell
    powershell
    Connect-SPOService -url $adminurl
    ```
    
- [ ] In the **Sign into your account** form, sign in as **MOD Administrator**. `admin@WWLx549660.onmicrosoft.com` Admin's password should be provided by your lab hosting provider.
- [ ] After signing in, navigate back to the terminal window.
- [ ] Run the **Set-SPOTenant** cmdlet to enable support for sensitivity labels:
    
    ```PowerShell
    powershell
    Set-SPOTenant -EnableAIPIntegration $true
    ```
    
- [ ] Confirm the changes with **Y** for Yes and press Enter.
- [ ] Close the PowerShell window.

You have successfully enabled support for sensitivity labels for Teams and SharePoint sites.

## Task 2 – Create sensitivity labels

In this task, your HR department has requested a sensitivity label to apply to HR employee documents. You'll create a sensitivity label for internal documents and a sublabel for the HR department.

- [ ] You should still be logged into Client 1 VM (SC-400-CL1) as the **SC-400-cl1\admin** account.
- [ ] Open **Microsoft Edge** and navigate to `**https://purview.microsoft.com**`. Log into Microsoft Purview as **Joni Sherman** `JoniS@WWLx549660.onmicrosoft.com` Joni's password was set in a previous exercise.
- [ ] In the Microsoft Purview portal, select **Solutions** from the left sidebar, then select **Information Protection**.
- [ ] On the **Microsoft Information Protection** page, on the left sidebar, select **Sensitivity labels**.
- [ ] On the **Sensitivity labels** page select **+ Create a label**.
- [ ] The **New sensitivity label** configuration will start. On the **Provide basic details for this label**, enter:
    - **Name**: `Internal`
    - **Display name**: `Internal`
    - **Description for users**: `Internal sensitivity label.`
    - **Description for admins**: `Internal sensitivity label for Contoso.`
- [ ] Select **Next**.
- [ ] On the **Define the scope for this label** page, select **Items**, then select **Files** and **Emails**. If the checkbox for **Meetings** is selected, make sure it's deselected.
- [ ] Select **Next**.
- [ ] On the **Choose protection settings for labeled items** page, select **Next**.
- [ ] On the **Auto-labeling for files and emails** page, select **Next**.
- [ ] On the **Define protection settings for groups and sites** page, select **Next**.
- [ ] On the **Auto-labeling for schematized data assets (preview)** page, select **Next**.
- [ ] On the **Review your settings and finish** page, select **Create label**.
- [ ] On the **Your sensitivity label was created** page, select **Don't create a policy yet**, then select **Done**.
- [ ] On the **Sensitivity labels** page, find the newly created **Internal** sensitivity label. Select the vertical ellipsis (**…**) next to it, then select **+ Create sublabel** from the dropdown menu.
    
    [![](https://raw.githubusercontent.com/riswinto/SC-400T00A-Microsoft-Information-Protection-Administrator/master/Instructions/Media/create-sublabel-button.png)](https://raw.githubusercontent.com/riswinto/SC-400T00A-Microsoft-Information-Protection-Administrator/master/Instructions/Media/create-sublabel-button.png)
    
- [ ] The **New sensitivity label** wizard will start. On the **Provide basic details for this label** page enter:
    - **Name**: `Employee data (HR)`
    - **Display name**: `Employee data (HR)`
    - **Description for users**: `This HR label is the default label for all specified documents in the HR Department.`
    - **Description for admins**: `This label is created in consultation with Ms. Jones (Head of HR department). Contact her, when you want to change settings of the label.`
- [ ] Select **Next**.
- [ ] On the **Define the scope for this label** page, select **Items**, then select **Files** and **Emails**. If the checkbox for **Meetings** is selected, make sure it's deselected.
- [ ] Select **Next**.
- [ ] On the **Choose protection settings for labeled items** page, select the **Control access** option, then select **Next**.
- [ ] On the **Access control** page, select **Configure access control settings**.
- [ ] Configure the encryption settings with these options:
    - **Assign permissions now or let users decide?**: Assign permissions now
    - **User access to content expires**: Never
    - **Allow offline access**: Only for a number of days
    - **Users have offline access to the content for this many days**: 15
    - Select the **Assign permissions** link. On the **Assign permissions** flyout panel, select the **+ Add any authenticated users**, then select **Save** to apply this setting.
- [ ] On the **Access control** page, select **Next**.
- [ ] On the **Auto-labeling for files and emails** page, select **Next**.
- [ ] On the **Define protection settings for groups and sites** page, select **Next**.
- [ ] On the **Auto-labeling for schematized data assets (preview)** page, select **Next**.
- [ ] On the **Review your settings and finish** page, select **Create label**.
- [ ] On the **Your sensitivity label was created** page, select **Don't create a policy yet**, then select **Done**.

You have successfully created a sensitivity label for your organizations internal policies and a sensitivity sublabel for the Human Resources (HR) department.

## Task 3 – Publish sensitivity labels

You will now publish the Internal and HR sensitivity label so that the published sensitivity labels will be available for the HR users to apply to their HR documents.

- [ ] You should still be logged into Client 1 VM (SC-400-CL1) as the **SC-400-cl1\admin** account, and you should be logged into Microsoft Purview as **Joni Sherman**.
- [ ] In **Microsoft Edge**, the Microsoft Purview portal tab should still be open. If not, navigate to `**https://purview.microsoft.com**` > **Solutions** > **Information Protection** > **Sensitivity labels**.
- [ ] On the **Sensitivity labels** page select **Publish label**.
- [ ] The publish sensitivity labels configuration will start.
- [ ] On the **Choose sensitivity labels to publish** page, select the **Choose sensitivity labels to publish** link.
- [ ] On the **Sensitivity labels to publish** flyout panel, select the **Internal** and **Internal/Employee Data (HR)** checkboxes, then select **Add** at the bottom of the flyout panel.
- [ ] Back on the **Choose sensitivity labels to publish** page, select **Next**.
- [ ] On the **Assign admin units** page, select **Next**
- [ ] On the **Publish to users and groups** page, select **Next**.
- [ ] On the **Policy settings** page, select **Next**.
- [ ] On the **Default settings for documents** select **Next**.
- [ ] On the **Default settings for emails** select **Next**.
- [ ] On the **Default settings for meetings and calendar events** select **Next**.
- [ ] On the **Default settings for Power BI Content** select **Next**.
- [ ] On the **Name your policy** page, enter:
    - **Name**: `Internal HR employee data`
    - **Enter a description for your sensitivity label policy**: `This HR label is to be applied to internal HR employee data.`
- [ ] Select **Next**.
- [ ] On the **Review and finish** page, select **Submit**.
- [ ] On the **New policy created**, select **Done** to finish publishing your label policy.

You have successfully published the Internal and HR sensitivity labels. Note that it can take up to 24 hours for changes to replicate to all users and services.

## Task 4 – Apply sensitivity labels

In this task, you will create sensitivity labels in Word and Outlook emails. The document created will be stored in OneDrive and sent to an HR employee via email.

- [ ] You should still be logged into Client 1 VM (SC-400-CL1) as the **SC-400-cl1\admin** account, and you should be logged into Microsoft 365 as **Joni Sherman** `JoniS@WWLx549660.onmicrosoft.com` Joni's password was set in a previous exercise.
- [ ] In **Microsoft Edge**, open a new Word document by selecting the meatball menu in the top left and selecting **Word**.
    
    [![](https://raw.githubusercontent.com/riswinto/SC-400T00A-Microsoft-Information-Protection-Administrator/master/Instructions/Media/meatball-menu-word.png)](https://raw.githubusercontent.com/riswinto/SC-400T00A-Microsoft-Information-Protection-Administrator/master/Instructions/Media/meatball-menu-word.png)
    
- [ ] Select **Blank document** to create a new document.
- [ ] On the **Your privacy option** dialogue, select **Close**.
- [ ] Enter this text in the new blank document:
    
    `Important HR employee document.`
    
- [ ] Select **Sensitivity** from the navigation ribbon and select **Internal** > **Employee Data (HR)** to apply the newly created sensitivity label to this document.
    
    [![](https://raw.githubusercontent.com/riswinto/SC-400T00A-Microsoft-Information-Protection-Administrator/master/Instructions/Media/word_label.png)](https://raw.githubusercontent.com/riswinto/SC-400T00A-Microsoft-Information-Protection-Administrator/master/Instructions/Media/word_label.png)
    
    > Note: It can take 24-48 hours for newly published sensitivity labels to be available for application. If the newly created sensitivity labels aren't available, you can use Confidential > All Employees for this exercise.
    
- [ ] In the upper left of the document, select **Document** to rename this file, and rename it to `**HR Document**`. Press enter to apply this name change.
    
    [![](https://raw.githubusercontent.com/riswinto/SC-400T00A-Microsoft-Information-Protection-Administrator/master/Instructions/Media/rename-web-word-file.png)](https://raw.githubusercontent.com/riswinto/SC-400T00A-Microsoft-Information-Protection-Administrator/master/Instructions/Media/rename-web-word-file.png)
    
- [ ] Close the tab to return to the Word Online tab. Select the meatball menu on the top left and select **Outlook** to open Outlook on the web.
- [ ] In Outlook on the web, select **New mail**.
- [ ] In the **To** field enter the name: `**Allan**` and select **Allan Deyoung** from the drop-down list.
- [ ] In the subject line, enter: `**Employee data for HR**`
- [ ] In the body of the email, enter:
    
    ```Plain
    text
    Dear Mr. Deyoung,
    
    Please find attached the important HR employee document.
    
    Kind regards,
    
    Joni Sherman
    ```
    
- [ ] Select the paperclip symbol from the top navigation ribbon to add an attachment. Under **Suggested files** select **HR Document.docx**.
- [ ] Select **Send** to send out the email message with attached document.

You have successfully created an HR Word document with a sensitivity label, which was saved onto your OneDrive. You then emailed to document to an HR staff member where the email was also set with a sensitivity label.

## Task 5 – Configure auto labeling

In this task, you'll create a sensitivity label that will auto label documents and emails found to contain information related to the European General Data Protection Regulation (GPDR).

- [ ] You should still be logged into Client 1 VM (SC-400-CL1) as the **SC-400-cl1\admin** account.
- [ ] In **Microsoft Edge**, navigate to `**https://purview.microsoft.com**` and log into the Microsoft Purview portal as **Joni Sherman**.
- [ ] In the Microsoft Purview portal, select **Solutions** from the left side bar, then select **Information protection**. Select **Sensitivity labels**.
- [ ] On the **Sensitivity labels** page, find the newly created **Internal** sensitivity label. Select the vertical ellipsis (**…**) next to it, then select **+ Create sublabel** from the dropdown menu.
- [ ] The **New sensitivity label** configuration will start. On the **Provide basic details for this label** page, enter:
    - **Name**: `GDPR Germany`
    - **Display name**: `GDPR Germany`
    - **Description for users**: `This document or email contains data related to the European General Data Protection Regulation (GPDR) for the region Germany.`
    - **Description for admins**: `This label is auto applied to German GDPR documents.`
- [ ] Select **Next**.
- [ ] On the **Define the scope for this label** page, select **Items**, then select **Files** and **Emails**. If the checkbox for **Meetings** is selected, make sure it's deselected.
- [ ] Select **Next**.
- [ ] On the **Choose protection settings for labeled items** page, select **Next**.
- [ ] On the **Auto-labeling for files and emails** page, set the **Auto-labeling for files and emails** to enabled.
- [ ] In the **Detect content that matches these conditions** section, select **+ Add condition** > **Content contains**.
- [ ] In **Content contains** section select the **Add** > **Sensitive info types**.
- [ ] In the **Sensitive info types** flyout panel, search for `German` to display sensitive info types related to Germany.
- [ ] Select the checkbox next to the **Name** field to select all sensitive info types related to German, then select **Add**.
    
    [![](https://raw.githubusercontent.com/riswinto/SC-400T00A-Microsoft-Information-Protection-Administrator/master/Instructions/Media/select-all-german-types.png)](https://raw.githubusercontent.com/riswinto/SC-400T00A-Microsoft-Information-Protection-Administrator/master/Instructions/Media/select-all-german-types.png)
    
- [ ] Back on the **Auto-labeling for files and emails** page, select **Next**.
- [ ] On the **Define protection settings for groups and sites** page, select **Next**.
- [ ] On the **Auto-labeling for schematized data assets (preview)** page, select **Next**.
- [ ] On the **Review your settings and finish** page, select **Create label**.
- [ ] On the **Your sensitivity label was created** page, select **Publish label to users' apps**, then select **Done**.
- [ ] On the **Create auto-labeling policy** flyout panel, select **Review policy** to start the configuration to create a new label policy.
- [ ] On the **Name your auto-labeling policy** page, enter:
    - **Name**: `GDPR Germany policy`
    - **Enter a description for your sensitivity label policy**: `This auto apply sensitivity labels policy is for the GDPR region of Germany.`
- [ ] Select **Next**.
- [ ] On the **Assign admin units** page, select **Next**.
- [ ] On the **Choose locations where you want to apply the label** page, leave the defaults selected, then select **Next**.
- [ ] On the **Set up common or advanced rules** page, select **Next**.
- [ ] On the **Define rules for content in all locations** page, select **Next**.
- [ ] On the **Decide if you want to test out the policy now or later** select **Run policy in simulation mode**, then select the checkbox for **Automatically turn on policy if not modified for 7 days in simulation.**, then select **Next**.
- [ ] On the **Review and finish** page, select **Create policy**.
- [ ] On the **Your auto-labeling policy was created** page, select **Done**.

You have successfully created and published an auto apply sensitivity label for GDPR documents in the region Germany.

It can take up to 24 hours for auto applied sensitivity labels to be applied. This duration will be longer when applied to more than 25,000 documents (that is, the daily limit).

  

# Lab 2 – Exercise 1 – Manage DLP Policies

You are Joni Sherman, the newly hired Compliance Administrator for Contoso Ltd. tasked to configure the company's Microsoft 365 tenant for data loss prevention. Contoso Ltd. is a company that offers driving instruction in the United States, and you need to make sure that sensitive customer information does not leave the organization.

**Tasks**:

- [ ] Create a DLP policy in simulation mode
- [ ] Modify a DLP policy
- [ ] Create a DLP policy in PowerShell
- [ ] Test your DLP policy
- [ ] Activate a policy in simulation mode
- [ ] Modify policy priority
- [ ] Enable file monitoring in Microsoft 365 Defender
- [ ] Create a file policy for Microsoft 365 Defender
- [ ] Create a DLP policy for Power Platform

## Task 1 – Create a DLP policy in simulation mode

In this exercise, you'll create a data loss prevention (DLP) policy to protect sensitive data from being shared by users. The DLP policy that you create will inform your users if they want to share content that contains credit card information and allow them to provide a justification for sending this information. The policy will be implemented in simulation mode because you don't want the block action to affect your users yet.

- [ ] Log into Client 1 VM (SC-400-CL1) as the **SC-400-CL1\admin** account.
- [ ] In **Microsoft Edge**, navigate to `**https://purview.microsoft.com**` and log into the Microsoft Purview portal as **Joni Sherman**. sign in as `JoniS@WWLx549660.onmicrosoft.com` Joni's password was set in a previous exercise.
- [ ] Select **Solutions** from the left sidebar, then select **Data Loss Prevention**.
- [ ] On the left sidebar, select **Policies**.
- [ ] On the **Policies** page, select **+ Create policy** to start the configuration for creating a new data loss prevention policy.
- [ ] On the **Start with a template or create a custom policy** page, select **Custom** as the category, then select **Custom policy** under **Regulations**.
- [ ] Select **Next**.
- [ ] On the **Name your DLP policy** page enter:
    - **Name**: `Credit Card DLP Policy`
    - **Description**: `Protect credit card numbers from being shared`
- [ ] Select **Next**.
- [ ] On the **Assign admin units** page select **Next**.
- [ ] On the **Choose locations to apply the policy** page, enable the location for **Teams chat and channel messages** only. If any other locations are selected, deselect them.
- [ ] Select **Next**.
- [ ] On the **Define policy settings** page, select **Create or customize advanced DLP rules**, then select **Next**.
- [ ] On the **Customize advanced DLP rules** page, select **+ Create rule**.
- [ ] On the **Create rule** flyout page, enter `Credit card information` as name in the **Name** field.
- [ ] Under **Conditions**, select **+ Add Condition**, then select **Content contains**.
- [ ] In the new **Content contains** area, select **Add**, then select **Sensitive info types**.
- [ ] On the **Sensitive info types** page, select **Credit Card Number** then select **Add**.
- [ ] Select **+ Add condition**, then select **Content is shared from Microsoft 365**.
- [ ] In the new **Content is shared from Microsoft 365** section, select the **only with people inside my organization** option.
- [ ] Under **Actions** select **+ Add an action**, then select **Restrict access or encrypt the content in Microsoft 365 locations**.
- [ ] In the new **Restrict access or encrypt the content in Microsoft 365 locations** area select **Block everyone.**
- [ ] Under **User notifications**, turn **On** the option for **Use notifications to inform your users and help educate them on the proper use of sensitive info.**, then select the checkbox to **Notify users in Office 365 service with a policy tip**.
- [ ] Under **User overrides** select the checkbox to **Allow users to override policy restrictions Fabric (including Power BI), Exchange, SharePoint, OneDrive and Teams.**
- [ ] Select the checkbox to **Require a business justification to override**.
- [ ] Under **Incident reports**, in the **Use this severity level in admin alerts and reports** dropdown, select **Low**.
- [ ] At the bottom of the **Create rule** flyout panel, select **Save**.
- [ ] Back on the **Customize advanced DLP rules**, select **Next**.
- [ ] On the **Policy mode** page select **Run the policy in simulation mode** and select the checkbox for **Show policy tips while in simulation mode**.
- [ ] Select **Next**.
- [ ] On the **Review and finish** page review your settings then select **Submit**.
- [ ] On the **New policy created** page select **Done**.

You have now created a DLP policy that scans for credit card numbers in Microsoft Teams chats and channels, allowing users to provide a business justification to override the policy.

## Task 2 – Modify a DLP policy

In this task, you'll modify the existing DLP policy created in the previous task to also scan emails for credit card information. This modification ensures that sensitive data is protected across more communication channels.

- [ ] You should still be logged into Client 1 VM (SC-400-CL1) as the **SC-400-CL1\admin** account, and you should be logged into Microsoft 365 as **Joni Sherman**.
- [ ] You should still be on the **Policies** page in Microsoft Purview. If not, open **Microsoft Edge** and navigate to `https://purview.microsoft.com`. Select **Solutions** > **Data Loss Prevention** > **Policies**.
- [ ] On the **Policies** page select the checkbox for the recently created **Credit Card DLP Policy**, then select **Edit policy** to open the policy configuration.
- [ ] On the **Name your DLP policy** page, select **Next**.
- [ ] On the **Assign admin units** page select **Next**.
- [ ] On the **Choose locations to apply the policy** page, select the checkbox for **Exchange email** to add this location to your DLP policy.
- [ ] Select **Next** until you reach the **Review and finish** page.
- [ ] Select **Submit** on the **Review and finish** page to apply the change you made to the policy.
- [ ] Once the policy is updated select **Done** on the **Policy updated** page.

You have successfully modified the DLP policy to include email scanning, enhancing the protection of sensitive information.

## Task 3 – Create a DLP policy in PowerShell

In this task, you'll use PowerShell to create a DLP policy to protect Contoso employee IDs and prevent them from being shared via Exchange. This policy will notify users attempting to share this sensitive data and block the email if it contains Employee IDs.

- [ ] You should still be logged into Client 1 VM (SC-400-CL1) as the **SC-400-CL1\admin** account.
- [ ] Open an elevated PowerShell window by right clicking the Windows button in the task bar, then select **Terminal (Admin)**.
- [ ] Run the **Connect-IPPSSession** cmdlet to connect to the Security & Compliance PowerShell:

```PowerShell
powershell
   Connect-IPPSSession
```

- [ ] Sign in as **Joni Sherman** `JoniS@WWLx549660.onmicrosoft.com` (where ZZZZZZ is your unique tenant ID provided by your lab hosting provider) in the **Sign in to your account** pop-up window. Joni's password was set in a previous exercise.
- [ ] Run the **New-DlpCompliancePolicy** cmdlet to create a DLP policy that scans all Exchange mailboxes:

```PowerShell
powershell
   New-DlpCompliancePolicy -Name "EmployeeID DLP Policy" -Comment "This policy blocks sharing of Employee IDs" -ExchangeLocation All
```

- [ ] Run the **New-DlpComplianceRule** cmdlet to add a DLP rule to the DLP policy you created in the previous step:

```PowerShell
powershell
   New-DlpComplianceRule -Name "EmployeeID DLP rule" -Policy "EmployeeID DLP Policy" -BlockAccess $true -ContentContainsSensitiveInformation @{Name="Contoso Employee IDs"}
```

- [ ] Run the **Get-DLPComplianceRule** cmdlet to review the **EmployeeID DLP rule**:

```PowerShell
powershell
   Get-DLPComplianceRule -Identity "EmployeeID DLP rule"
```

You have successfully created a DLP policy using PowerShell that scans for Contoso Employee IDs in Exchange.

## Task 4 – Test your DLP Policy

In this task you'll test the DLP policy that was created in the previous task.

- [ ] You should still be logged into Client 1 VM (SC-400-CL1) as the **SC-400-CL1\admin** account and logged into Microsoft 365 as Joni Sherman.
- [ ] Open a Microsoft Edge browser window and navigate to `**https://outlook.office.com**`
- [ ] Select the **New mail** button on the top left to compose a new email message.
- [ ] In the **To** field, enter `Megan` and select **Megan Bowen**'s email address.
- [ ] In the subject field enter `Help with employee information`.
- [ ] In the body of the email enter:

```Plain
text
   Please help me with the start dates for the following employees:
   ABC123456
   DEF678901
   GHI234567

   Thank you,
   Joni Sherman
```

- [ ] Select the **Send** button in the upper right of the message window to send the email.
- [ ] You should receive a message that the email was undeliverable and blocked by a DLP policy.
    
    [![](https://raw.githubusercontent.com/riswinto/SC-400T00A-Microsoft-Information-Protection-Administrator/master/Instructions/Media/dlp-email-blocked.png)](https://raw.githubusercontent.com/riswinto/SC-400T00A-Microsoft-Information-Protection-Administrator/master/Instructions/Media/dlp-email-blocked.png)
    

You have successfully tested your DLP policy.

## Task 5 – Activate a policy in simulation mode

In this task, you'll activate the **Credit Card DLP Policy** you created in simulation mode so it enforces its protective actions.

- [ ] You should still be logged into Client 1 VM (SC-400-CL1) as the **SC-400-CL1\admin** account, and you should be logged into Microsoft 365 as **Joni Sherman**.
- [ ] In **Microsoft Edge**, navigate to DLP policies by going to `https://purview.microsoft.com` > **Solutions** > **Data Loss Prevention** then select **Policies** from the left sidebar.
- [ ] On the **Policies** page select the checkbox for the **Credit Card DLP Policy** and select **Edit policy** to open the policy configuration.
- [ ] Select **Next** until you reach the **Policy mode** page and select **Turn the policy on immediately**.
- [ ] On the **Review and finish** select **Submit**.
- [ ] On the **Policy updated** page select **Done**.

You have successfully activated the DLP policy, ensuring that any attempts to share credit card information are blocked and require a business justification.

## Task 6 – Modify policy priority

After creating two DLP policies, you want to make sure that the more restrictive policy is processed at a higher priority than the less restrictive policy. For this reason, you want to move the EmployeeID DLP Policy into the higher priority.

- [ ] You should still be logged into Client 1 VM (SC-400-CL1) as the **SC-400-CL1\admin** account, and you should be logged into Microsoft 365 as **Joni Sherman**.
- [ ] In **Microsoft Edge**, the Microsoft Purview portal tab should still be open to the **Policies** page. If not, open **Microsoft Edge** and navigate to `https://purview.microsoft.com`. Select **Solutions** > **Data Loss Prevention** > **Policies**.
- [ ] On the **Policies** page, select the **EmployeeID DLP Policy** DLP policy.
- [ ] Select **Reprioritize** from the top navigation ribbon, then select **Move to top (highest priority)**.
- [ ] In the **Data loss prevention** window, select **Refresh** and review the priority in the **Order** column of the policy table.

You have successfully modified the policy priority, ensuring that the most restrictive DLP policy is enforced first when matching content.

## Task 7 – Enable file monitoring in Microsoft 365 Defender

You want to use file policies in Microsoft 365 Defender to protect files in your OneDrive and SharePoint Online locations. Before you can create a file policy, you need to enable file monitoring so Microsoft 365 Defender can scan files in your organization.

- [ ] You should still be logged into Client 1 VM (SC-400-CL1) as the **SC-400-CL1\admin** account.
- [ ] In **Microsoft Edge**, the Microsoft Purview portal tab should still be open. Sign out of Joni's account by selecting the profile picture of Joni Sherman in the top right. Select **Sign out**, then close the browser window.
- [ ] Open **Microsoft Edge** and navigate to `**https://security.microsoft.com**` and log into the Microsoft 365 Defender portal as **MOD Administrator** `admin@WWLx549660.onmicrosoft.com` Admin's password should be provided by your lab hosting provider.
- [ ] On the left sidebar, expand **System** then select **Settings**.
- [ ] On the **Settings** page select **Cloud Apps**.
- [ ] In the left pane within the **Cloud apps** window, scroll down to the **Information Protection** section, then select **Files**.
- [ ] Select the **Enable file monitoring** checkbox then select **Save** if it's not already marked.

You successfully enabled file monitoring in Microsoft 365 Defender and can now scan files for sensitive content using file policies.

## Task 8 – Create a file policy for Microsoft 365 Defender

In this task, you'll create a file policy in Microsoft 365 Defender to scan files in OneDrive and SharePoint Online for credit card information. The policy will automatically quarantine files containing sensitive data

- [ ] You should still be logged into Client 1 VM (SC-400-CL1) as the **SC-400-CL1\admin** account.
- [ ] Sign out of the MOD Administrator account by selecting the **MA** icon in the top right, then selecting **Sign out**. Close the browser window once you're signed out.
- [ ] Open **Microsoft Edge** and navigate to `**https://security.microsoft.com**` and log into the Microsoft 365 Defender portal as **Joni Sherman** `JoniS@WWLx549660.onmicrosoft.com` Joni's password was set in a previous exercise.
- [ ] In the **Microsoft 365 Defender** portal, in the left navigation, scroll down to the **Cloud apps** section. Expand **Policies** then select **Policy management**.
- [ ] On the **Policies** page, select **+ Create policy**, then select **File policy**.
- [ ] On the **Create file policy** page, leave the **Policy template** selection as **No template**.
- [ ] In the **Policy name** and **Description** fields, enter:
    - **Policy name**: `Credit card information for files`
    - **Description**: `Protect credit card numbers from being shared in files.`
- [ ] Keep the **Policy Severity** set to **Low** (one lighted icon) and make sure the **Category** is set to **DLP**. For a file policy, this should be the default.
    
    [![](https://raw.githubusercontent.com/riswinto/SC-400T00A-Microsoft-Information-Protection-Administrator/master/Instructions/Media/policy-severity-low.png)](https://raw.githubusercontent.com/riswinto/SC-400T00A-Microsoft-Information-Protection-Administrator/master/Instructions/Media/policy-severity-low.png)
    
- [ ] In the **Files matching all of the following** area, expand the dropdown menu **Public (Internet), External, Public**, and add **Internal**.
    
    [![](https://raw.githubusercontent.com/riswinto/SC-400T00A-Microsoft-Information-Protection-Administrator/master/Instructions/Media/files-matching-internal.png)](https://raw.githubusercontent.com/riswinto/SC-400T00A-Microsoft-Information-Protection-Administrator/master/Instructions/Media/files-matching-internal.png)
    
- [ ] In the **Inspection method** dropdown menu, select **Data Classification Service**.
- [ ] In the **Choose inspection type…** dropdown menu, select **Sensitive information type…**.
- [ ] On the **Select a sensitive information type** dialog, search for `Credit card`, then select the checkbox for **Credit Card Number**.
- [ ] Select **Done** in the upper right corner of the **Select a sensitive information type** screen.
- [ ] Under **Alerts**, select the checkbox for **Create an alert for each matching file** and review your options. Keep the settings as the default by selecting **Save as default settings**.
- [ ] In the **Governance actions** section, expand **Microsoft OneDrive for Business** and select **Put in user quarantine**.
- [ ] In the **Governance actions** section, expand **Microsoft SharePoint Online** and select the checkbox for **Put in user quarantine**.
- [ ] Select **Create** at the bottom of the page to create the file policy.
- [ ] Sign out of Joni's account by selecting the profile picture of Joni Sherman in the top right. Select **Sign out**, then close the browser window.

You have successfully created a file policy that scans and quarantines files with credit card information in OneDrive and SharePoint.

## Task 9 – Create a DLP policy for Power Platform

Your company uses Power Automate flows to share data between SharePoint Online and Salesforce. In this task, you will create a DLP policy for Power Platform that allows your existing flows to keep working but prevents the creation of flows that will share data between SharePoint Online and Apps defined as non-business.

- [ ] You should still be logged into Client 1 VM (SC-400-CL1) as the **SC-400-CL1\admin** account.
- [ ] In **Microsoft Edge**, navigate to `**https://admin.powerplatform.microsoft.com**` and log into the Power Platform admin center as **MOD Administrator** `admin@WWLx549660.onmicrosoft.com` Admin's password should be provided by your lab hosting provider.
- [ ] In the **Power Platform admin center**, in the left sidebar, select the drop-down for **Policies**, then select **Data policies**.
- [ ] On the **Data policies** page, select **+ New Policy**.
- [ ] On the **Name your policy** page, enter `Tenant-wide SharePoint Policy` as the policy name, then select **Next**.
- [ ] On the **Non-business|Default** tab on the **Assign connectors** page, select **SharePoint** and **Salesforce**, then select **Move to Business** at the top of the page.
    
    [![](https://raw.githubusercontent.com/riswinto/SC-400T00A-Microsoft-Information-Protection-Administrator/master/Instructions/Media/move-to-business.png)](https://raw.githubusercontent.com/riswinto/SC-400T00A-Microsoft-Information-Protection-Administrator/master/Instructions/Media/move-to-business.png)
    
- [ ] In the **Assign connectors** page, select the **Business** tab to make sure both SharePoint and Salesforce now appear in this tab, then select **Next**.
- [ ] On the **Custom connector patterns** page select **Next**.
- [ ] On the **Define scope** page, select **Add all environments**, then select **Next**.
- [ ] On the **Review and create policy** page review your policy settings, then select **Create policy**.
- [ ] Sign out of the MOD Administrator account by selecting the **MA** icon in the top right, then selecting **Sign out**. Close the browser window once you're signed out.

You have successfully created a Power Platform DLP policy, ensuring that data flow between SharePoint Online and non-business connectors is controlled.

# Lab 2 – Exercise 2 – Manage endpoint DLP

You are Joni Sherman, the newly hired Compliance Administrator for Contoso Ltd. tasked to configure the company's Microsoft 365 tenant for data loss prevention. Contoso Ltd. is a company offering driving instruction in the United States and you need to make sure that sensitive customer information does not leave the organization. For this reason, you decide to not only implement Microsoft 365 DLP policies but extend this protection to devices in your organization.

**Tasks**:

- [ ] Enable device onboarding
- [ ] Onboard a device to endpoint DLP
- [ ] Create an endpoint DLP policy
- [ ] Configure Endpoint DLP settings
- [ ] Configure Microsoft Purview extension

## Task 1 – Enable device onboarding

In this task, you'll enable device onboarding for your organization.

- [ ] Log into Client 1 VM (SC-400-CL1) as the **SC-400-CL1\admin** account.
- [ ] In **Microsoft Edge**, navigate to `**https://purview.microsoft.com**` and log into the Microsoft Purview portal as **Joni Sherman**. sign in as `JoniS@WWLx549660.onmicrosoft.com` Joni's password was set in a previous exercise.
- [ ] In **Microsoft Edge**, navigate to `**https://purview.microsoft.com**`, then select **Settings** from the left sidebar.
- [ ] In the left sidebar, expand **Device onboarding** then select **Devices**.
- [ ] On the **Devices** page, select **Turn on device onboarding** to enable the solution for your tenant.
- [ ] Accept the **Turn on device onboarding** dialog by selecting **OK**.
- [ ] Accept the **Device monitoring is being turned on** dialog by selecting **OK**.

You have now enabled device onboarding and can start to onboard devices to be protected with Endpoint DLP policies. The process of enabling the feature might take up to 30 minutes, but you can proceed with the next task as it's not dependent on this.

## Task 2 – Onboard a device to endpoint DLP

In this task, you will use the local script option to onboard a Windows 11 device to allow it to be protected by Endpoint DLP policies.

- [ ] Log into Client 2 VM (SC-400-CL2) as the **SC-400-cl1\admin** account.
- [ ] Open Microsoft Edge, and navigate to `**https://purview.microsoft.com**` and log into the Microsoft Purview portal as **Joni Sherman**. sign in as `JoniS@WWLx549660.onmicrosoft.com` Joni's password was set in a previous exercise.
- [ ] Select **Settings** from the left sidebar.
- [ ] On the left sidebar, expand **Device onboarding**, then select **Onboarding**.
- [ ] On the **Onboarding** page, in the **Deployment method** dropdown menu, select **Local Script (for up to 10 machines)** and select **Download package**.
- [ ] In the **Downloads** dialog, hover over the download, then select the folder icon to **Show in folder**.
- [ ] Extract the zip-file to the **Desktop** of SC-400-CL1. You should see a script named **DeviceComplianceLocalOnboardingScript.cmd**.
- [ ] On the desktop right click the **DeviceComplianceLocalOnboardingScript.cmd** file you just extracted and select **Show more options**, then select **Properties**.
- [ ] Towards the bottom of the **General** tab of the properties window, in the **Security** section, select **Unblock**, then select **OK** to save this setting.
- [ ] Back on the desktop, right click **DeviceComplianceLocalOnboardingScript.cmd**, then select **Run as administrator**. On the **User Account Control** dialogue, select **Yes**.
- [ ] In the **Command Prompt** screen type **Y** to confirm, and then press Enter.
- [ ] When the script is complete, you'll get a success message and a prompt to **Press any key to continue**. Press any key to close the command line window. It can take a minute to complete the onboarding.
- [ ] Open the start menu and search for `Access work or school`. Select **Access work or school** under **Best match**.
- [ ] In the **Access work or school** window for **Add a work or school account** select **Connect**.
- [ ] In the **Set up a work or school account** dialog, select the **Join this device to Microsoft Entra ID** link and sign in as **Joni Sherman** `JoniS@WWLx549660.onmicrosoft.com` Joni's password was set in a previous exercise.
- [ ] In the **Make sure this is your organization** dialog, review the tenant URL and select **Join**.
- [ ] Once your device has connected select **Done** on the **You're all set!** screen.
- [ ] Restart Client 2 VM (SC-400-CL2).
- [ ] Log back into Client 1 VM (SC-400-CL1).
- [ ] The Microsoft Purview window should still be open at the **Devices** page. Refresh this page and verify the device has been successfully onboarded.

You have successfully onboarded a device and joined it to Microsoft Entra ID to be protected by endpoint DLP policies.

## Task 3 – Create an endpoint DLP policy

In this task, you will create a Data Loss Prevention (DLP) policy in the Microsoft Purview portal to prevent sensitive information from being shared with generative AI platforms on Windows 11 devices. This policy will help ensure that sensitive customer data, such as driver's license numbers and personal information, is not accidentally or intentionally shared with AI platforms, protecting the organization's data integrity.

- [ ] Log on to Client 1 VM (SC-400-CL1) as the SC-400-cl1\admin account.
- [ ] You should still be at the **Devices** page in the Microsoft Purview portal, logged in as Joni Sherman. Select the **Home** button on the top left of the screen. If you're not logged in, navigate to `https://purview.microsoft.com` and login as Joni Sherman. Joni's password was set in a previous exercise.
- [ ] In the Microsoft Purview portal, select **Solutions** from the left sidebar, then select **Data Loss Prevention**.
- [ ] From the left, navigation pane, select **Policies** then select **+ Create policy**.
- [ ] On the **Start with a template or create a custom policy** page, select **Custom** and **Custom policy**, then select **Next**.
- [ ] On the **Name your DLP policy** page, enter:
    - **Name**: `Generative AI sharing DLP policy`
    - **Description**: `Prevent sharing of sensitive data with generative AI platforms.`
- [ ] On the **Assign admin units** page, select **Next**.
- [ ] On the **Choose locations to apply the policy** page, select only the **Devices** location. If any other location is selected, ensure they're deselected, then select **Next**.
- [ ] On the **Define policy settings** page, select **Create or customize advanced DLP rules** then select **Next**.
- [ ] On the **Customize advanced DLP rules** page, select **+ Create rule**.
- [ ] On the **Create rule** page, enter:
    - **Name**: `Sensitive data protection rule`
    - **Description**: `Detect and restrict sharing of sensitive information with generative AI platforms.`
- [ ] Under **Conditions** select **+ Add condition** then select **Content contains**.
- [ ] In the newly opened **Content contains** area, select **Add** then select **Sensitive info types**.
- [ ] On the **Sensitive info types** flyout panel on the right, search for `U.S.` then select all United States related sensitive info types. Select **Add** at the bottom of the flyout panel.
- [ ] Scroll down to **Actions** and select the **+ Add an action** dropdown then select **Audit or restrict activities on devices**.
- [ ] In the newly opened **Audit or restrict activities on devices** area, in the **Service domain and browser activities** section, select the checkbox for **Upload to a restricted cloud service domain or access from an unallowed browsers**, then select **+ Choose different restrictions for sensitive service domains** under this option.
- [ ] In the **Sensitive service domain restrictions** flyout panel, select **+ Add group**.
- [ ] In the **Choose sensitive service domain groups** select the checkbox for **Generative AI Websites**, then select **Add** at the bottom of the flyout panel.
- [ ] Back on the **Sensitive service domain restrictions** page, ensure **Generative AI Websites** is listed, then select **Save** at the bottom of the flyout panel.
- [ ] Back on the **Create rule**, select the checkbox for **Paste to supported browsers**, then select **+ Choose different restrictions for sensitive service domains** under this option.
- [ ] In the **Sensitive service domain restrictions** flyout panel, select **+ Add group**.
- [ ] In the **Choose sensitive service domain groups** select the checkbox for **Generative AI Websites**, then select **Add** at the bottom of the flyout panel.
- [ ] Back on the **Create rule** in the **Service domain and browser activities** section, update the action for both **Upload to a restricted cloud service domain or access from an unallowed browsers** and **Paste to supported browsers** from **Audit only** to **Block**.
- [ ] In the **File activities for all apps** section, leave the default action of **Audit only**.
- [ ] In the **User notifications** section, set **Use notifications to inform your users and help educate them on the proper use of sensitive info.** to **On**.
- [ ] Under **Endpoint devices** select the checkbox for **Show users a policy tip notification when an activity is restricted. This is turned on when you select Block for an activity in Windows. To turn off the notifications on Windows devices, disable the restrictions**.
- [ ] Under **Microsoft 365 services** select the checkbox for **Notify users in Office 365 service with a policy tip**.
- [ ] Select **Save** at the bottom of the flyout panel.
- [ ] Back on the **Customize advanced DLP rules**, select **Next**.
- [ ] On the **Policy mode** page select **Turn the policy on immediately** then select **Next**.
- [ ] On the **Review and finish** page, review your policy settings then select **Submit** to create the policy.
- [ ] Once the policy is created select **Done** on the **New policy created** page.

You have successfully activated the Endpoint DLP Policy. This policy will prevent the sharing of sensitive information with generative AI platforms, ensuring that sensitive data such as driver's license numbers and personal details are protected from unauthorized access or exposure.

## Task 4 – Configure endpoint DLP settings

In this task, you will configure a file path exclusion to a folder on your Windows 11 devices to make sure that the content of this folder is not monitored by the Endpoint DLP policy you created.

- [ ] You should still be logged into Client 1 VM (SC-400-CL1) as the **SC-400-cl1\admin** account, and you should be logged into Microsoft 365 as **Joni Sherman**.
- [ ] In **Microsoft Edge**, the Microsoft Purview portal tab should still be open to the **Policies** page for data loss prevention. Select **Settings** from the left sidebar.
- [ ] On the settings page, select **Data Loss Prevention** from the left sidebar.
- [ ] The **Data Loss Prevention settings** page should open to the **Endpoint DLP settings**.
- [ ] On the **Endpoint DLP settings** page, expand **File path exclusions for Windows** then select **+ Add file path exclusion**.
- [ ] On the **Exclude these file paths from Windows devices** flyout page in the **File path exclusion** field, enter `C:\FilePathExclusionTest` then select the **+** button to the right. Select **Save** to save this entry.
- [ ] Back on the **Endpoint DLP settings** page, expand **Browser and domain restrictions to sensitive data** and select **+ Add or edit unallowed browsers**.
- [ ] On the **Add unallowed browsers** flyout page select the checkbox for **Google Chrome** and select **Save**.
- [ ] Back on the **Endpoint DLP settings** page, select the dropdown to for **Service domains** and change it from **Off** to **Block**.
- [ ] In the **Update cloud app mode** dialogue select **Yes** to activate the block mode.
- [ ] Under **Service domains** select **+ Add cloud service domain**.
- [ ] On the **Add cloud service domain** flyout page in the **Domain** field enter `dropbox.com` then select the **+** to the right. Select **Save** to save this setting.
- [ ] Close the browser window.

You have now configured custom settings for your Endpoint DLP policies. Every policy you create will ignore content in the folder you configured, and the Google Chrome browser has been added as unallowed browser to handle sensitive data.

## Task 5 – Configure Microsoft Purview extension

As Compliance Administrator you need to evaluate the new business requirement of rolling out the Chrome browser to several users for working with sensitive data. For this test, you'll install the Google Chrome browser to Client 01 and then add the **Microsoft Purview Compliance Extension for Google** manually from the Google web store.

- [ ] Open the Edge browser from the task bar.
- [ ] Navigate to the Google Chrome download at `**https://chrome.google.com**`.
- [ ] Select **Download Chrome** and select **Open file** from the **Downloads** notification for **ChromeSetup.exe**.
- [ ] Select **Yes** in the **User Account Control** dialog to install the Chrome browser.
- [ ] When the installation is finished, select **Don't sign in** on the **Sign in to Chrome** page.
- [ ] Select **Skip** on the **Set your default browser** page.
- [ ] When the newly installed Chrome browser window opens, navigate to the Microsoft Purview Extension in the Chrome web store at:
    
    `https://chrome.google.com/webstore/detail/microsoft-purview-extensi/echcggldkblhodogklpincgchnpgcdco`
    
- [ ] Verify you are on the extension page of **Microsoft Purview Extension** and select **Add to Chrome**.
- [ ] On the **Add "Microsoft Purview Extension"?** window, select **Add extension**.
- [ ] Close the notification for the extension being added to Chrome, then navigate to `**chrome://extensions**`.
- [ ] Validate the **Microsoft Purview Extension** is visible and activated.
- [ ] Close the Chrome browser window.

You have successfully installed the Chrome browser and added the Microsoft Purview Extension to your client. The Chrome browser can now be used like the Edge browser to work with sensitive data and the previously configured Endpoint DLP policy also applies when using the Chrome browser.

# Lab 2 - Exercise 3 – Manage DLP reports

You are Joni Sherman, the Compliance Administrator for Contoso Ltd. tasked to configure the company's Microsoft 365 tenant for data loss prevention. Contoso Ltd. is a company offering driving instruction in the United States and you need to make sure that sensitive customer information does not leave the organization. You are informed that a new compliance officer will help you review DLP reports.

**Tasks**:

- [ ] Grant access to DLP reports
- [ ] Review DLP data in the activity explorer
- [ ] Explore DLP data using PowerShell

## Task 1 – Grant access to DLP reports

In this exercise, you will grant the new compliance officer Megan Bowen access to the DLP reports. As a non-technical user this compliance officer will only read reports and not change the DLP configuration.

- [ ] Log into Client 1 VM (SC-400-CL1) as the **SC-400-cl1\admin** account.
- [ ] In **Microsoft Edge**, navigate to `**https://purview.microsoft.com**` and log into the Microsoft Purview portal as **MOD Administrator** `admin@WWLx549660.onmicrosoft.com` Admin's password should be provided by your lab hosting provider.
- [ ] Select **Settings** from the left sidebar.
- [ ] On the **Settings** page, expand **Roles and scopes** on the left sidebar, then select **Role groups**.
- [ ] On the **Role groups for Microsoft Purview solutions** page select the checkbox for **Information Protection Analysts**, then select the **Edit** tab from the top navigation bar.
- [ ] On the **Edit members of the role group** page select **+ Choose users**.
- [ ] On the **Choose users** flyout panel, search for `Megan` to find Megan Bowen's account. Select the checkbox for **Megan Bowen**'s account then select the **Select** button at the bottom of the panel.
- [ ] Back on the **Edit members of the role group** page verify Megan's account is displayed, then select **Next**.
- [ ] On the **Review the role group and finish** page select **Save**.
- [ ] On the **You successfully updated the role group** page select **Done**.
- [ ] Sign out of the MOD Administrator account by selecting the **MA** icon in the top right, then selecting **Sign out**.

You have now granted the new compliance officer access to the DLP reports in the Microsoft 365 compliance portal.

## Task 2 – Review DLP data in the activity explorer

In this task, you will test that the access to the DLP reports you granted in Task 1 is applied correctly.

- [ ] Log into the Client 1 VM (SC-400-CL1) as the **SC-400-cl2\admin** account.
- [ ] In **Microsoft Edge**, navigate to `**https://purview.microsoft.com**` and log into the Microsoft Purview portal as **Megan Bowen** `MeganB@WWLx549660.onmicrosoft.com` Megan's password was set in a previous exercise.
- [ ] Select **Solutions** from the left sidebar, then select **Data Loss Prevention**.
- [ ] In the left sidebar, select **Activity explorer**.
- [ ] On the **Activity explorer** page, select the dropdown for **Built-in filters**.
- [ ] Explore the **DLP policies that detected activities** filter and the **DLP policy rules that detected activities** filter.
- [ ] Sign out of Megan's account by selecting the **MB** icon in the top right, then selecting **Sign out**.

You now verified that the access has been configured and the new compliance officer can view reports in the Purview portal.

## Task 3 – Explore DLP data using PowerShell

In this task, you will review DLP activities via PowerShell.

- [ ] You should still be logged into Client 1 VM (SC-400-CL1) as the **SC-400-cl1\admin** account.
- [ ] Open an elevated PowerShell window by right clicking the Windows button in the task bar, then select **Terminal (Admin)**.
- [ ] Run the **Connect-IPPSSession** cmdlet to connect to the Information Protection PowerShell session:

```PowerShell
powershell
   Connect-IPPSSession
```

- [ ] In the **Sign in to your account** dialogue, select **+ Use another account** then login with the account **Megan Bowen** `MeganB@WWLx549660.onmicrosoft.com`
- [ ] Run the **Export-ActivityExplorerData** PowerShell cmdlet to explore the activity explorer from PowerShell. The script below is an example that will display a grid view of activities from the most recent week:

```PowerShell
powershell
   $StartTime = (Get-Date).AddDays(-7)
   $EndTime = (Get-Date).AddDays(1)
   $Results = Export-ActivityExplorerData -StartTime $StartTime -EndTime $EndTime -OutputFormat JSON
   ($Results.ResultData) | ConvertFrom-Json | select -ExpandProperty SyncRoot | ogv
```

- [ ] Explore the data collected from previous labs then close the grid view window.
- [ ] The script below is an example of using the **Filter1** parameter to display endpoint activities from the most recent week:

```PowerShell
powershell
   $StartTime = (Get-Date).AddDays(-7)
   $EndTime = (Get-Date).AddDays(1)
   $Results = Export-ActivityExplorerData -StartTime $StartTime -EndTime $EndTime -Filter1 @("Workload","Endpoint")-OutputFormat JSON
   ($Results.ResultData) | ConvertFrom-Json | select -ExpandProperty SyncRoot | ogv
```

- [ ] Explore the data collected from previous labs then close the grid view window.

You have successfully reviewed DLP activities as the new compliance officer, Megan Bowen.

  

# Lab 3 - Exercise 1 - Configure retention policies

In this lab, you are Joni Sherman, a Compliance Administrator at Contoso Ltd. in Texas. Your task is to implement retention policies to comply with state regulations, which allow records to be deleted after three years. You'll configure various retention policies across the organization to ensure data is managed and retained according to these legal requirements.

**Tasks**:

- [ ] Create a company-wide retention policy
- [ ] Create a Teams retention policy with specific user selection
- [ ] Create a retention policy with PowerShell
- [ ] Create an adaptive retention policy for legal and retail documents
- [ ] Test the adaptive scope policy

## Task 1 – Create a company-wide retention policy

In this task, you'll set up a company-wide retention policy that covers key Microsoft 365 locations, ensuring that all items are retained for three years in compliance with state laws.

- [ ] Log into Client 1 VM (SC-400-CL1) as the **SC-400-cl1\admin** account.
- [ ] In **Microsoft Edge**, navigate to `**https://purview.microsoft.com**` and log into the Microsoft Purview portal as **Joni Sherman** `JoniS@WWLx549660.onmicrosoft.com` Joni's password was set in a previous exercise.
- [ ] Select **Solutions** then select **Data Lifecycle Management**.
- [ ] On the **Data Lifecycle Management** page, on the left sidebar, expand **Policies** then select **Retention policies**.
- [ ] On the **Retention policies** page, select **+ New retention policy**.
- [ ] On the **Name your retention policy** page, enter:
    - **Name**: `Company wide`
    - **Description**: `All locations except for teams`
- [ ] Select the **Next** button.
- [ ] On the **Policy Scope** page select **Next**.
- [ ] On the **Choose the type of retention policy to create** page, select **Static** then select **Next**.
- [ ] In the **Choose where to apply this policy** these locations:
    - Exchange mailboxes
    - SharePoint classic and communication sites
    - OneDrive accounts
    - Microsoft 365 Group mailboxes & sites
- [ ] Select **Next**.
- [ ] On the **Decide if you want to retain content, delete it, or both** page, ensure these values are set for the retention configuration:
    - Select **Retain items for a specific period**.
    - Under **Retain items for a specific period**, select **Custom** from the dropdown list
    - Change the years field to **3**
    - **Start the retention period based on**: When items were last modified
    - **At the end of the retention period**: Delete items automatically
- [ ] Select **Next**.
- [ ] On the **Review and finish** page select **Submit**.
- [ ] Once your policy is created select **Done** on the **You successfully created a retention policy** page.

You have successfully created a retention policy that retains items across key Microsoft 365 locations for three years from the date of last modification. This policy can take up to 24 hours to be applied in your tenant, but you can proceed to the next step.

## Task 2 – Create a Teams retention policy with specific user selection

Next, you'll create a retention policy specifically for Microsoft Teams, applying it to channel messages and select user chats to manage their retention separately from other data. Your organization has decided that a limited number of users are required to have their Team chats require a retention period.

- [ ] You should still be logged into Client 1 VM (SC-400-CL1) as the **SC-400-cl1\admin** account, and you should be logged into Microsoft Purview as **Joni Sherman**.
- [ ] In Microsoft Edge, you should still be on the **Retention policies** page in the Microsoft Purview portal. If not, navigate to `**https://purview.microsoft.com**`, then select **Solutions** and select **Data Lifecycle Management**. Select **Policies** > **Retention policies** from the left sidebar.
- [ ] On the **Retention policies** page, select **+ New retention policy**.
- [ ] On the **Name your retention policy** page, enter:
    - **Name**: `Teams Retention`
    - **Description**: `Retention for Teams locations`
- [ ] Select **Next**.
- [ ] On the **Policy Scope** page select **Next**.
- [ ] On the **Choose the type of retention policy to create** page, select **Static** then select **Next**.
- [ ] On the **Choose locations to apply the policy** page enable these locations:
    - Teams channel messages
    - Teams chats and Copilot interactions
    - Leave all other locations disabled.
- [ ] For the **Teams chats and Copilot interactions** location, select the **Edit** text link under **All users**
- [ ] On the **Teams chats and Copilot interactions** flyout panel add users:
    
    - Adele Vance
    - Pradeep Gupta
    
    > Note: By adding these two users the setting for Included in Teams chats changes from All teams to 2 users.
    
- [ ] Select **Done** at the bottom of the flyout panel.
- [ ] Back on the **Choose where to apply this policy** page select **Next**.
- [ ] On the **Decide if you want to retain content, delete it, or both** page, ensure these values are set for the retention configuration:
    - Select **Retain items for a specific period**.
    - Under **Retain items for a specific period**, select **Custom** from the dropdown list
    - Change the years field to **3**
    - **Start the retention period based on**: When items were last modified
    - **At the end of the retention period**: Delete items automatically
- [ ] Select **Next**.
- [ ] On the **Review and finish** page select **Submit**.
- [ ] Once your policy is created select **Done** on the **You successfully created a retention policy** page.
- [ ] Close the browser window.

You have successfully configured a retention policy for Microsoft Teams, ensuring that channel messages and specific user chats are retained for three years.

## Task 3 – Create retention policy with PowerShell

In this task, you'll create the same retention policies using PowerShell, demonstrating how to automate the policy setup process.

- [ ] Log into Client 1 VM (SC-400-CL1) as the **SC-400-cl1\admin** account.
- [ ] Open an elevated PowerShell window by right clicking the Windows button in the task bar, then select **Terminal (Admin)**. Select **Yes** if the **User Account Control** dialogue pops up.
- [ ] Run the **Connect-IPPSSession** cmdlet to connect to the Security & Compliance Center in your tenant:
    
    ```PowerShell
    powershell
    Connect-IPPSSession
    ```
    
- [ ] When prompted with a sign in dialog box, sign in as **MOD Administrator** `admin@WWLx549660.onmicrosoft.com` Admin's password should be provided by your lab hosting provider.
- [ ] Run the **New-RetentionCompliancePolicy** cmdlet to create the first retention policy for all locations except teams:
    
    ```PowerShell
    powershell
    New-RetentionCompliancePolicy -Name "Company Wide PS" -ExchangeLocation All -ModernGroupLocation All -SharePointLocation All -OneDriveLocation All
    ```
    
- [ ] Run the **New-RetentionComplianceRule** cmdlet to set the retention period to 3 years, using days as units based on the date modified:
    
    ```PowerShell
    powershell
    New-RetentionComplianceRule -Name "Company Wide PS Rule" -Policy "Company Wide PS" -RetentionDuration 1095 -ExpirationDateOption ModificationAgeInDays -RetentionComplianceAction Keep
    ```
    
- [ ] Run the **New-RetentionCompliancePolicy** cmdlet to create the second retention policy for Teams locations:
    
    ```PowerShell
    powershell
    New-RetentionCompliancePolicy -Name "Teams Retention PS" -TeamsChannelLocation All -TeamsChatLocation "Adele Vance", "Pradeep Gupta"
    ```
    
- [ ] Run the **New-RetentionComplianceRule** cmdlet to set the retention period to 3 years, using days as units:
    
    ```PowerShell
    powershell
    New-RetentionComplianceRule -Name "Teams Retention PS Rule" -Policy "Teams Retention PS" -RetentionDuration 1095 -RetentionComplianceAction Keep
    ```
    
- [ ] Close the terminal window.

You have successfully created retention policies using PowerShell, mirroring the policies set up through the Microsoft Purview portal.

## Task 4 – Create an adaptive retention policy for legal and retail documents

Now, you'll create an adaptive retention policy for the finance and legal departments, ensuring that all legal-related documents are retained for five years.

- [ ] You should still be logged into Client 1 VM (SC-400-CL1) as the **SC-400-cl1\admin** account, and you should be logged into Microsoft 365 as **Joni Sherman**.
- [ ] Open Microsoft Edge and navigate to `**https://purview.microsoft.com**`. Verify you're still logged in with Joni's account, then select **Settings** from the left sidebar.
- [ ] On the **Settings** page, expand **Roles and scopes** from the left sidebar, then select **Adaptive scopes**.
- [ ] On the **Adaptive scopes** page select **+ Create scope**.
- [ ] On the **Name your adaptive policy scope** page enter:
    - **Name**: `Legal Documents Retention`
    - **Description**: `Retention for legal related documents`
- [ ] Select **Next**.
- [ ] On the **Assign admin unit** page select **Next**.
- [ ] On the **What type of scope do you want to create?** page select **Users** then select **Next**.
- [ ] On the **Create the query to define users** page, in the **User attributes** section, ensure these values are selected for the user attribute configuration:
    - Select the **Attribute** dropdown then select **Department**
    - Leave the default **is equal to** value in the next field
    - Enter `Legal` as the **Value**
- [ ] Add a second attribute by selecting **+ Add attribute** on the **Create the query to define users** page. In the new field under the one we just configured, configure these values:
    - Select the dropdown for the query operator and update it from And to **Or**
    - Select the **Attribute** dropdown then select **Department**
    - Leave the default **is equal to** value in the next field
    - Enter `Retail` as the **Value**
- [ ] Select **Next**.
- [ ] On the **Review and finish** page select **Submit**.
- [ ] Once your adaptive scope is created select **Done** on the **Your scope was created** page.
- [ ] Back on the **Adaptive scopes** page, select **Solutions** from the bottom of the left sidebar.
- [ ] Select the tab for **Data Governance** from the top filter buttons.
- [ ] Select the **Data Lifecycle Management** card.
- [ ] On the **Data Lifecycle Management** page, expand **Policies** then select **Retention policies**.
- [ ] On the **Retention policies** page, select **+ New retention policy**.
- [ ] On the **Name your retention policy** page enter:
    - **Name**: `Legal Data Retention`
    - **Description**: `Retention of all documents within the legal and retail departments.`
- [ ] Select **Next**.
- [ ] On the **Policy Scope** page select **Next**.
- [ ] On the **Choose the type of retention policy to create** page select **Adaptive** then select **Next**.
- [ ] On the **Choose adaptive policy scopes and locations** page select **+ Add scopes**.
- [ ] On the **Choose adaptive policy scopes** flyout panel select the checkbox for **Legal Documents Retention** then select **Add** at the bottom of the panel.
- [ ] Back on the **Choose locations to apply the policy** enable:
    - Exchange mailboxes
    - OneDrive accounts
    - Leave all other locations disabled.
- [ ] Select **Next**.
- [ ] On the **Decide if you want to retain content, delete it, or both** page, ensure these values are set for the retention configuration:
    - Select **Retain items for a specific period**.
    - Under **Retain items for a specific period**, select **5 years** from the dropdown list
    - **Start the retention period based on**: When items were last modified
    - **At the end of the retention period**: Do nothing
- [ ] Select **Next**.
- [ ] On the **Review and finish** page select **Submit**.
- [ ] Once your policy is created, select the **Done** button.
- [ ] Once your policy is created select **Done** on the **You successfully created a retention policy** page.

You have successfully applied an adaptive scope to a retention policy, covering legal and retail department documents for five years.

## Task 5 – Test the adaptive scope policy

In this final task, you'll verify the users affected by the adaptive scope and test the new retention policy to ensure it is functioning as expected.

> Note: When you create and submit a retention policy, it can take up to seven days for the retention policy to be applied.

- [ ] Open an elevated PowerShell window by right clicking the Windows button in the task bar, then select **Terminal (Admin)**. Select **Yes** if the **User Account Control** dialogue pops up.
- [ ] Run the **Connect-IPPSSession** cmdlet to the Security & Compliance Center in your tenant:
    
    ```PowerShell
    powershell
    Connect-IPPSSession
    ```
    
- [ ] When prompted with a sign in dialog box, sign in with Joni Sherman's account, `JoniS@WWLx549660.onmicrosoft.com` Joni's account was set in a previous exercise.
- [ ] Run the **Get-RetentionCompliancePolicy** cmdlet to view all details of the adaptive scope policy:
    
    ```PowerShell
    powershell
    Get-RetentionCompliancePolicy -Identity "Legal Data Retention" -DistributionDetail | Format-List
    ```
    
- [ ] Review the results and search for these details:
    
    - **Enabled**: True
    - **Mode**: Enforce
    - **DistributionStatus**: Success
    
    [![](https://raw.githubusercontent.com/riswinto/SC-400T00A-Microsoft-Information-Protection-Administrator/master/Instructions/Media/results-getretentioncompliancepolicy.png)](https://raw.githubusercontent.com/riswinto/SC-400T00A-Microsoft-Information-Protection-Administrator/master/Instructions/Media/results-getretentioncompliancepolicy.png)
    

You have verified the successful implementation of the adaptive scope retention policy, confirming that it is correctly applied and operational.

# Lab 3 - Exercise 2 - Implement retention labels

In this exercise, you will assume the role of Joni Sherman, a System Administrator for Contoso Ltd., based in Sudbury, England. The company is focused on adhering to strict compliance and data retention standards, particularly concerning financial records. To ensure these records are managed systematically and efficiently, you will implement a file plan that includes creating and applying retention labels for critical documents, such as Value Added Tax (VAT) returns and credit card receipts. This will help Contoso Ltd. meet both legal and internal compliance requirements.

**Tasks**:

- [ ] Create retention labels with file plan
- [ ] Publish retention labels
- [ ] Publish auto-apply retention labels
- [ ] Apply retention labels in Outlook
- [ ] Apply retention labels in SharePoint
- [ ] Apply retention labels in OneDrive

## Task 1 – Create retention labels with file plan

In this task, you'll create retention labels for VAT returns and supporting documents, as well as for credit card receipts. These labels will be part of a comprehensive file plan to manage and secure these documents according to the company's compliance requirements.

- [ ] Log into Client 1 VM (SC-400-CL1) as the **SC-400-cl1\admin** account.
- [ ] In **Microsoft Edge**, navigate to `**https://purview.microsoft.com**` and log into the Microsoft Purview portal as **Joni Sherman** `JoniS@WWLx549660.onmicrosoft.com` Joni's password was set in a previous exercise.
- [ ] In the **Microsoft Purview** portal, on the left sidebar, select **Solutions**, then select **Records Management**.
- [ ] On the **Records Management** page, in the left sidebar select **File plan**.
- [ ] On the **File plan** page, select **+ Create a label**.
- [ ] On the **Name your retention label** page enter:
    - **Name**: `VAT Returns and Supporting Documents`
    - **Description for users**: `Assign this label to VAT Documents to ensure they are retained for the legal period of seven years.`
    - **Description for admins**: `VAT returns with seven-year retention.`
- [ ] Select **Next**.
- [ ] On the **Define file plan descriptors for this label** page enter:
    - **Reference ID**: `VAT-001`
    - **Business function/department**: Select **Choose** next to this field. In the **Business function/department** flyout panel select **Finance**, then select **Choose** at the bottom of the panel.
    - **Category**: Select **Choose** next to this field. In the **Category** flyout panel, select **+ Create new category**. In the **Category** field, enter `Financial records`, then select **Add** at the bottom of the panel.
    - **Sub category**: Leave this field blank.
    - **Authority type**: Select **Choose** next to this field. In the **Authority type** flyout panel, select **Regulatory**, then select **Choose** at the bottom of the panel.
    - **Provision/citation**: Select **Choose** next to this field. In the **Provision/citation** flyout panel, select **Sarbanes-Oxley Act of 2002**, then select **Choose** at the bottom of the panel.
- [ ] Back on the **Define file plan descriptors for this label** page, select **Next**.
- [ ] On the **Define label settings** page, select **Retain items forever or for a specific period**, then select **Next**.
- [ ] On the **Define the period** page, ensure these values are set for the retention period configuration input:
    - **How long is the period?**: 7 Years
    - **When should the period begin?**: When items were created
- [ ] Select **Next**.
- [ ] On the **Choose what happens during the retention period** page, select **Retain items even if users delete**, then select **Next**.
- [ ] On the **Choose what happens after the retention period** page select **Deactivate retention settings** then select **Next**.
- [ ] On the **Review and finish** page select **Create label**.
- [ ] On the **Your retention label is created** page select the option to **Do Nothing** then select **Done**. The label will be published in a later task.
- [ ] Back on the **File plan** page, select **+ Create a label** to create another retention label.
- [ ] On the **Name your retention label** enter:
    - **Name**: `Credit Card Receipts`
    - **Description for users**: `This label is auto applied to Credit card receipts with a retention period of three years.`
    - **Description for admins**: `Auto applied retention label for Credit card receipts with three-year retention.`
- [ ] Select **Next**.
- [ ] On the **Define file plan descriptors for this label** page enter:
    - **Reference ID**: `CC-002`
    - **Business function/department**: Select **Choose** next to this field. In the **Business function/department** flyout panel select **Sales**, then select **Choose** at the bottom of the panel.
    - **Category**: Select **Choose** next to this field. In the **Category** flyout panel select **Financial records**, then select **Choose** at the bottom of the panel.
    - **Sub category**: Select **Choose** next to this field. In the **Sub category** flyout panel, select **+ Create new subcategory**. In the **Sub category** field, enter `Receipts`, then select **Add** at the bottom of the panel.
    - **Authority type**: Select **Choose** next to this field. In the **Authority type** flyout panel, select **Business**, then select **Choose** at the bottom of the panel.
    - **Provision/citation**: Select **Choose** next to this field. In the **Provision/citation** flyout panel, select **Truth in Lending Act**, then select **Choose** at the bottom of the panel.
- [ ] Back on the **Define file plan descriptors for this label** page, select **Next**.
- [ ] On the **Define label settings** page select **Retain items forever or for a specific period** then select **Next**.
- [ ] On the **Define the period** page, ensure these values are set for the retention period configuration input:
    - **Retain items for**: Select the dropdown list and select **Custom**. Enter 3 for Years.
    - **Start the retention period based on**: When items were created.
- [ ] Select **Next**.
- [ ] On the **Choose what happens during the retention period** page, select **Retain items even if users delete**, then select **Next**.
- [ ] On the **Choose what happens after the retention period** page select **Deactivate retention settings** then select **Next**.
- [ ] On the **Review and finish** page select **Create label**.
- [ ] On the **Your retention label is created** page select **Do Nothing** then select **Done**.

You have successfully created retention labels for VAT returns with a seven-year retention period and for Credit Card receipts with a three-year retention period.

## Task 2 – Publish retention labels

Now, you will publish the VAT returns retention label, making it available for finance users to apply to relevant documents in Exchange emails and SharePoint sites.

- [ ] You should still be logged into Client 1 VM (SC-400-CL1) as the **SC-400-cl1\admin** account, and you should be logged into Microsoft 365 as **Joni Sherman**.
- [ ] You should still be on the **File plan** page in **Records Management**. If not, navigate to `https://purview.microsoft.com`, and select **Solutions** from the left sidebar, then select **Records Management**. Select **File plan** from the **Records Management** page.
- [ ] Select the **VAT Returns and Supporting Documents** label that was created previously.
- [ ] Select the **Publish labels** button ( ) to start the configuration to publish this retention label.
    
    [![](https://raw.githubusercontent.com/riswinto/SC-400T00A-Microsoft-Information-Protection-Administrator/master/Instructions/Media/publish-labels-icon.png)](https://raw.githubusercontent.com/riswinto/SC-400T00A-Microsoft-Information-Protection-Administrator/master/Instructions/Media/publish-labels-icon.png)
    
- [ ] On the **Choose labels to publish** page, verify the **VAT Returns and Supporting Documents** label is selected, then select **Next**.
- [ ] On the **Policy Scope** page select **Next**.
- [ ] On the **Choose the type of retention policy to create** page select **Static** then select **Next**.
- [ ] On the **Choose where to publish labels** page select **Let me choose specific locations** and select:
    - Exchange mailboxes
    - SharePoint classic and communication sites
    - OneDrive accounts
    - Deselect all other locations
- [ ] Select **Next**.
- [ ] On the **Name your policy** enter:
    - **Name**: `VAT Returns and Supporting Documents Retention Label`
    - **Description**: `VAT Returns and supporting documents Retention label, retention period 3 years, Exchange email and SharePoint site locations.`
- [ ] Select **Next**.
- [ ] On the **Finish** page select **Submit**.
- [ ] Once your retention label has been published, select **Done** on the **Your retention label was published** page.

You have successfully published the retention label for VAT Returns and supporting documents.

## Task 3 – Publish auto-apply retention labels

In this task, you'll configure the credit card receipts retention label to be auto-applied, ensuring that any relevant documents are automatically labeled and retained for the required period.

- [ ] You should still be logged into Client 1 VM (SC-400-CL1) as the **SC-400-cl1\admin** account, and you should be logged into Microsoft 365 as **Joni Sherman**.
- [ ] You should still be on the **File plan** page in **Records Management**. If not, navigate to `https://purview.microsoft.com`, and select **Solutions** from the left sidebar, then select **Records Management**. Select **File plan** from the **Records Management** page.
- [ ] Select the **Credit Card Receipts** label that was created previously.
- [ ] Select the **Auto-apply a label** button ( ) to start the configuration to publish this auto-apply retention label.
    
    [![](https://raw.githubusercontent.com/riswinto/SC-400T00A-Microsoft-Information-Protection-Administrator/master/Instructions/Media/auto-apply-labels-icon.png)](https://raw.githubusercontent.com/riswinto/SC-400T00A-Microsoft-Information-Protection-Administrator/master/Instructions/Media/auto-apply-labels-icon.png)
    
- [ ] On the **Let's get started** page, enter:
    - **Name**: `Credit Card Receipts auto-applied`
    - **Description**: `Credit Card Receipts auto-applied retention label, with a retention period of three years for all locations.`
- [ ] Select **Next**.
- [ ] On the **Choose the type of content you want to apply this label to** page select **Apply label to content that contains sensitive info** then select **Next**.
- [ ] On the **Content that contains sensitive info** page, select **Financial** under **Categories**, then select **U.K. Financial Data** under **Regulations**
- [ ] Select **Next**.
- [ ] On the **Define content that contains sensitive info** page select **Next**.
- [ ] On the **Policy Scope** page select **Next**.
- [ ] On the **Choose the type of retention policy to create** page, select **Static** then select **Next**.
- [ ] On the **Choose locations to apply the policy** page, select these locations:
    - Exchange mailboxes
    - SharePoint classic and communication sites
    - OneDrive accounts
    - Microsoft 365 Group mailboxes & sites
- [ ] Select **Next**.
- [ ] On the **Choose a label to auto-apply** page, ensure the **Credit Card Receipts** label is selected, then select **Next**.
- [ ] On the **Decide whether to test or run your policy**, select **Turn on policy** then select **Next**.
- [ ] On the **Review and finish** page, select **Submit**.
- [ ] Once your auto-labeling policy has been created, select **Done** on the **Your auto-labeling policy has been created.** page.
- [ ] Sign out of Joni's account by selecting her image in the top, right hand corner and selecting **Sign out**.

You have successfully configured the **Credit Card Receipts** retention label to be auto-applied, setting a three-year retention period for all identified documents.

## Task 4 – Apply retention labels in Outlook

Megan Bowen, a financial analyst at Contoso Ltd., needs to ensure that specific emails and folders in Outlook comply with the company's data retention policies. In this task, you'll apply the appropriate retention labels to her Outlook items.

- [ ] Log into Client 1 VM (SC-400-CL1) as the **SC-400-cl1\admin** account.
- [ ] In **Microsoft Edge**, navigate to `**https://outlook.office.com**`. and login as **Megan Bowen** `MeganB@WWLx549660.onmicrosoft.com` Megan's password was set in a previous exercise.
- [ ] In Megan's inbox, select right click the any email then select **Advanced actions** > **Assign policy** > **5 year delete** under the **Retention labels** section.
    
    This retention label assigns a retention period of 5 years to the chosen email. After the 5 year period, the item is deleted.
    
- [ ] Still in Outlook, expand **Inbox** from the left side bar, then right click the right click the **Project Falcon** folder.
- [ ] From the menu that appeared when you right clicked, select **Advanced actions** > **Assign policy** > **5 year delete** under the **Retention labels** section.
    
    This retention label assigns a retention period of 5 years to the Project Falcon folder and all its contents. After the 5 year period, the items are deleted.
    

You have successfully applied retention labels to both an email and a folder in Outlook.

## Task 5 – Apply retention labels in SharePoint

As a financial analyst, Megan Bowen manages sensitive documents in SharePoint. In this task, you will apply a retention label to a specific document in the SharePoint library, ensuring the document's retention aligns with company policy.

- [ ] You should still be logged into Client 1 VM (SC-400-CL1) as the **SC-400-cl1\admin** account.
- [ ] You should still be logged into Outlook as Megan Bowen. Select the meatball menu in the top left, then select **SharePoint** to navigate to SharePoint.
    
    [![](https://raw.githubusercontent.com/riswinto/SC-400T00A-Microsoft-Information-Protection-Administrator/master/Instructions/Media/meatball-menu-sharepoint.png)](https://raw.githubusercontent.com/riswinto/SC-400T00A-Microsoft-Information-Protection-Administrator/master/Instructions/Media/meatball-menu-sharepoint.png)
    
- [ ] On the SharePoint landing page, search for `Communication site` then select **Communication site** from the search results.
- [ ] In the top navigation bar, select the **Documents** tab.
- [ ] Select the **CAS** folder.
- [ ] Within the CAS folder, hover over the **Blog Post preview.docx** document and select the ellipses **…** for **Show more actions** to open the menu to show more options.
    
    [![](https://raw.githubusercontent.com/riswinto/SC-400T00A-Microsoft-Information-Protection-Administrator/master/Instructions/Media/show-more-actions-sharepoint.png)](https://raw.githubusercontent.com/riswinto/SC-400T00A-Microsoft-Information-Protection-Administrator/master/Instructions/Media/show-more-actions-sharepoint.png)
    
- [ ] From the action menu, select **More** > **Compliance details**
- [ ] A new window displaying the **Compliance details** for the document opens. For **Label Status** select **None** to open the **Apply Label** window.
    
    [![](https://raw.githubusercontent.com/riswinto/SC-400T00A-Microsoft-Information-Protection-Administrator/master/Instructions/Media/modify-label-status-sharepoint.png)](https://raw.githubusercontent.com/riswinto/SC-400T00A-Microsoft-Information-Protection-Administrator/master/Instructions/Media/modify-label-status-sharepoint.png)
    
- [ ] On the **Apply Label** page, select the dropdown for **Apply label** and change it from **None** to **VAT Returns and supporting documents (Retain for 7 years)**. Select **Save** to the right of the screen.

> Note: Retention labels might take 1-2 days to appear in SharePoint. If the VAT Returns and Supporting Documents label isn't available during this task, you can revisit and apply the label later.

You have successfully applied a retention label to a document in SharePoint.

## Task 6 – Apply retention labels in OneDrive

Megan Bowen, while working remotely, stores critical financial documents in OneDrive. This task involves applying retention labels to ensure these documents are managed according to the company's retention policies.

- [ ] You should still be logged into Client 1 VM (SC-400-CL1) as the **SC-400-cl1\admin** account.
- [ ] You should still be logged into Outlook as Megan Bowen. Select the meatball menu in the top left, then select **OneDrive** to navigate to OneDrive.
- [ ] Select **My files** from the left sidebar. When the list of files appears, hover over **Annual Financial Report** and select the ellipses **…** for **More actions** to open the menu to show more options.
- [ ] From the action menu, select **Details** to open the detail panel on the right.
- [ ] Under **Properties** scroll down to find the **Apply label** section. Select **Choose a label**, then select **VAT Returns and Supporting Documents** if available.
    
    [![](https://raw.githubusercontent.com/riswinto/SC-400T00A-Microsoft-Information-Protection-Administrator/master/Instructions/Media/apply-retention-label-onedrive.png)](https://raw.githubusercontent.com/riswinto/SC-400T00A-Microsoft-Information-Protection-Administrator/master/Instructions/Media/apply-retention-label-onedrive.png)
    

> Note: Retention labels might take 1-2 days to appear in OneDrive. If the VAT Returns and Supporting Documents label isn't available during this task, you can revisit and apply the label later.

- [ ] Select the **x** at the top of the details panel to close it. Changes made here are automatically applied.
- [ ] Sign out of Megan's account by selecting her icon in the top right, then selecting **Sign out**.

You have successfully applied a retention label to a document in OneDrive.

# Lab 3 - Exercise 3 - Configure event-based retention

In this exercise you will assume the role of Joni Sherman, a Compliance Administrator for Contoso Ltd. Your organization is based in Texas and wants to implement retention policies to retain content belonging to specific projects for 5 years after they close.

- [ ] Create event-driven retention label and event type
- [ ] Publish event-driven retention label
- [ ] Apply label and add an asset ID
- [ ] Create specific event
- [ ] Observe results of event trigger

## Task 1 – Create event-driven retention label and event type

In this step, you'll create a retention label and an event type. The event type will trigger the retention period. Any content that has the retention label applied to it for that specific event type will have the retention actions from the label enforced on it.

- [ ] You should still be logged into Client 1 VM (SC-400-CL1) as the **SC-400-cl1\admin**.
- [ ] In **Microsoft Edge**, navigate to `**https://purview.microsoft.com**` and log into the Microsoft Purview portal as **Joni Sherman** `JoniS@WWLx549660.onmicrosoft.com` Joni's password was set in a previous exercise.
- [ ] In the **Microsoft Purview** portal, on the left sidebar, select **Solutions**, then select **Records management**.
- [ ] On the **Records Management** page select **File plan** from the left sidebar, then select **Create a label**.
- [ ] On the **Name your retention label**, enter:
    - **Name**: `Project Asset`
    - **Description for users**: `Assign this label to project documents to ensure they are retained for the period of 5 years.`
    - **Description for admins**: `Project asset for event-based retention.`
- [ ] Select **Next**.
- [ ] On the **Define file plan descriptors for this label**, leave this page blank and select **Next**.
- [ ] On the **Define label settings** page, select **Retain items forever or for a specific period**, then select **Next**.
- [ ] On the **Define the retention period** page select the dropdown for **Retain items for**, then select **5 years**.
- [ ] Under the **Start the retention period based on** dropdown select **+ Create new event type**. This will start the event-based label configuration.
- [ ] On the **Name your event type** flyout panel on the right, enter:
    - **Name**: `Project Closure`
    - **Description**: `This event will be triggered when a project closes.`
- [ ] Select **Next**.
- [ ] Review the **Summary** page then select **Submit**
- [ ] On the **Your event type was created** page, select **Done**.
- [ ] Back on the **Define the retention period**, select the dropdown for **Start the retention period based on** then select the newly created **Product Closure** event type.
- [ ] Select **Next**.
- [ ] On the **Choose what happens during the retention period** page, select **Mark items as a record**, and select the option for **Unlock this record by default**.
- [ ] Select **Next**.
- [ ] On the **Choose what happens after the retention period** page, select **Delete items automatically**, then select **Next**.
- [ ] On the **Review and finish** page, select **Create label**.
- [ ] On the **Your retention label is created** page select **Do Nothing** then select **Done**.

You have successfully created an event-based retention label.

## Task 2 – Publish event-driven retention label

In this task, you will publish the Project Asset retention label, making it available for users to apply to relevant documents in SharePoint and OneDrive.

- [ ] You should still be logged into Client 1 VM (SC-400-CL1) as the **SC-400-cl1\admin** account, and you should be logged into Microsoft Purview as **Joni Sherman**.
- [ ] You should still be on the **File plan** page within Microsoft Purview. If not, navigate to `https://purview.microsoft.com`, then select **Solutions** > **Records Management** > **File plan**.
- [ ] Select the **Project Asset** label, then select the **Publish labels** button ( ).
    
    [![](https://raw.githubusercontent.com/riswinto/SC-400T00A-Microsoft-Information-Protection-Administrator/master/Instructions/Media/publish-labels-icon.png)](https://raw.githubusercontent.com/riswinto/SC-400T00A-Microsoft-Information-Protection-Administrator/master/Instructions/Media/publish-labels-icon.png)
    
- [ ] On the **Choose labels to publish** page, ensure the **Project Asset** retention label is selected, then select **Next**.
- [ ] On the **Policy Scope** page, select **Next**.
- [ ] On the **Choose the type of retention policy to create** page, select **Static**, then select **Next**.
- [ ] On the **Choose where to publish labels** page select **Let me choose specific locations** to display the location options.
- [ ] On the **Choose where to publish labels** page select **Let me choose specific locations** and select:
    - SharePoint classic and communication sites
    - OneDrive accounts
    - Deselect all other locations
- [ ] Select **Next**.
- [ ] On the **Name your policy** enter:
    - **Name**: `Project Asset Retention Label`
    - **Description**: `Project Assets Retention label, retention period 5 years, SharePoint site locations.`
- [ ] Select **Next**.
- [ ] Review your settings on the **Finish** page, then select **Submit**.
- [ ] Once your retention label has been published, select **Done** on the **Your retention label was published** page.

You have successfully published the retention label for project assets.

## Task 3 – Apply label and add an asset ID

In this task, you'll apply the Project Asset retention label to a document and assign an asset ID, which will be used to trigger the retention period once the related project event occurs.

- [ ] You should still be logged into Client 1 VM (SC-400-CL1) as the **SC-400-cl1\admin** account, and you should be logged into Microsoft 365 as **Joni Sherman**.
- [ ] You should still be on the **File plan** page within Microsoft Purview. Select meatball menu in the top-left corner, then select **SharePoint** from the sub-menu.
    
    [![](https://raw.githubusercontent.com/riswinto/SC-400T00A-Microsoft-Information-Protection-Administrator/master/Instructions/Media/show-more-actions-sharepoint.png)](https://raw.githubusercontent.com/riswinto/SC-400T00A-Microsoft-Information-Protection-Administrator/master/Instructions/Media/show-more-actions-sharepoint.png)
    
- [ ] Search for `Brand` in the search bar on the top, then select the **Brand** SharePoint page from the search results.
- [ ] On the top navigation pane, select **Documents**.
- [ ] Within the documents folder, hover over the **Customer Product Survey.xlsx** document and select the ellipses **…** for **Show more actions** to open the menu to show more options, then select **Details**.
- [ ] In the right-side panel, under **Properties** select **Apply label**, then select the **Project Asset** label.

> Note: Retention labels might take 1-2 days to appear in SharePoint. If the Project Asset label isn't available during this task, you can revisit and apply the label later.

- [ ] In the newly appeared **Asset ID** field enter `**NewProductLaunch**` and close the right-side menu by selecting **X** in the top right corner.
    
    [![](https://raw.githubusercontent.com/riswinto/SC-400T00A-Microsoft-Information-Protection-Administrator/master/Instructions/Media/event-based-retention-with-asset-id.png)](https://raw.githubusercontent.com/riswinto/SC-400T00A-Microsoft-Information-Protection-Administrator/master/Instructions/Media/event-based-retention-with-asset-id.png)
    

You've successfully applied the Project Asset label and assigned an Asset ID to a document. This setup will initiate the retention process when the project closure event occurs.

## Task 4 – Create specific event

In this task, you'll create a specific event to mark the closure of a project, triggering the retention period for all labeled documents.

- [ ] You should still be logged into Client 1 VM (SC-400-CL1) as the **SC-400-cl1\admin** account, and you should be logged into Microsoft 365 as **Joni Sherman**.
- [ ] In **Microsoft Edge**, navigate to `**https://purview.microsoft.com**`, then select **Solutions** > **Records Management** from the left sidebar.
- [ ] On the **Records Management** page, select **Events** from the left sidebar.
- [ ] On the **Events** page, select **+ Create**.
- [ ] On the **Name the event** flyout panel on the right, enter:
    - **Name**: `New Product Launch Closed`
    - **Description**: `Assets with the Project Asset label and AssetID NewProductLaunch will enter their retention period.`
- [ ] Select **Next**.
- [ ] On the **Event settings** page, select **Use event type** then select **Choose an event type**.
- [ ] On the **Choose an event type** page, select **Project Closure**, then select **Add**.
- [ ] Select **Next** on the flyout panel.
- [ ] On the **Event settings** page, set **Asset IDs for items in SharePoint and OneDrive** to `**NewProductLaunch**`.
- [ ] Select today's date for **When did this event occur?**, then select **Next**.
- [ ] Review the **Finish** page then select **Submit**.
- [ ] On the **Your event has been created** page select **Done**.

You have successfully triggered an event and started the retention period for all documents with the Project Asset label and an Asset ID of NewProductLaunch.

## Task 5 – Observe results of event trigger

To verify that the retention period you specified started, you need to try to delete the file.

- [ ] You should still be logged into Client 1 VM (SC-400-CL1) as the **SC-400-cl1\admin** account, and you should be logged into Microsoft 365 as **Joni Sherman**.
- [ ] In Microsoft Edge, you should still be on the **Events** page for records management in the Microsoft Purview portal.
- [ ] In the top left corner select the nine dots and under **Apps** select **SharePoint**.
- [ ] Search for `Brand` in the search bar on the top, then select the **Brand** SharePoint page from the search results.
- [ ] In the top navigation pane, select **Documents**.
- [ ] On the **Documents** page, select the checkbox for **Customer Product Survey.xlsx**, then select the horizontal ellipses, **…** to open the action menu"
- [ ] From the action menu, select **Delete** and observe the results. You should be blocked from deleting this file due to policy.
    
    [![](https://raw.githubusercontent.com/riswinto/SC-400T00A-Microsoft-Information-Protection-Administrator/master/Instructions/Media/retention-label-blocked-delete.png)](https://raw.githubusercontent.com/riswinto/SC-400T00A-Microsoft-Information-Protection-Administrator/master/Instructions/Media/retention-label-blocked-delete.png)
    

You have successfully confirmed that the retention period on the document has started. If you can still delete the document the synchronization period for the event has not been completed and the triggering of the retention policy is still in progress. As with other Retention Labels, this process can take up to 1-2 days to complete.

# Lab 3 - Exercise 4 - Configure service-based retention

Contoso Ltd. has recently experienced some internal challenges, and there is concern that a potentially disgruntled employee might attempt to delete critical company data. As Joni Sherman, the Compliance Admin for Contoso Ltd., you have been tasked with securing sensitive information and ensuring that no vital records are lost. The legal department has identified specific areas where data might be at risk, and your role is to implement measures to prevent data loss, particularly focusing on email communications and SharePoint documents.

**Tasks**:

- [ ] Configure mailbox holds
- [ ] Recover SharePoint documents

## Task 1 – Configure mailbox holds

To prevent data loss, you'll place a mailbox hold on Alex Wilber's account.

- [ ] Log into Client 1 virtual machine (SC-400-CL1) as the **SC-400-cl1\admin** account.
- [ ] In **Microsoft Edge**, navigate to `**https://admin.exchange.microsoft.com**` and log into the Exchange Admin Center as **Joni Sherman**. Sign in as `JoniS@WWLx549660.onmicrosoft.com`
- [ ] Close all tip windows if any appear.
- [ ] In the Exchange Admin Center, in the left sidebar, expand **Recipients** then select **Mailboxes**.
- [ ] Select **Alex Wilber** from the list of mailboxes, and a flyout panel on the right displaying Alex's mailbox settings will appear.
- [ ] On **Alex Wilber**'s flyout page, select the **Others** tab.
- [ ] Under **Litigation hold** select **Manage litigation hold**.
- [ ] On the **Manage litigation hold** page, set the **Litigation hold** from **Off** to **On** to display the litigation hold settings.
- [ ] Use these values to configure the litigation hold for Alex's mailbox:
    - **Hold duration (days).**: `90`
    - **Note (visible to the user)**: `Your mailbox has been put on hold for the next 90 days. You will not be able to delete any messages.`
- [ ] Select **Save** at the bottom of the panel. In the panel, you'll get a message stating **Litigation hold updated** should appear.

You have successfully activated the Mailbox Hold on a mailbox in your environment and stopped everyone with access from permanently deleting any content in the mailbox. Applying the hold can take up to 60 minutes.

## Task 2 – Recover SharePoint documents

In this task, you'll delete and restore a deleted document to make sure you can restore documents the employee might delete after he is informed about the litigation hold against his mailbox.

- [ ] Log into Client 1 VM (SC-400-CL1) as the **SC-400-cl1\admin** account.
- [ ] In **Microsoft Edge**, navigate to `**https://www.office.com**` and log in Microsoft 365 as **Joni Sherman**.
- [ ] In the Microsoft Office 365 landing page, select the meatball menu in the top-left corner, then select **SharePoint** from the sub-menu.
    
    [![](https://raw.githubusercontent.com/riswinto/SC-400T00A-Microsoft-Information-Protection-Administrator/master/Instructions/Media/show-more-actions-sharepoint.png)](https://raw.githubusercontent.com/riswinto/SC-400T00A-Microsoft-Information-Protection-Administrator/master/Instructions/Media/show-more-actions-sharepoint.png)
    
- [ ] On the SharePoint landing page, search for `Benefits` then select **Benefits @ Contoso** from the search results.
- [ ] In the left sidebar select **Documents**.
- [ ] On the **Documents** page, select the checkbox to the left of **Vacation Policies.pptx** then select **Delete** from the action bar.
- [ ] On the **Delete?** dialog, select **Delete**.
- [ ] On the left sidebar, select **Recycle bin**.
- [ ] On the **Recycle bin** page, right click **Vacation Policies.pptx**, then select **Restore**.
- [ ] On the left sidebar, select **Documents** and notice the file has been restored.

You have successfully recovered a deleted document from a SharePoint Site.