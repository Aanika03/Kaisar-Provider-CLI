# Kaisar-Provider-CLI
Requirements
To run the Kaisar Provider, ensure your system meets the following specifications:

Operating System: Ubuntu 20.04+, CentOS 8+, or compatible 64-bit Linux distribution

Memory: 4GB RAM

Processor: 64-bit CPU with virtualization support

Storage: 100GB HDD/SSD

Internet Speed: 100Mbps or higher
Dependencies
The following packages and libraries are required (the setup script will install them automatically if missing):

Node.js (v18 or higher recommended)

npm

pm2

curl

tar

git (for some operations)
1) Install basic tools (in case they’re missing)
Ubuntu/Debian
sudo apt-get update
sudo apt-get install -y curl tar git

CentOS/RHEL/Fedora
sudo dnf install -y curl tar git || sudo yum install -y curl tar git


The setup script can install Node.js, npm, and pm2 automatically if you don’t have them.

2) Download the Kaisar setup script
curl -O https://raw.githubusercontent.com/Kaisar-Network/kaisar-releases/main/kaisar-provider-setup.sh


(Optional but smart:) glance at the script:

head -n 40 kaisar-provider-setup.sh

3) Make it executable
chmod +x kaisar-provider-setup.sh

4) Run the installer (with sudo)
sudo ./kaisar-provider-setup.sh


The script will:

Install Node.js (v18+), npm, and pm2 if needed

Download the latest Kaisar Provider CLI

Install dependencies

Set up the CLI globally (kaisar command)

5) Verify the installation
kaisar


If you see a welcome/help message, you’re good to go.
(You can also check Node/pm2 if you’re curious:)

node -v
npm -v
pm2 -v

6) Start using the CLI
# Start the Provider App
kaisar start

# Create a wallet (replace with your email)
kaisar create-wallet -e you@example.com

# OR import an existing wallet
kaisar import-wallet -e you@example.com -k <your-private-key>

# Check node status
kaisar status

# View detailed logs of the Provider App
kaisar log


Where your data lives
Wallet + config are stored at:

/var/lib/kaisar-provider-cli


This persists across updates.

7) Common operations & tips

Update to the latest version

# Simply re-run the setup script; your data is preserved
sudo ./kaisar-provider-setup.sh


pm2 basics (the installer uses pm2 under the hood):

pm2 list
pm2 logs
pm2 restart all
pm2 startup    # optional: generate a startup command so pm2 apps survive reboots


If kaisar isn’t found after install
Open a new shell or ensure /usr/local/bin (or the script’s chosen path) is in your PATH:

echo $PATH
hash -r


If ports are in use
Stop other apps or change their ports, then:

kaisar start
kaisar log


Firewall (only if you manage one)
If your provider requires inbound ports, allow them via ufw/firewalld as appropriate.

8) One-liner quickstart (copy–paste)
# Ubuntu/Debian quickstart
sudo apt-get update && sudo apt-get install -y curl tar git && \
curl -O https://raw.githubusercontent.com/Kaisar-Network/kaisar-releases/main/kaisar-provider-setup.sh && \
chmod +x kaisar-provider-setup.sh && \
sudo ./kaisar-provider-setup.sh && \
kaisar

# CentOS/RHEL/Fedora quickstart
(sudo dnf install -y curl tar git || sudo yum install -y curl tar git) && \
curl -O https://raw.githubusercontent.com/Kaisar-Network/kaisar-releases/main/kaisar-provider-setup.sh && \
chmod +x kaisar-provider-setup.sh && \
sudo ./kaisar-provider-setup.sh && \
kaisar

9) Earning rewards

Create or import your wallet, then follow any on-screen steps to connect your account to the Kaisar Network. Keep your node running and healthy (use kaisar status and kaisar log to monitor).
