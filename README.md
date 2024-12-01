# configure-ad

# On-Premises Active Directory Deployed in the Cloud (Azure)

This guide outlines the steps to deploy an on-premises Active Directory (AD) environment in Azure.

---

## Step 1: Set Up the Azure Virtual Network
1. Log in to the [Azure Portal](https://portal.azure.com).
2. Create a new Virtual Network (VNet):
   - **Address Space**: Use an IP range (e.g., `10.0.0.0/16`).
   - **Subnets**: Create at least one subnet for your AD servers.
3. Ensure the VNet has internet connectivity through a public IP or NAT gateway.

---

## Step 2: Create Virtual Machines for AD
1. Create a Windows Server VM in the Azure Portal:
   - **Image**: Use a Windows Server version supported for AD.
   - **Size**: Choose a size with sufficient resources (e.g., Standard_B2ms).
   - **Network**: Attach the VM to the VNet created in Step 1.
2. Set a static private IP for the VM in the network interface settings.

---

## Step 3: Install Active Directory Domain Services (AD DS)
1. Log in to the Windows Server VM via Remote Desktop.
2. Open **Server Manager** and add the **Active Directory Domain Services** role:
   - Follow the wizard to install the role.
   - Promote the server to a domain controller and create a new forest (e.g., `example.local`).
3. Restart the server after the configuration completes.

---

## Step 4: Configure DNS and Connectivity
1. In the Azure Portal, update the DNS settings for the VNet:
   - Use the private IP address of the AD server as the primary DNS.
2. Verify DNS functionality:
   - Test name resolution within the VNet.
   - Configure additional subnets if required.

---

## Step 5: Join Clients to the Domain
1. Create additional VMs (Windows clients or servers) in the same VNet or connected VNets.
2. Update their DNS settings to point to the AD server’s private IP.
3. Join the VMs to the domain:
   - Right-click **This PC > Properties > Change settings > Change**.
   - Enter the domain name (e.g., `example.local`) and credentials of a domain admin.
4. Restart the VMs to apply domain membership.

---

