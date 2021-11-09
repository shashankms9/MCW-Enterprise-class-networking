## Exercise 4: Create route tables with required routes

Duration: 15 minutes

Route Tables are containers for User Defined Routes (UDRs). The route table is created and associated with a subnet. UDRs allow you to direct traffic in ways other than normal system routes would. In this case, UDRs will direct outbound traffic via the Azure firewall.

### Task 1: Create route tables

1.  On the main portal menu, select **+ Create a Resource**. Type **route** into the search box, and select **Route table** then select **Create**.

2.  On the **Create a Route table** blade enter the following information:

    -  Subscription: **Select your subscription**.

    -  Resource group: Select **WGVNetRG1** from the drop down.
    
    -  Name: **MgmtRT**

    -  Region: **(US) South Central US**

    -  Propagate gateway routes: **Yes**

3.  When the dialog looks like the following screenshot, select **Create**.

    ![This represents completed fields when initially creating a route table.](images/Hands-onlabstep-by-step-Enterprise-classnetworkinginAzureimages/media/image163.png "Create route table")

4.  Repeat steps 1 and 2 to create the **AppRT** route table:

    -  Subscription: **Select your subscription**.

    -  Resource group: Select **WGVNetRG2** from the drop down.
    
    -  Name: **AppRT**

    -  Region: **(US) South Central US**

    -  Propagate gateway routes: **Yes**

5.  Once route tables are created, your **Route tables** blade should look like the following screenshot:

    ![Route Table listing showing the two route tables that were just created.](images/Hands-onlabstep-by-step-Enterprise-classnetworkinginAzureimages/media/image38.png "Route table link")

### Task 2: Add routes to each route table

1.  Select the **AppRT** route table, and select **Routes** under **Settings** on the left.

    ![On the Route table menu, under Settings, Routes is selected. ](images/Hands-onlabstep-by-step-Enterprise-classnetworkinginAzureimages/media/image39.png "Route table blade ")

2.  On the **Routes** blade, select **+ Add**. Enter the following information, and select **OK**:

    -  Route name: **AppToInternet**

    -  Address prefix: **0.0.0.0/0**

    -  Next hop type: **Virtual appliance**

    -  Next hop address: **10.7.1.4**

    ![The Add route blade is shown with the AppToInternet route being added with the above configurations.](images/Hands-onlabstep-by-step-Enterprise-classnetworkinginAzureimages/media/image40.png "Add route configuration")

3.  Repeat this procedure to add the **AppToMgmt** route using the following information:

    -  Route name: **AppToMgmt**

    -  Address prefix: **10.7.0.8/29**

    -  Next hop type: **Virtual appliance**

    -  Next hop address: **10.7.1.4**

    ![The Add route blade is shown with the AppToInternet route being added with the above configurations.](images/Hands-onlabstep-by-step-Enterprise-classnetworkinginAzureimages/media/image41.png "Edit route")

4.  Upon completion, your routes in the **AppRT** route table should look like the following screenshot:

    ![AppRT route table is shown with the AppToInternet and AppToMgmt routes shown in the table.](images/Hands-onlabstep-by-step-Enterprise-classnetworkinginAzureimages/media/image43.png "Route table ")

5.  In the Azure Portal, go to All Services and type Route in the search box and select **Route tables**.

6.  Select **MgmtRT**, and select **Routes** under **Settings** on the left.

    ![The Routes blade is shown and Under Name, the MgmtRT route is selected.](images/Hands-onlabstep-by-step-Enterprise-classnetworkinginAzureimages/media/image50.png "MgmtRT")

7.  On the **Routes** blade, select +**Add**. Enter the following information, and select **OK**:

    -  Route name: **MgmtToOnPremises**

    -  Address prefix: **192.168.0.0/16**

    -  Next hop type: **Virtual network gateway**

    -  Next hop address: **Leave blank**.

    ![The Add route blade of the MgmtRT route is shown with the configuration values above filled in.](images/Hands-onlabstep-by-step-Enterprise-classnetworkinginAzureimages/media/image51.png "Add route")

8.  Add the **MgmtToApp** route using the following information:

    -  Route name: **MgmtToApp**

    -  Address prefix: **10.7.2.0/25**

    -  Next hop type: **Virtual appliance**

    -  Next hop address: **10.7.1.4** (This is the private IP of Azure Firewall.)

    ![The Add route blade of the MgmtRT route is shown with the configuration values above filled in.](images/Hands-onlabstep-by-step-Enterprise-classnetworkinginAzureimages/media/image164.png "Add route")

9.  Upon completion, your routes in the **MgmtRT** route table should look like the following screenshot:

    ![The MgmtRT route table with the MgmtToApp and MgmtToOnPremises routes added to the table.](images/Hands-onlabstep-by-step-Enterprise-classnetworkinginAzureimages/media/image165.png "Route table")

    >**Note:** The route tables and routes you have just created are not associated with any subnets yet, so they are not impacting any traffic flow yet. This will be accomplished later in the lab.

