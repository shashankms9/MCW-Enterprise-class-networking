## Exercise 10: Create a Network Monitoring Solution

Duration: 15 minutes

### Task 1: Create a Log Analytics Workspace

1.  From your **LABVM**, connect to the Azure portal, select **+ Create a resource**, and in the list of Marketplace categories, select **IT & Management Tools** followed by selecting **Log Analytics**.

2.  On the **Create workspace** blade, enter the following information:

    -  Name: **Enter Unique Name all lowercase**

    -  Subscription: **Select your subscription**.

    -  Resource group: Select **Create new**, and enter the name **MonitoringRG**.

    -  Location: **East US**

    -  Pricing Tier: **Pay-as-you-go**

3.  Upon completion, it should look like the following screenshot. Validate the information is correct, and select **OK**.

    ![This represents the properly filled out fields when creating a Log Analytics Workspace.](images/Hands-onlabstep-by-step-Enterprise-classnetworkinginAzureimages/media/image160.png "Create Log Analytics Workspace")

### Task 2: Configure Network Watcher

1.  From your **LABVM**, connect to the Azure portal, select **All Services**, and in the Category list, select **Networking** followed by selecting **Network Watcher**.

    ![This is a Network Watcher configuration. On the left, networking is highlighted and numbered one, on the right, Network Watcher is highlighted and numbered two.](images/Hands-onlabstep-by-step-Enterprise-classnetworkinginAzureimages/media/image161.png "All Services blade")

2.  In the **Overview** blade, expand your subscription and select **SouthCentralUS** by selecting the **...** button to the right then enabling the service within the region.

3.   Repeat the step above this time enabling the service within the **East US** region.

   ![This is the Network Watcher blade where the enable region is selected. The Overview menu item is highlighted as step 1, the subscription name is highlighted as step 2 and the regions used in the lab are highlighted as step 3.](images/Hands-onlabstep-by-step-Enterprise-classnetworkinginAzureimages/media/image162.png "Network Watcher Overview blade")

