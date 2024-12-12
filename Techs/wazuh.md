# Install wazuh on a system 

download wazuh OVA 

https://packages.wazuh.com/4.x/vm/wazuh-4.9.2.ova

# Import wazuh OVA to vmware

Select open virtual machine in vmware

# Configure

Open wazuh OVA and wait for it to finish installation

# Access wazuh dashboard

https://<wazuh-vm-ip>

find wazuh-vm-ip using: '''ip a''' command

Set network connection to NAT

# Configure dashboard

sudo systemctl start wazuh-manager

sudo systemctl start wazuh-dashdoard

sudo systemctl daemon-reload

sudo systemctl enable wazuh-indexer

sudo systemctl start wazuh-indexer

Now dashboard should open
