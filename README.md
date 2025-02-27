# Guide to Installing Cortensor Mining

This guide will help you install Cortensor Mining AI on your server and join the incentivized testnet.

![Ubuntu](https://img.shields.io/badge/Ubuntu-22.04-orange)  
![Docker](https://img.shields.io/badge/Tool-Docker-blue)  
![Node Status](https://img.shields.io/badge/Node%20Status-Active-brightgreen)

## **Overview**
Cortensor aims to democratize AI by leveraging the power of decentralized networks and open-source models. By eliminating the constraints of centralized services, Cortensor provides a scalable and cost-effective solution for AI inference and development.

### **Key Features**
- **Decentralized AI Inference**: Utilize distributed computing power for efficient AI processing.
- **Open-Source Models**: Allow flexible AI applications without restrictions.
- **Blockchain Integration**: Ensure secure and transparent transactions with incentives for participants.
- **Scalability and Efficiency**: Optimize resource usage and reduce operational costs.

**Website & Community:**
- [Cortensor Website](https://cortensor.network/)
- [Cortensor Discord](https://discord.gg/cortensor)
- [Cortensor Telegram](https://t.me/CortensorNetwork)

---

## **Part 01: Order and Configure a VPS**
To run the node, you need to rent a VPS with the following specifications:

**Minimum Hardware Requirements:**
- **CPU**: 6 vCore (AVX512 support)
- **RAM**: 16GB
- **SSD**: 100GB
- **OS**: Ubuntu 22.04

We recommend using [Contabo](https://contabo.com) due to its affordability and AI mining-friendly features.

1. **Create an account on Contabo**
2. **Choose Cloud VPS 6C or Cloud VPS 8C**
3. **Configure location, OS, and add-ons as needed**
4. **Click "Order and Pay" to complete the purchase**
5. **Check your email for VPS details (IP Address and Password)**

---

## **Part 02: Preparation**
### **1. Staking $COR (Required 2000 $COR per node)**
- Smart Contract for COR:
  ```
  0x8e0eef788350f40255d86dfe8d91ec0ad3a4547f
  ```
- **Buy $COR on Uniswap (ETH Mainnet)** → [Buy here](https://app.uniswap.org/)
- **Stake 2000 $COR in Pool 3** → [Stake here](https://stake.cortensor.network/)
- **Whitelist miner address on Discord** → [Cortensor Discord](https://discord.com/channels/1261511806350790767/1302949161011773491)

### **2. Get ETH on ARB Sepolia**
- **Bridge ETH Mainnet to Sepolia** → [Bridge](https://testnetbridge.com/sepolia)
- **Bridge ETH Sepolia to ARB Sepolia** → [Arbitrum Bridge](https://bridge.arbitrum.io/)
- **Send ETH to your Miner Address**

### **3. Set Up Your Own RPC**
- **Use [drpc.org](https://drpc.org) to get an RPC endpoint**
- **Create an API Key and save your RPC Endpoint**

---

## **Part 03: Prerequisite Installation**
### **1. Update System and Install Dependencies**
```bash
sudo apt update -q && sudo apt upgrade -qy
sudo apt install -qy curl git jq lz4
```

### **2. Clone Installer**
```bash
git clone https://github.com/cortensor/installer
cd installer
```

### **3. Install Docker**
```bash
./install-docker-ubuntu.sh
```

### **4. Install IPFS**
```bash
./install-ipfs-linux.sh
```

### **5. Install Cortensor**
```bash
./install-linux.sh
```
> **Note**: This process will create a new user named `deploy`.

### **6. Copy Installer Folder to Deploy User**
```bash
cd ~/
cp -Rf ./installer /home/deploy/installer
chown -R deploy.deploy /home/deploy/installer
```

### **7. Switch to Deploy User and Verify Installation**
```bash
sudo su deploy
cd ~/
ls -al /usr/local/bin/cortensord
ls -al $HOME/.cortensor/bin/cortensord
ls -al /etc/systemd/system/cortensor.service
ls -al $HOME/.cortensor/bin/start-cortensor.sh
ls -al $HOME/.cortensor/bin/stop-cortensor.sh
docker version
ipfs version
```

If no errors are found, the installation is successful.

---

## **Part 04: Node Management**
1. **Switch to Deploy User**
   ```bash
   sudo su deploy
   ```
2. **Generate Key**
   ```bash
   /usr/local/bin/cortensord ~/.cortensor/.env tool gen_key
   ```
   ***Fill out this form with details [HERE](https://docs.google.com/forms/u/0/d/e/1FAIpQLSfNEGWnWO10pnMPu5uX6yk4mZ9qf4fOxvTqcsFaO9V88OQFJw/formResponse)***
   ***For Referral - Discord ID use:  `Suryaone`***
   
4. **Register the Node**
   ```bash
   /usr/local/bin/cortensord ~/.cortensor/.env tool register
   ```
**After your Node is approved by the Cortensor team and your data is Valid, follow these steps**
   
4. **Verify the Node**
   ```bash
   /usr/local/bin/cortensord ~/.cortensor/.env tool verify
   ```
5. **Start the Node**
   ```bash
   sudo systemctl start cortensor
   ```
6. **Check Node Logs**
   ```bash
   tail -f /var/log/cortensord.log
   ```

---

## **Part 05: Troubleshooting**
### **1. Changing Your Own RPC**
```bash
sudo su deploy
nano ~/.cortensor/.env
```
Locate the `#RPC` section and replace `HOST` with your own RPC from drpc.org, then save and restart:
```bash
sudo systemctl restart cortensor
```

### **2. Check Node Address & ID**
```bash
/usr/local/bin/cortensord ~/.cortensor/.env tool id
```

### **3. Check Node Stats**
```bash
/usr/local/bin/cortensord ~/.cortensor/.env tool stats
```

---

## **Monitoring Node**
- **Official Cortensor Dashboard:** [Click here](https://dashboard-devnet3.cortensor.network/nodestats)
- **Node Alert System Bot:** [Telegram Bot](https://t.me/Cortensor_BOT)

---

### **Congratulations! You have successfully installed and managed the Cortensor Mining AI node! 🚀**

