# Azure-File-Storage-and-Network-Restriction-Lab
In this lab, I created and configured an Azure File share, uploaded a file using Azure Storage Browser, created a virtual network, configured a Microsoft.Storage service endpoint, and restricted access to the Storage Account so that only traffic from the approved virtual network could access the storage resources.

---

## Step 1: Open Classic File Shares

### What I did

I navigated to my Azure Storage Account and opened:

**Data storage > Classic file shares**

This is where Azure File shares can be created and managed.

### Screenshot

`01-classic-file-shares.png`

![Classic File Shares](screenshots/01-classic-file-shares.png)

---

## Step 2: Create the File Share

### What I did

I selected **+ Classic file share** and created a new file share named:

`share1`

I kept the default access tier set to:

**Transaction optimized**

### Screenshot

`02-create-share1.png`

![Create File Share](screenshots/02-create-share1.png)

---

## Step 3: Disable Backup

### What I did

I opened the **Backup** tab during file share creation.

I confirmed that **Enable backup** was not selected because backup was not required for this lab.

I then selected **Review + create** and created the file share.

### Screenshot

`03-disable-backup.png`

![Disable Backup](screenshots/03-disable-backup.png)

---

## Step 4: Verify the File Share

### What I did

After deployment completed, I returned to the Storage Account and opened **Storage browser**.

Under **Classic file shares**, I verified that `share1` had been successfully created.

### Screenshot

`04-verify-share1.png`

![Verify File Share](screenshots/04-verify-share1.png)

---

## Step 5: Open the File Share

### What I did

I selected `share1` inside Storage Browser.

I reviewed the available options, including the ability to create directories using **+ Add directory**.

### Screenshot

`05-open-share1.png`

![Open File Share](screenshots/05-open-share1.png)

---

## Step 6: Upload a File

### What I did

Inside `share1`, I selected **Upload** and selected a file from my local computer.

If an authorization error occurs, Storage Browser can be configured to use the **Microsoft Entra user account** authentication method.

### Screenshot

`06-upload-file.png`

![Upload File](screenshots/06-upload-file.png)

---

## Step 7: Verify the Uploaded File

### What I did

After the upload completed, I confirmed that the file appeared inside the Azure File share.

This verified that the file share was working correctly and that I could manage files through Azure Storage Browser.

### Screenshot

`07-file-uploaded.png`

![Uploaded File](screenshots/07-file-uploaded.png)

---

## Step 8: Create a Virtual Network

### What I did

I searched for **Virtual networks** in the Azure portal and selected **Create**.

I configured:

**Resource group:** `az104-rg7`

**Virtual network name:** `vnet1`

I kept the remaining settings at their default values.

### Screenshot

`08-create-vnet1.png`

![Create Virtual Network](screenshots/08-create-vnet1.png)

---

## Step 9: Verify the Virtual Network

### What I did

After deployment completed, I opened `vnet1` and verified that the virtual network had been successfully created.

The default subnet would be used to configure access to the Storage Account.

### Screenshot

`09-vnet1-overview.png`

![Virtual Network Overview](screenshots/09-vnet1-overview.png)

---

## Step 10: Configure the Microsoft.Storage Service Endpoint

### What I did

Inside `vnet1`, I navigated to:

**Settings > Service endpoints**

I selected **Add** and configured:

**Service:** `Microsoft.Storage`

**Service endpoint policies:** `0 selected`

**Subnet:** `default`

I then selected **Add** to save the configuration.

### Screenshot

`10-storage-service-endpoint.png`

![Storage Service Endpoint](screenshots/10-storage-service-endpoint.png)

---

## Step 11: Open Storage Account Networking

### What I did

I returned to my Storage Account and navigated to:

**Security + networking > Networking**

Under **Public network access**, I selected **Manage**.

This section controls which networks are allowed to access the Storage Account.

### Screenshot

`11-storage-networking.png`

![Storage Account Networking](screenshots/11-storage-networking.png)

---

## Step 12: Add the Virtual Network

### What I did

I selected **Add a virtual network** and then selected **Add existing network**.

I configured:

**Virtual network:** `vnet1`

**Subnet:** `default`

I then added the network to the Storage Account access rules.

### Screenshot

`12-add-vnet1.png`

![Add Virtual Network](screenshots/12-add-vnet1.png)

---

## Step 13: Remove My Public IP Address

### What I did

In the **IPv4 Addresses** section, I removed my computer's public IP address from the allowed network list.

This ensured that access would only be permitted through the approved Azure virtual network.

I then saved the networking configuration.

### Screenshot

`13-remove-public-ip.png`

![Remove Public IP](screenshots/13-remove-public-ip.png)

---

## Step 14: Verify the Network Restriction

### What I did

After saving the changes, I reviewed the Storage Account networking configuration.

The Storage Account was now configured to allow access through:

`vnet1`

and its:

`default`

subnet.

### Screenshot

`14-network-restriction-configured.png`

![Network Restriction Configured](screenshots/14-network-restriction-configured.png)

---

## Step 15: Test Storage Access

### What I did

I returned to **Storage browser** and refreshed the page.

I attempted to access the contents of `share1`.

Because my computer was not connecting through the approved Azure virtual network, Azure blocked access to the storage content.

### Screenshot

`15-test-storage-access.png`

![Test Storage Access](screenshots/15-test-storage-access.png)

---

## Step 16: Verify Unauthorized Access

### What I did

Azure displayed an authorization error when I attempted to access the files.

This confirmed that the Storage Account networking restriction was working correctly.

My Azure identity could still access the Azure portal, but the Storage Account rejected the request because it did not originate from the approved virtual network.

### Screenshot

`16-access-denied.png`

![Access Denied](screenshots/16-access-denied.png)

---

## Lab Results

I successfully created an Azure File share, uploaded a file using Storage Browser, created a virtual network, configured a Microsoft.Storage service endpoint, restricted Storage Account access to the virtual network, and verified that traffic from an unauthorized network was blocked.

---

## Key Takeaways

This lab demonstrated that Azure Storage security can be controlled at both the identity and network layers.

Azure Files provides managed cloud file storage, while Storage Browser provides a simple way to manage files directly from the Azure portal.

Azure Virtual Networks and service endpoints provide additional security by allowing Storage Accounts to restrict access based on the source network.

The final access test demonstrated that having valid Azure credentials does not automatically provide access to a storage resource. The identity must have the correct permissions, and the request must also meet the configured network requirements.

---

## Skills Demonstrated

- Azure Files
- Azure Storage Accounts
- Azure Storage Browser
- Microsoft Entra ID
- Azure Virtual Networks
- Azure Service Endpoints
- Storage Account networking
- Network access restrictions
- Azure storage security
- Cloud storage administration

---

## Screenshot Structure

```text
