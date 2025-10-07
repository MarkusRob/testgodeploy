PAGE 1
===
test
===
#### Lab 1 - Create a virtual machine in the portal

`singleBacktick`
```tripleBacktick```

::: secondary
**Scenario**

In this walkthrough, we will create a virtual machine in the Azure Portal, connect to the virtual machine, install the web server role and test. 
:::

::: warning
**Note**: Take time during this walk-through to click and read the Informational icons. 
:::


##### Task 1: Create the virtual machine


::: secondary
In this task, we will create a Windows Server virtual machine in Azure. 
:::
===
1. [ ] If necessary, send the **$gd.fn.sendVmKeyCombo(CTRL+ALT+DEL)** command and then sign in to the **$gd.fn.selectVm(LON-CL1)** as virtual machine as **[`Admin`](urn:gd:lg:a:send-vm-keys)** with the password **[`Pa55w.rd`](urn:gd:lg:a:send-vm-keys)**. 

1. [ ] Once logged in, open your choice of web browser and sign in to the **Azure portal** by navigating to **[https://portal.azure.com](urn:gd:lg:a:send-vm-keys)** and entering the following Azure Credentials:

    - Username: **[`$gd.com(azure).username`](urn:gd:lg:a:send-vm-keys)**
    - Password: **[`$gd.com(azure).password`](urn:gd:lg:a:send-vm-keys)**


2. [ ] On **Stay signed in?** select **Yes**.

3. [ ] From the **All services** blade in the Portal Menu, search for and select **Virtual machines**, and then click **+Create** and choose **+Azure Virtual machine** from the drop down.

3. [ ] On the **Basics** tab, fill in the following information (leave the defaults for everything else):

    | Settings | Values |
    |  -- | -- |
    | Subscription | **$gd.com(azure).subscriptionName** |
    | Resource group | **$gd.com(azure).resourceGroups(myRGVM)** |
    | Virtual machine name | **[`myVM`](urn:gd:lg:a:send-vm-keys)** |
    | Region | **(US) East US**|
    | Availability options | No infrastructure redundancy required|
    | Security type | Standard | 
    | Image | **Windows Server 2019 Datacenter - x64 Gen2**|
    | Size | **Standard D2s v3**|
    | Administrator account username | **[`azureuser`](urn:gd:lg:a:send-vm-keys)** |
    | Administrator account password (type in carefully!) | **[`$gd.com(azure).password`](urn:gd:lg:a:send-vm-keys)** |
    | Public inbound port  | **Allow select ports** |
    | Select inbound ports | **RDP (3389)** and **HTTP (80)**| 
4. [ ] Switch to the **Networking** tab, and look for the **Select inbound ports**:

    ::: warning
    **Note** - Verify that both port 80 and 3389 are selected.
    :::

    | Settings | Values |
    | -- | -- |
    | Select inbound ports | **HTTP (80), RDP (3389)**|



5. [ ] Switch to the **Monitoring** tab and select the following setting:

    | Settings | Values |
    | -- | -- |
    | Boot diagnostics | **Disable**|

6. [ ] Leave the remaining defaults and then click the **Review + create** button at the bottom of the page.

7. [ ] Once Validation is passed click the **Create** button. 

    ::: warning
    **Note**: It can often take anywhere from five to seven minutes to deploy the virtual machine.
    :::


8. [ ] You will receive updates on the deployment page and via the **Notifications** area (the bell icon in the top menu).

    ::: info
    **Verify Port 80 and 3389 were opened**
    :::

##### Task 2: Connect to the virtual machine

1. [ ] Click on bell icon from the upper blue toolbar, and select **Go to resource** when your deployment has succeded. 

    ::: warning
        **Note**: You could also use the **Go to resource** link on the deployment page 
    :::

2. [ ] On the virtual machine **Overview** blade, click the **Connect** button.

    ::: warning
    **Note**: The following directions tell you how to connect to your VM from a Windows computer. On a Mac, you need an RDP client such as this Remote Desktop Client from the Mac App Store and on Linux virtual machine you could connect directly from a bash shell using `ssh`.
    :::


2. [ ] On the **myVM | Connect** page, scroll down and click on **Select** under **Native RDP**.

3. [ ] In the pane that appears, select **Download RDP file** under step 3. Open the file once downloaded and click **Connect**.

    ![Screenshot](https://gdlabresourceseastus01.blob.core.windows.net/labguideimages/AZ-900T00/All-Labs/020b314c-3278-4e2f-bc9e-24cd2a4f13af.png)

4. [ ] In the **Windows Security** window, sign in using the Admin Credentials you used when creating your VM **[`azureuser`](urn:gd:lg:a:send-vm-keys)** and the password **[`$gd.com(azure).password`](urn:gd:lg:a:send-vm-keys)**. 

5. [ ] You may receive a warning certificate during the sign-in process. Click **Yes** or to create the connection and connect to your deployed VM. You should connect successfully.


::: success
**Congratulations**! You have deployed and connected to a Windows Server virtual machine in Azure
:::

##### Task 3: Install the web server role and test

::: secondary
In this task, install the Web Server role on the server on the Virtual Machine you just created and ensure the default IIS welcome page will be displayed. 
:::

1. [ ] In the newly opened virtual machine, launch PowerShell by searching **[`PowerShell`](urn:gd:lg:a:send-vm-keys)** in the search bar, when found right click **Windows PowerShell** to **Run as administrator**.

    ![Screenshot](https://gdlabresourceseastus01.blob.core.windows.net/labguideimages/AZ-900T0Xv2-(CS)/Lab-1/a9cc6a14-acb4-4df4-ba2b-2d8d350292ac.png)

2. [ ] In PowerShell, install the **Web-Server** feature on the virtual machine by running the following command. 

    ```PowerShell
    Install-WindowsFeature -name Web-Server -IncludeManagementTools
    ```

3. [ ] When completed, a prompt will state **Success** with a value **True**. You do not need to restart the virtual machine to complete the installation. Close the RDP connection to the VM by clicking the **x** on the blue bar at the top center of your virtual machine. You can also minimize it by clicking the **-** on the blue bar at the top center.

    ![Screenshot](https://gdlabresourceseastus01.blob.core.windows.net/labguideimages/AZ-900T0Xv2-(CS)/Lab-1/26208d15-f3a0-443b-952d-9bdb6173160a.png)

4. [ ] Back in the portal, navigate back to the **Overview** blade of myVM and, use the **Copy to clipboard** button to copy the public IP address of myVM, then open a new browser tab, paste the public IP address into the URL text box, and press the **Enter** key to browse to it.

    ![Screenshot](https://gdlabresourceseastus01.blob.core.windows.net/labguideimages/AZ-900T0Xv2-(CS)/Lab-1/599bcece-663f-49a9-aa87-4263539cb94b.png)

5. [ ] The default IIS Web Server welcome page will be displayed.

    ![Screenshot](https://gdlabresourceseastus01.blob.core.windows.net/labguideimages/AZ-900T0Xv2-(CS)/Lab-1/a2553b64-7bd1-48b8-96b9-74fcf6a38b70.png)

::: success
**Congratulations!** You have created a new VM running a web server that is accessible via its public IP address. If you had a web application to host, you could deploy application files to the virtual machine and host them for public access on the deployed virtual machine.
:::



/page 
$gd.lab.courseName
asdasdas
/page




![Free Tom Smacking his Head](./media/Image.jpg)






# Lab 1 - Preparing your lab environment

## Exercise 1: Preparing the lab environment

## Task 1: Ensure the VMs are ready

Hyper-V Integration Services must be installed and running on guest VMs
in order for discovery to identify the apps installed on them.

1.  Login to the provided VM using the credential provided on the **Resources** tab of the Lab interface.

    ![](./media/image61.png)

1.  Open the **Microsoft Edge** from the desktop, then go to the IP
    address of **RHEL-WEB-01**: `192.168.1.24`

    ![A screenshot of a computer Description automatically
    generated](./media/image1.png)

2.  **RHEL-WEB-01** serves a Drupal website that is configured to make
    calls to a database that is hosted on **RHEL-DB-01**. Successfully
    loading the website confirms that both VMs are functioning
    correctly.

## Task 2: Create an Azure Migrate project

1.  In a new Edge tab, navigate to Azure Portal `https://portal.azure.com` , and sign in
    using the credentials provided in the Lab resources

2.  In the Azure portal, in the **Search** box, enter `Azure Migrate`
    then select **Azure Migrate** to go to the Azure Migrate page.

3.  In the left navigation, under **Migration goals**, select **Servers,
    databases and web apps**.

    ![A screenshot of a computer Description automatically
    generated](./media/image2.png)

4.  On the **Servers, databases and web apps** blade, select **Create
    project** in the middle of the page.

5.  On the **Create project** blade, use the following settings to
    create a new project.

    Use the default values for any setting not specified in the table.

    Resource group – click on **Create new** `AZMigrateRG`

    Project - `az-migrate-@lab.LabInstance.Id`

    Geography - **United States**

6.  Select **Create**.

7.  Wait for the deployment to complete before proceeding to the next
    task.

## Task 3: Deploy and configure the Azure Migrate appliance

1.  On the **Servers, databases and web apps** blade, in
    the **Assessment Tools** section, under **Azure Migrate: Discovery and assessment**, select **Discover** and choose **Using appliance**

    ![](./media/image3.png)

2.  On the **Discover** blade, on the **Are your Machines virtualized?** menu, select **Yes, with Hyper-V**.

3.  Under **1. General product key**, in the **Name your
    appliance** box, enter `HV-@lab.LabInstance.Id`, then select **Generate key**.

    >**Note** - The key-generation process can take up to 2 minutes to complete.

4.  Once the key is generated, select the **copy icon** on the **Project
    key** field.

    ![](./media/image4.png)

5.  Under **2. Download Azure Migrate appliance**, select **.zip file.
    500MB**, and *note* the Download button\*.

    <font color=Green>

    > **This would download the PowerShell script that installs the appliance to a Windows Server machine.** 
    
    >For this Lab, the script has **already been downloaded** to the E: drive and **run**. You will **continue past this step**.
    
    </font>

6.  Under **3. Set up the appliance**

7.  Minimize the Edge window, then select the **Azure Migrate Appliance
    Configuration Manager** shortcut on the desktop.

8.  Once the **Azure Migrate Appliance Configuration Manager** page
    loads, you may need to accept the EULA. Select **Accept** if
    prompted.

9.  On the **Azure Migrate Appliance Configuration Manager** page, in
    the **Register Hyper-V appliance by pasting the key here** box,
    paste the key you copied earlier.

10. Select **Verify**.

11. Select **Login**. A modal will appear asking you to **Continue with
    Azure Login**.

12. Select **Copy code & Login** and sign in to your subscription by
    pasting the device code, then selecting your username.

13. When prompted **Are you trying to sign in to Microsoft Azure
    PowerShell?**, select **Continue** and close the newly opened
    browser tab.

14. On the **Azure Migrate Appliance Configuration Manager** page, wait
    for registration to complete.

    ![](./media/image5.png)

    <font color=Green>

    > **It can take up to 10 minutes for registration to complete.** </font>

15. In the **Provide Hyper-V host credentials** section, select **Add
    credentials** and add credentials with the following settings:

    - Friendly Name - `Hypervisor`

    - User Name - `Administrator`

    - Password - `Passw0rd! `

16. In the **Provide Hyper-V host/cluster details** section,
    select **add a discovery source**, then select **Add single
    item** and use the following settings:

    - Discovery source - **Hyper-V Host/Cluster**

    - IP address FQDN - `win-msite54sfl9`

    - Map credentials - **Hypervisor**

17. In the **Provide server credentials to perform software
    inventory** section, ensure that the slider is **enabled**, then add
    credentials with the following settings:

    - Credentials type - **Linux (Non-domain)**

    - Friendly Name - `RHELUser`

    - User Name - `fetch6474`

    - Password - `RHELWorkshop`

18. Select **Start discovery**.

19. Leave Edge open for the next exercise. Discovery will continue
    processing.

# Exercise 3: Create a Business case and run an assessment

## Task 1: Create and review a business case

1.  In Azure portal, go back to the **Azure Migrate Servers, databases
    and web apps** page. Select **Refresh** to verify that your servers
    have been discovered.

    ![A screenshot of a computer Description automatically
    generated](./media/image17.png)

2.  In the **Azure Migrate: Discovery and assessment** section,
    select **Build business case**.

    ![A screenshot of a computer Description automatically
    generated](./media/image18.png)

3.  In the **Build business case** blade, use the following values to
    create the business case.

    - Business case name - `bc-43240741`

    - Target location - **West US**

    - Migration strategy - **Minimize migration time**

    - Savings options - **Reserved Instance + Azure Savings Plan**

    - Discount (%) on Pay as you go - **0**

    - Select **Build business case**.

    ![Business Case Refresh](./media/image19.png)

    > The business case can take up to 5 minutes to generate. If it has been more than 5 minutes, select **Refresh**.

4.  On the **bc-43240741** page, review the information indicating Azure readiness and monthly cost estimate for both compute and storage.

## Task 2: Configure, run, and view an assessment

1.  In a new tab navigate **Resource groups** page `https://portal.azure.com/#view/HubsExtension/BrowseResourceGroups.ReactView` select the **AZMigrateRG** resource group and then note down the location of the **Key Vault**, as shown below it is **West US 2**.
   ![](./media/image84.png)

    <font color=Orangered>

    > **Note** - This location would be required to be specified for other resources to be created later in the Lab, also to ensure the **Azure resources are created in the same region** to ensure the Migration is done smoothly.

    </font>

2.  Switch back to the **Azure Migrate** page and under **Azure Migrate: Discovery and assessment** section, select **Assess** and then, in the drop-down menu, select **Azure VM**.

    ![](./media/image20.png)

3.  On the **Create assessment** page, leave the dropdowns menus on
    their defaults.

4.  Select the **Edit** link next to **Assessment settings**,

    ![](./media/image21.png)

5.  On the Assessment Settings page, use the following settings to
    create the assessment.
    <font color=Green>
    > **Accept the default settings for anything not specified in the table.** </font>

    - Target location - **West US 2**

    - Storage type - **Premium managed disks**

    - Savings options - **None**

    - Sizing criteria - **As on premises**

    - VM series - **Dsv3_series**

    - Comfort factor - **1**

    - Offer - **Pay-As-You-Go**

    - Currency - **US Dollar ($)**

    - Discount - **0**

    - VM uptime - **31 Day(s) per month and 24 Hour(s) per day**

    - Already have a Windows Server license? - **No**

    - Security - **No**

6.  Select **Save** to return to Create Assessment, then select **Next:
    Select servers to assess \>**

7.  Use the following settings to create the server group and select the
    servers to be assessed.

    > Accept the default settings for anything not specified in the table.

    Assessment name - `as-43240741`

    Select or create a group - **Create new**

    Group name - `RHEL-Servers`

    List of machines to be added to the group - **RHEL-DB-01** and **RHEL-WEB-01**

8.  Select **Create assessment**. You will be redirected to the **Azure Migrate | Servers, databases and web apps** page.

9.  **Refresh** the page.

10. In the **Azure Migrate: Discovery and Assessment** section, verify that the **Assessments Total** equals **1**, then select **1**.

    ![](./media/image22.png)

11. On the **Azure Migrate: Discovery and Assessment |
    Assessments** page, select the newly created
    assessment **as-43240741**.

    ![](./media/image23.png)

12. On the **as-43240741** page, review the information indicating Azure
    readiness and monthly cost estimate for both compute and storage.

<font color=Green>

> **In real-world scenarios, you should consider installing the Dependency Agent to provide more insights into server dependencies during the
assessment stage.** </font>




