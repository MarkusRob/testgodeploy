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











