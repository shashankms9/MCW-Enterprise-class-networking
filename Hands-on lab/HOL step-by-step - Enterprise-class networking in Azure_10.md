## Exercise 5: Configure n-tier application and validate functionality

Duration: 20 minutes

In this exercise, you will create and configure a load balancer to distribute load between the web servers. 

### Task 1: Create a load balancer to distribute load between the web servers

1.  In the Azure portal, select **Load balancers** on the left navigation then select **+ Create**.

2.  On the **Create load balancer** blade, on the **Basics** tab, enter the following values:

    -  Subscription: **Select your subscription**.

    -  Resource group: **WGVNetRG2**

    -  Name: **WGWEBLB**

    -  Region: **South Central US**

    -  Type: **Internal**

    -  SKU: **Standard**

    Ensure your **Create load balancer** dialog looks like the following, and select **Next: Frontend IP configuration** then select **Create**.

    ![In this screenshot, the 'Create load balancer' blade is depicted with the required settings listed above selected along with the 'Next: Frontend IP configuration' button.](images/load-balancer-101.png "Create load balancer")

3. On the **Frontend IP configuration** tile, select **+ Add a frontend IP configuration and enter the following values:

    -  Name: **WGWEBLBIP**
  
    -  Virtual network: **WGVNet2**

    -  Subnet: **AppSubnet (10.8.0.0/25)**

    -  IP address assignment: Select **Static** and enter the IP address **10.8.0.100**.

    Ensure your **Create load balancer - Frontend IP configuration** dialog looks like the following, and select **Add**, **Review + create** then select **Create**.

    ![In this screenshot, the 'Frontend IP configuration' blade is depicted with the required settings listed above selected along with the 'Review + create' button.](images/load-balancer-102.png "Frontend IP configuration")

    >**Note**: **Backend pools** can now be configured within the **Create Load balancer** wizard.  For this exercise, we will complete this in the next task.

### Task 2: Configure the load balancer

1.  Open the **WGWEBLB** load balancer in the Azure portal.

2.  Select **Backend pools**, and select **+Add** at the beginning.

    ![In the Load balancer blade under Settings, Backend pools is selected, and the Add button is selected as well.](images/Hands-onlabstep-by-step-Enterprise-classnetworkinginAzureimages/media/image67.png "Load balancer blade")

3.  Enter **LBBE** for the pool name. Under **Associated to**, select **Virtual machine**.

    ![In the Name field in the Add backend pool blade is LBBE, and under Associated to, Virtual machine is selected.](images/2020-01-27-18-33-43.png "Add backend pool blade")

4.  Under **Virtual machine**, choose the **WGWEB1** virtual machine and private IP address, then for the second virtual machine choose the **WGWEB2** virtual machine and private IP address.

5.  Select **Add** to add the backend pool.

6.  Wait to proceed until the Backend pool configuration is finished updating.

    ![The WGWEBLB backend pools blade is shown. The two virtual machines in the backend pool show a status of running, indicating that the backend pool configuration is complete.](images/backendpool.png "Backend pool blade")

7.  Next, under **Settings** on the WGWEBLB Load Balancer blade select **Health Probes**. Select **+ Add**, and use the following information to create a health probe.

    ![Under Settings, Health probes is selected. In the Add health probe blade, HTTP displays in the Name field, and Protocol is set to HTTP.](images/Hands-onlabstep-by-step-Enterprise-classnetworkinginAzureimages/media/image73.png "Settings section, Add health probe blade")

8. Enter the following values:

    -  Name: **HTTP**

    -  Protocol: **HTTP**
    
    ![In the Add health probe blade, Name is HTTP, and Protocol is HTTP.](images/Hands-onlabstep-by-step-Enterprise-classnetworkinginAzureimages/media/image75.png "Add health probe blade")

8.  Select **Add**.

9.  After the Health probe has updated. Select **Load balancing rules**. Select **+Add** and complete the configuration as shown below followed by selecting **Add**.

    - Name: **HTTP**
  
    - FrontEnd ip address: **WGWEBLBIP(10.8.0.100)**
   
    - Protocol: **TCP**

    - Port: **80**   

    - Backend port: **80**

    - Backend pool: **LBBE**

    - Health probe: **HTTP(HTTP:80)**

    ![The add load balancing rule blade for the WGWEBLB load balancer is displayed with the name set to HTTP and all of the remaining configurations set to the default.](images/loadbalancer-5.png "Add load balancing rule")

    **It will take 2-3 minutes for the changes to save.**

10. Connect to WGWEB1 via Bastion, use the given credentials for login to WGWEB1 i.e, Username: **demouser** Password: **demo@pass123**. Open your browser and navigate to <http://10.8.0.100>. Ensure that you successfully connect to either one of two Web servers.

    ![A CloudShop Demo - Products - running on Web1 message displays. ](images/Hands-onlabstep-by-step-Enterprise-classnetworkinginAzureimages/media/image77.png "Server response")

    ![A CloudShop Demo - Products - running on Web2 message displays. ](images/Hands-onlabstep-by-step-Enterprise-classnetworkinginAzureimages/media/image78.png "Server response")

11. Using the portal, disassociate the public IP from the NIC of **WGWEB1** **VM**. Do this by navigating to the VM and selecting **Networking** under **Settings** on the left. Select the **NIC Public IP** then choose **Dissociate**. Select **Yes** when prompted.

    ![Selection of the Networking section on the VM with the NIC Public IP highlighted.](images/Hands-onlabstep-by-step-Enterprise-classnetworkinginAzureimages/media/image79.png "Virtual machine networking blade")

12. Next, return to the **WGWEB1 - Networking** blade and select the **Network Interface**

13. Select **IP configurations** under **Settings** on the left.

    ![Selection of the IP Configuration section in the settings menu.](images/Hands-onlabstep-by-step-Enterprise-classnetworkinginAzureimages/media/image169.png "Network interface blade")

14. Next, select **ipconfig1** shown above.

15. Select and make sure that the **Public IP address settings** is shown as disabled, and select **Save** if necessary. This should remove the public IP address from the network interface of the VM.

    ![The ipconfig1 blade of the WGWEBNetworkInterface. Disabling of the Public IP address settings is highlighted along with the save button.](images/Hands-onlabstep-by-step-Enterprise-classnetworkinginAzureimages/media/image170.png "IP configuration blade")

