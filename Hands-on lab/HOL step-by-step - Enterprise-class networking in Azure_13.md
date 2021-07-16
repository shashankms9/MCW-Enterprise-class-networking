## Exercise 8: Build the Bastion host service

Duration: 15 minutes

In this exercise, management of the Azure-based systems will only be available through a Bastion host. In this section, you will provision this service.

### Task 1: Build the Bastion host

This step should have been completed in Exercise 1, Task 1.  If it was not, please complete the steps below.

1.  In the Azure portal, select **+ Create a resource** then select **Bastion**. In the search results, select the Bastion service with Microsoft as the publisher.

2.  On the **Create a Bastion** blade, on the **Basics** tab, enter the following information, and select **Review + Create**:

    -  Subscription: **Select your subscription**.

    -  Resource group: Select **WGVnetRG1**.

    -  Name: **WGBastion**

    -  Region: **(US) South Central US**

    -  Virtual network: **WGVNet1**

    -  Subnet: **AzureBastionSubnet** Note: After creation, assign (10.7.5.0/24) as the subnet address.

    -  Public IP: **Create New**

    -  Public IP address name: **BastionPublicIP**


3.  On the **Create a Bastion** blade, on the **Review + Create** tab, ensure the validation passes, and select **Create**. The Bastion host will take about 5 minutes to provision.

