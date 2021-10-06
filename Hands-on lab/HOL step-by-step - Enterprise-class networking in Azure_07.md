## Exercise 2: Virtual Network Peering

Duration: 20 Minutes

### Task 1: Configure VNet peering WGVNet1 to WGVNet2 and Vice Versa

1.  Select the resource group **WGVNetRG1**, and select the configuration blade for **WGVNet1**. Select **Peerings** under **Settings** on the left.

2.  Select **Add**.

    ![The WGVNet1 Virtual Network Peerings blade is shown. The add button is highlighted.](images/Hands-onlabstep-by-step-Enterprise-classnetworkinginAzureimages/media/image92.png "Virtual network blade")

3.  Set the following configuration for the new peering. Select **Add** to create the peering.

    - Peering link name (This virtual network): **VNETPeering_WGVNet1-WGVNet2**

    - Traffic to remote virtual network: **Allow (default)**

    - Traffic forwarded from remote virtual network: **Allow (default)**
  
    - Peering link name (Remote virtual network: **VNETPeering_WGVNet2-WGVNet1**

    - Virtual Network: **WGVNet2**

    - Traffic to remote virtual network: **Allow (default)**

    - Traffic forwarded from remote virtual network: **Allow (default)**

    ![The add peering blade is shown with the values above specified and highlighted. The OK button is highlighted.](images/Hands-onlabstep-by-step-Enterprise-classnetworkinginAzureimages/media/image171.png "WGVNet1 add peering blade")

