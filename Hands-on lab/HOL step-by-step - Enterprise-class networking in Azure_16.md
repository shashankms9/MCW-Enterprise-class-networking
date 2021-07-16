## Exercise 11: Using Network Watcher to Test and Validate Connectivity

Duration: 60 minutes

In this exercise, you will collect the flow log and perform connectivity from your simulated on-premises environment to Azure. This will be accomplished by using the Network Watcher Service in the Azure Platform.

### Task 1: Configuring the Storage Account for the NSG Flow Logs

1. On the Azure portal select **+ Create a resource**. From the Azure Marketplace menu select **storage** then select **Storage Account**

2. On the **Create Storage account** blade. Enter the following information, and select **Review + Create** then select the **Create** button:

    -  Subscription: **Your Subscription**

    -  Resource Group: **MonitoringRG** (Use the existing resource group created earlier.)

    -  Storage Account Name: **This must be Unique and alphanumeric, lowercase and no special characters.**

    -  Location: **South Central US**

    -  Performance: **Standard**

    -  Redundancy: **Locally-redundant storage (LRS)**

    ![The create storage account blade with the above configuration values set.](images/Hands-onlabstep-by-step-Enterprise-classnetworkinginAzureimages/media/image186.png "Add storage account")

   >**Note:** Ensure the storage account is created before continuing.

3. Repeat step 2, but select **East US** for the region and give it a different name.

4. On the Azure portal select **All services** at the left navigation. From the Categories menu select **Networking** then select **Network Watcher**.

5. From the **Network Watcher** blade under the **Logs** menu select **NSG flow logs**. You will see both the **OnPremVM-nsg** and **WGAppNSG1** Network Security Groups.

    ![The NSG Flow logs blade listing the network security groups. The status for both NSGs is shows as disabled.](images/Hands-onlabstep-by-step-Enterprise-classnetworkinginAzureimages/media/image185.png "Network Security Groups in Flow Log")

6. Select the **WGAppNSG1** network security group to open the flow log settings. Select **On** and then select **Version 2** for the Flow logs version.

7. Select **Storage Account-Configure**. From the drop down select the available storage account created earlier, then the **OK** button.

    ![The select a storage account blade with the storage account selected in the NSG Flow logs blade.](images/Hands-onlabstep-by-step-Enterprise-classnetworkinginAzureimages/media/image187.png "Network Watcher Flow Log Settings")

8. Select **On** to enable the traffic analytics status and set the interval to 10 minutes. Select the **Log Analytics Workspace** created earlier. Select **Save** at the top to confirm the settings.  

    ![Flow logs Settings blade, with the configuration set to on, Traffic Analytics status set to on, the processing interval set to every 10 minutes, the log analytics workspace selected and the save button highlighted.](images/Hands-onlabstep-by-step-Enterprise-classnetworkinginAzureimages/media/image188.png "Network Watcher Flow Log Settings")

9.  Repeat Steps 4 - 7 to enable the **OnPremVM-nsg** Network Security Group as well. When completed your configuration should show as the following image.

     ![The NSG Flow logs blade listing the network security groups. Both NSGs show a status of enabled.](images/Hands-onlabstep-by-step-Enterprise-classnetworkinginAzureimages/media/image189.png "Network Watcher Flow Log")

10. Navigate back to the **OnPremVM**. Connect to it by downloading and opening the RDP file. Then open another RDP connection to the **WGWEB1** virtual machine within the connection to **OnPremVM**. In the RDP connection to **WGWEB1**, navigate to the load balancer's private ip (**10.8.0.100**) and generate some traffic by refreshing the browser. Allow ten minutes to pass for traffic analytics to generate.  

     ![CloudShop External and Internal web application.](images/Hands-onlabstep-by-step-Enterprise-classnetworkinginAzureimages/media/image190.png "CloudShop Application")

### Task 2: Configuring Diagnostic Logs

1. On the Azure portal, select **All services** at the left navigation. From the Categories menu select **Networking**, then **Network Watcher**,

2. Select **Diagnostic Logs** from the **Logs Menu** within the blade.

     ![Network Watcher Diagnostic Log Settings Blade. Under the Logs menu on the left, diagnostic logs is highlighted.](images/Hands-onlabstep-by-step-Enterprise-classnetworkinginAzureimages/media/image192.png "Network Watcher Diagnostic Log")

3. Select **onpremvm*NNN*** then select **+Add diagnostic setting**.

4. Enter **OnPremDiag** as the name then select the checkbox for **Archive to a storage account**. Select **Storage account** and from the drop down select the available storage account you created earlier. Select **OK**. 

     ![Network Watcher Diagnostic Log Settings Blade. The name, archive to storage account, and select storage account are highlighted. On the right the select storage account blade is shown with the name of the storage account highlighted.](images/Hands-onlabstep-by-step-Enterprise-classnetworkinginAzureimages/media/image193.png "Network Watcher Diagnostic Resources")

5. Select the **Send to Log Analytics** checkbox. Select the workspace created earlier. Select the **AllMetrics** checkbox and set the **Retention (days)** to **60**. Select the **Save** button to complete the settings.

     ![Network Watcher Diagnostic Log Settings Blade with the configurations above set.](images/Hands-onlabstep-by-step-Enterprise-classnetworkinginAzureimages/media/image194.png "Diagnostic Settings")

6. Repeat Steps 2 - 5 for each network resource. Once completed your settings will look like the following screenshot.

     ![Network Watcher Diagnostic Log Settings Blade. All diagnostic status are set to enabled.](images/Hands-onlabstep-by-step-Enterprise-classnetworkinginAzureimages/media/image195.png "Diagnostic Settings")

### Task 3: Reviewing Network Traffic

1. On the Azure portal select **All services** at the left navigation. From the Categories menu select **Networking** then select **Network Watcher**.

2. Select **Traffic Analytics** from the **Logs** menu in the blade. At this time the diagnostic logs from the network resources have been ingested. Select **View map**.

     ![Network Watcher Traffic Analytics Blade. The view map button in the middle of the page is highlighted.](images/Hands-onlabstep-by-step-Enterprise-classnetworkinginAzureimages/media/image196.png "Your Network Environment")

3. Select the **green check mark** which identifies your network. Within the pop-up menu select **More Details** to propagate detailed information of the flow to and from your network.

     ![The Traffic Analytics Geo Map View is shown with a green check mark on the region where your network resides and monitor metrics displayed next to it.](images/Hands-onlabstep-by-step-Enterprise-classnetworkinginAzureimages/media/image197.png "Your Network Environment")

>**Note:** You can select the **See More** link to query the connections detail for more information.

### Task 4: Network Connection Troubleshooting

1. On the Azure portal select **All services** at the left navigation. From the Categories menu select **Networking** then select **Network Watcher**.

2. Select **Connection Troubleshoot** from the **Network Diagnostic tools** menu.

3. To troubleshoot a connection or to validate the route enter the following information and select **Check**:
   
    -  Subscription: **Your Subscription**

    -  Resource Group: **OnPremVMRG**

    -  Source Type: **Virtual Machine**

    -  Virtual Machine: **OnPremVM**

    -  Destination: **Select a virtual machine**
 
    -  Resource Group: **WGVNetRG2**
 
    -  Virtual Machine: **WGWEB1**

    -  Probe Settings: **TCP**
    
    -  Destination Port: **80**

     ![Network Watcher Connection Troubleshoot Blade with the configuration values above set.](images/Hands-onlabstep-by-step-Enterprise-classnetworkinginAzureimages/media/image198.png "Connection Troubleshoot")

4. Once the check is complete the connection troubleshoot feature will display a grid view on the name, IP Address Status and Next hop as seen in the following screenshot. 

     ![Network Watcher Connection Troubleshoot Blade with the name, IP Address Status and Next hop shown with a green check mark in the status column.](images/Hands-onlabstep-by-step-Enterprise-classnetworkinginAzureimages/media/image199.png "Connection Troubleshoot")

