******
# Bloodhound Installation Steps
- Cursor issue: click VM > Manage > Change Hardware Compatibility > VMWare 17.x
```bash
#!/bin/bash

# WE ASSUME FRESH INSTALL OF KALI
# RUN AS SUPER USER (sudo su)
# Remember to move file.dat
# nano script.sh -> paste this script
# Ctrl+X, Y, ENTER.
# chmod +x script.sh
# ./script.sh

# Install Docker
sudo apt update -y
sudo apt install docker.io docker-compose -y
sudo systemctl enable docker --now

# Get Bloodhound
git clone https://github.com/SpecterOps/BloodHound.git

# Get ADExplorer
cd /home/kali/
git clone https://github.com/c3c/ADExplorerSnapshot.git
cd ADExplorerSnapshot

# Install requirements 
pip3 install -r requirements.txt --break-system-packages

# Run tool for bloodhound output
python3 ADExplorerSnapshot.py -m BloodHound /home/kali/Desktop/file.dat

# 
cd /home/kali/BloodHound/examples/docker-compose
docker compose up -d

echo "Going to sleep... give me 15!"
sleep 15
# Grab initial password from bloodhound container
# open location
open http://127.0.0.1:8080/
docker logs docker-compose-bloodhound-1 | grep -i "Initial Password"
open ./ADExplorerSnapshot/
```