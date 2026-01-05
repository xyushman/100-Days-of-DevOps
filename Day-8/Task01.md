### Day 8: Install Ansible

During the weekly meeting, the Nautilus DevOps team discussed about the automation and configuration management solutions that they want to implement. While considering several options, the team has decided to go with Ansible for now due to its simple setup and minimal pre-requisites. The team wanted to start testing using Ansible, so they have decided to use jump host as an Ansible controller to test different kind of tasks on rest of the servers.



Install ansible version 4.9.0 on Jump host using pip3 only. Make sure Ansible binary is available globally on this system, i.e all users on this system are able to run Ansible commands.


📦 Step 2: Install Ansible 4.9.0 using pip3 (system-wide)

Run as root to make it global:

sudo pip3 install ansible==4.9.0


This installs:

ansible

ansible-playbook

ansible-galaxy
into /usr/local/bin

🧪 Step 3: Verify Ansible Version
ansible --version


Expected output (version may show ansible-core internally, that is OK):

ansible 4.9.0

🌍 Step 4: Ensure Ansible is Globally Available

Check if /usr/local/bin is in PATH:

echo $PATH


If /usr/local/bin is missing, add it globally:

sudo echo 'export PATH=$PATH:/usr/local/bin' >> /etc/profile