## System Requirements

| **Hardware** | **Minimum Requirement** |
|--------------|-------------------------|
| **CPU**      | 4 Cores                 |
| **RAM**      | 8 GB                    |
| **Disk**     | 200 GB                  |
| **Bandwidth**| 10 MBit/s               |

## Install Guide

### 1. Install Docker
```
sudo apt-get update && sudo apt-get install -y apt-transport-https ca-certificates curl software-properties-common && curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /usr/share/keyrings/docker-archive-keyring.gpg && echo "deb [arch=$(dpkg --print-architecture) signed-by=/usr/share/keyrings/docker-archive-keyring.gpg] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable" | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null && sudo apt-get update && sudo apt-get install -y docker-ce docker-ce-cli containerd.io && sudo systemctl start docker && sudo systemctl enable docker && sudo docker --version
```
### 2. Generate Validator Private Key

Prepare any EVM wallet like Metamask and Extract Private key
Faucet on Sepolia Network:

- https://cloud.google.com/application/web3/faucet/ethereum/sepolia
- https://www.alchemy.com/faucets/ethereum-sepolia

### 3. Set Up Validator Environment
```
wget https://files.elixir.finance/validator.env
```
```
sudo nano ~/validator.env
```

**STRATEGY_EXECUTOR_IP_ADDRESS: Your public IP/VPS IP.**

**STRATEGY_EXECUTOR_DISPLAY_NAME: Your chosen display name.**

**STRATEGY_EXECUTOR_BENEFICIARY: The wallet address to receive rewards.**

**SIGNER_PRIVATE_KEY: The private key from Metamask (without 0x).**


### 5. Enroll Validator

- Go to: https://testnet-3.elixir.xyz
- Mint Mock and Stake 1000 Mock
- Click to "**Custom validator**" and fill your wallet address

  ![image](https://github.com/user-attachments/assets/7c8fccd3-20cc-4154-9953-e137439fe61b)

### 5. Run the Validator

- Pull the Docker Image:
```
docker pull elixirprotocol/validator:v3
```
- Start Validator:
```
docker run -d \
  --env-file /root/validator.env \
  --name elixir \
  --restart unless-stopped \
  elixirprotocol/validator:v3
```
### 5. Check logs

Determine your container ID
```
docker ps
```
![image](https://github.com/user-attachments/assets/3a99e2f2-5e19-4657-9a87-4e375294131b)

Check logs
```
docker logs --tail 50 -f <container-ID>

```
![image](https://github.com/user-attachments/assets/0bcda0f6-8cfc-4ade-b2ea-7a73f57bdffe)

