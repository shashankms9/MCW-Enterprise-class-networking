## Exercise 1: Create a Virtual Network and provision subnets

Duration: 15 minutes

### Task 1: Create a Virtual Network

1.  From your **LABVM**, connect to the Azure portal, select **+ Create a resource**, and in the **Search the Marketplace** box, search for and select **Virtual network** and select **Create**. 

2.  On the **Create virtual network** blade, on the **Basic** tab, enter the following information:

    -  Subscription: **Select the subscription available**
  
    -  Resource group: **WGVNetRG1** from the drop-down option

    -  Name: **WGVNet1**

    -  Location: **(US) South Central US**

3.  Select **Next: IP Addresses**

    ![The create virtual network basic dialog is displayed. The configuration options specified in the previous step are highlighted. ](images/Hands-onlabstep-by-step-Enterprise-classnetworkinginAzureimages/media/20201112virtualnetworkbasic.png "Create virtual network: Basics")
   
4.  On the **Create virtual network IP Addresses** tab, enter the following information:

    -  IPv4 Address space: **10.7.0.0/20**

    - Select **+ Add subnet** then enter the following information and select **Add**. 

    - Subnet name: **GatewaySubnet**

    - Subnet address range: **10.7.0.0/29**

    -  Address space: **10.7.0.0/20**

    -  Subnet name: **GatewaySubnet** (Select the **default** name and change to this name.)

    -  Subnet address range: **10.7.0.0/29**

5.  Select **Next: Security**.

    ![The create virtual network IP addresses dialog is displayed. The configuration options specified in the previous step are highlighted. ](images/Hands-onlabstep-by-step-Enterprise-classnetworkinginAzureimages/media/20201112virtualnetworkipaddresses.png "Create virtual network: IP Addresses")

6.  On the **Create virtual network Security** tab, select **Enable** for BastionHost.

7.  Enter the following information:

    -  Bastion Host: **Enable**

    -  Bastion name: **WGBastion**

    -  AzureBastionSubnet address space: **10.7.5.0/24**

    -  Public IP address: **Create new**
  
    -  Public IP address name: **BastionPublicIP**

8.  Leave the other options as default for now.

    ![The create virtual network security dialog is displayed. The configuration options specified in the previous step are highlighted. ](images/Hands-onlabstep-by-step-Enterprise-classnetworkinginAzureimages/media/20201112virtualnetworksecurity.png "Create virtual network: Security")

9.  Select **Review + Create**.

10. Review the configuration and select **Create**.

    ![The create virtual network review + create dialog is displayed. The configuration options specified in the previous step are highlighted. ](images/Hands-onlabstep-by-step-Enterprise-classnetworkinginAzureimages/media/20201112virtualnetworkreview.png "Create virtual network: Review + create")

11. Monitor the deployment status by selecting **Notifications Bell** at the top of the portal. In a minute or so, you should see a confirmation of the successful deployment. Select **Go to Resource**.

### Task 2: Configure subnets

1.  Go to the WGVNetRG1 Group, and select **WGVNet1 Virtual Network** blade if you're not there already, and select **Subnets** under **Settings** on the left.

    ![In the Virtual Network blade, under Settings, Subnets is selected.](images/Hands-onlabstep-by-step-Enterprise-classnetworkinginAzureimages/media/image28.png "Virtual Network blade")

2.  In the **Subnets** blade select **+Subnet**.

    ![In the Subnets blade, the add Subnet button is selected.](images/Hands-onlabstep-by-step-Enterprise-classnetworkinginAzureimages/media/image29.png "Subnets blade")

3.  On the **Add subnet** blade, enter the following information:

    -  Name: **Management**

    -  Address range: **10.7.2.0/25**

    -  Network security group: **None**

    -  Route table: **None**

    -  Service Endpoints: **Leave as Default**.

4.  When your dialog looks like the following screenshot, select **Save** to create the subnet.

    ![Field values in the Add Subnet blade are set to the previously defined settings.](images/Hands-onlabstep-by-step-Enterprise-classnetworkinginAzureimages/media/image30.png "Add Subnet blade")

5. Repeat Step 3, enter the following information for the Azure Firewall which we will use to control traffic flow in and out of the Network and click on **Save**.

    -  Name: **AzureFirewallSubnet** (This name is fixed and cannot be changed.)

    -  Address range: **10.7.1.0/24**

    -  Network security group: **None**

    -  Route table: **None**

    -  Service Endpoints: **Leave as Default**

    ![Field values in the Add Subnet blade are set to the previously defined settings.](images/Hands-onlabstep-by-step-Enterprise-classnetworkinginAzureimages/media/image159.png "Add Subnet blade")

