## Exercise 2: Virtual Network Peering

Duration: 20 Minutes

### Task 1: Configure VNet peering WGVNet1 to WGVNet2 and Vice Versa

1.  Select the resource group **WGVNetRG1**, and select the configuration blade for **WGVNet1**. select **Peerings** under **Settings** on the left.

2.  Select **Add**.

    ![The WGVNet1 Virtual Network Peerings blade is shown. The add button is highlighted.](images/Hands-onlabstep-by-step-Enterprise-classnetworkinginAzureimages/media/image92.png "Virtual network blade")

3.  Set the following configuration for the new peering. Select **OK** to create the peering.

    - Peering Name (WGVNet1 to WGVNet2): **VNETPeering_WGVNet1-WGVNet2**
  
    - Virtual Network: **WGVNet2**
  
    - Peering Name (WGVNet2 to WGVNet1): **VNETPeering_WGVNet2-WGVNet1**

    - Allow virtual network access from WGVNet1 to WGVNet2: **Enabled**
   
    - Allow virtual network access from WGVNet2 to WGVNet1: **Enabled** 

    - Allow forwarded traffic from WGVNet2 to WGVNet1: **Enabled**
  
    - Allow forwarded traffic from WGVNet1 to WGVNet2: **Enabled**

    ![The add peering blade is shown with the values above specified and highlighted. The OK button is highlighted.](images/Hands-onlabstep-by-step-Enterprise-classnetworkinginAzureimages/media/image171.png "WGVNet1 add peering blade")

