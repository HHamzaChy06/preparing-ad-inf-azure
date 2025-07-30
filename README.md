<p align="center">
  <img src="https://i.imgur.com/pU5A58S.png" width="200" alt="Active Directory Logo"/>
</p>

# Building an Active Directory Lab in Azure

This project walks through creating a small Active Directory environment entirely within Azure. The setup uses one Windows Server acting as a Domain Controller (DC) and one Windows 10 client machine. Both are deployed inside the same virtual network with custom DNS settings to allow domain join and authentication.

---

## 🔧 Tools & Services
- **Azure Portal** (Resource Groups, VNets, Virtual Machines)
- **Active Directory Domain Services**
- **Remote Desktop Protocol (RDP)**
- **PowerShell / Command Prompt**

---

## 🖥️ Operating Systems
- **Windows Server 2022** – Domain Controller
- **Windows 10 21H2** – Client

---

## 📌 Deployment Steps

### Step 1: Prepare Azure Environment
- **Create a Resource Group** for all AD lab resources.
- **Deploy a Virtual Network** with an address space (e.g. `10.0.0.0/16`) and at least one subnet (e.g. `10.0.0.0/24`).

### Step 2: Configure Domain Controller (DC-1)
- Launch a **Windows Server 2022** VM inside the resource group and virtual network.
- Assign a strong admin username and password.
- After creation, go to the network interface and set the **Private IP to Static** to prevent changes on reboot.
- Connect via RDP and ensure basic connectivity (ping gateway or other VMs).
- (Optional for lab use) Temporarily disable Windows Firewall for easier testing.

📷 *[Insert screenshot of DC-1 networking settings here]*

### Step 3: Configure Client Machine (Client-1)
- Deploy a **Windows 10** VM in the same resource group and virtual network as DC-1.
- In the Client-1 NIC settings, change the **DNS server** to the Private IP of DC-1.
- Restart the client VM to apply DNS changes.
- RDP into Client-1 and test by pinging DC-1's Private IP.
- Verify DNS settings via:
  ```powershell
  ipconfig /all
