## Exercise 7: Configure Site-to-Site connectivity

Duration: 60 minutes

In this exercise, we will simulate an on-premises connection to the internal web application. To do this, we will first set up another Virtual Network in a separate Azure region followed by the Site-to-Site connection of the 2 Virtual Networks Finally, we will set up a virtual machine in the new Virtual Network to simulate on-premises connectivity to the internal load-balancer.

### Task 1: Create OnPrem Virtual Network

1.  In the Azure portal, select **+ Create a resource**, **Networking** and **Virtual network**.

2.  On the **Create virtual network** blade, enter the following information:

    -  Subscription: **Select your subscription**.

    -  Resource group: Select **OnPremVNetRG**.

    -  Name: **OnPremVNet**

    -  Region: **(US) East US** (Make sure this is **NOT** the same location you have specified in the previous exercises.)

3.  Leave the other options with their default values.

4.  Upon completion, it should look like the following screenshot and then click on **Review+Create** to validate the information is correct, and select **Next: IP Addresses**.

    ![The create virtual network blade is shown with the above configuration values specified and the create button highlighted.](images/onprem-vm.png "Create virtual network")

5. On the **IP addresses** tab of the **Create virtual network blade**, enter the following information.

    -  Address space: **192.168.0.0/16**

    - Select **+ Add subnet** then enter the following information in the blade that appears on the right and select **Add**.

      -  Subnet name: **default**

      -  Subnet address range: **192.168.0.0/24**
     
     ![The create virtual network blade is shown with the above configuration values specified and the create button highlighted.](images/onprem-vm-create.png "Create virtual network")

6. Select **Review + create** then **Create**.

### Task 2: Configure gateway subnets for on premise Virtual Network

1.  Select the **OnPremVnetRG** Resource Group and then open the **OnPremVNet** blade and select **Subnets**.

2.  Next, select **+ Gateway subnet**.

    ![The OnPremVNet subnet blade with Subnets highlighted in the menu and the + Gateway subnet highlighted.](images/Hands-onlabstep-by-step-Enterprise-classnetworkinginAzureimages/media/image122.png "Virtual network blade")

3.  Specify the following configuration for the subnet, and select **OK**:

    -  Address range: **192.168.1.0/29**

    -  Route table: **None** (We will add later.)

    ![The Add subnet blade of the OnPremVNet virtual network. The Address range with the above address range specified and the OK button highlighted.](images/Hands-onlabstep-by-step-Enterprise-classnetworkinginAzureimages/media/image123.png "Add subnet")

4.  Next, select **+ Subnet** and add **OnPremManagementSubnet** to the **OnPremVNet**, as shown below in the screenshot and select **Save**.

    - Name: **OnPremManagementSubnet**
  
    - Address range: **192.168.2.0/29**
  
    - Leave the rest of the values as their defaults. 

    ![The Add subnet blade of the OnPremVNet virtual network. The Name and Address range with the above address range specified and the OK button highlighted.](images/Hands-onlabstep-by-step-Enterprise-classnetworkinginAzureimages/media/image124.png "Add subnet")

### Task 3: Create the first gateway

1.  Using the Azure Management portal, select **+ Create a resource**, type **Virtual Network gateway** in the **Search the Marketplace** text box, in the list of results, select **Virtual network gateway**, and then select **Create**.

2.  On the **Create virtual network gateway** blade,  enter the following information and select **Review + create**:

    -  Subscription: **Select your subscription**.

    -  Name: **OnPremWGGateway**

    -  Region: **(US) East US** (This must match the location in which you created the **OnPremVNet** virtual network.)

    -  Gateway type: **VPN**

    -  VPN type: **Route-based**

    -  SKU: **VpnGw1**

    -  Virtual network: **OnPremVNet**

    -  Public IP address: **Create new**

    -  Public IP address name: **onpremgatewayIP1**

    -  Enable active-active mode: **Enabled**

    -  Second Public IP address name: **onpremgatewayIP2**

    -  Configure BGP ASN: **Disabled**

    ![The create virtual network gateway blade with the above configuation values set.](images/Hands-onlabstep-by-step-Enterprise-classnetworkinginAzureimages/media/image176.png "Create virtual network gateway")

3.  Validate your settings and select **Review + Create** then **Create**.

    >**Note:** The gateway will take 30-45 minutes to provision. Rather than waiting, continue to the next task.


### Task 4: Create the second gateway

1.  Using the Azure Management portal, select **+ Create a resource**, type **Virtual Network gateway** in the **Search the Marketplace** text box, in the list of results, select **Virtual network gateway**, and then select **Create**.

2.  On the **Create virtual network gateway** blade,  enter the following information and select **Review + create**:

    -  Subscription: **Select your subscription**.

    -  Name: **WGVNet1Gateway**

    -  Region: **(US) South Central US** (This must match the location in which you created the **WGVNet1** virtual network.)

    -  Gateway type: **VPN**

    -  VPN type: **Route-based**

    -  SKU: **VpnGw1**

    -  Virtual network: **WGVNet1**

    -  Resource group: **WGVNetRG1**

    -  Public IP address: **Create new**

    -  Public IP address name: **vnet1gatewayIP1**

    -  Enable active-active mode: **Enabled**

    -  Second Public IP address name: **vnet1gatewayIP2**

    -  Configure BGP ASN: **Disabled**

    ![The create virtual network gateway blade with the above configuration values set.](images/Hands-onlabstep-by-step-Enterprise-classnetworkinginAzureimages/media/image177.png "Create virtual network gateway")

3.  Validate your settings and select **Create**.

    >**Note:** The gateway will take 30-45 minutes to provision. You will need to wait until both gateways are provisioned before proceeding to the next section.

4.  The Azure portal will display a notification when the deployments have completed.

### Task 5: Connect the gateways

1.  In the Azure portal, select **+ Create a resource**, in the **Search the Marketplace** text box, type in **Connection**, and press **Enter**.

2.  On the **Connection** blade, select **Create**.

3.  On the **Basics** blade, enter the following information and select **Next:Settings>**

    -  Resource group: **WGVNetRG1**

    -  Connection type: **Vnet-to-Vnet**

    -  Establish bidirectional connectivity: **Enable**

    -  First connection Name: **WGVNet1Gateway-to-OnPremWGGateway**

    -  Second connection name: **OnPremWGGateway-to-WGVNet1Gateway**

    -  Region: **South Central US**

    ![The create connection blade with the basics tab selected. The configuration values are set to those in the instructions above.](images/createconnection1.png "Basics")

4.  On the Settings tab, enter the following information and click **Review + create** and then **Create**

    - First virtual network gateway: **WGVnet1Gateway**

    - Second virtual metwork gateway: **OnPremWGGateway**

    - Shared key (PSK): **AIB2C3D4**

    - IKE Protocol: **IKEv2**

    ![The create connection blade, on the Settings tab, select WGVNet1Gateway as the first virtual network gateway and OnPremWGGateway as the first virtual network gateway. Ensure Establish bidirectional connectivity is selected. Enter a Shared key, such as A1B2C3D4, for example.](images/createconnection2.png "select virtual network gateway")

5.  In the Azure portal, select **All services**. Then, type **connections** in the search text box and select **Connections**.

    ![In the Azure portal, Browse is selected. In the search field, connections is typed. In the results section, Connections is selected.](images/Hands-onlabstep-by-step-Enterprise-classnetworkinginAzureimages/media/image138.png "Azure Portal")

6.  Watch the progress of the connection status, and use the **Refresh** icon until the status changes for both connections from **Unknown** to **Connected**. This may take 5-10 minutes or more. You might need to refresh the page to see the change in status.

    ![The Connections tab showing the connection status as Connected. The refresh button at the top of the screen has been selected.](images/connections.png "Connections blade")

