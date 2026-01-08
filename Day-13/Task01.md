### Day 13: IPtables Installation And Configuration

We have one of our websites up and running on our Nautilus infrastructure in Stratos DC. Our security team has raised a concern that right now Apache’s port i.e 6300 is open for all since there is no firewall installed on these hosts. So we have decided to add some security layer for these hosts and after discussions and recommendations we have come up with the following requirements:



1. Install iptables and all its dependencies on each app host.


2. Block incoming port 6300 on all apps for everyone except for LBR host.


3. Make sure the rules remain, even after system reboot.




✅ STEP 1: Get LBR IP (from Jumphost)
On jumphost:
hostname -I


and:

cat /etc/hosts | grep -i lb


You will see something like:

172.16.238.14   lbr


👉 Note this IP — call it <LBR_IP>

✅ STEP 2: Install iptables on EACH App Server

Do this on stapp01, stapp02, stapp03

sudo yum install -y iptables-services
sudo systemctl enable iptables
sudo systemctl start iptables


Check:

sudo systemctl status iptables

✅ STEP 3: Add Firewall Rules (VERY IMPORTANT ORDER)
On EACH App Server:
🔹 First allow LBR
sudo iptables -I INPUT 1 -p tcp -s <LBR_IP> --dport 8089 -j ACCEPT

🔹 Then block everyone else
sudo iptables -A INPUT -p tcp --dport 8089 -j DROP

🔹 (Optional but safe) allow established traffic
sudo iptables -I INPUT 1 -m state --state ESTABLISHED,RELATED -j ACCEPT

✅ STEP 4: Save Rules Permanently
On EACH App Server:
sudo service iptables save


or

sudo iptables-save | sudo tee /etc/sysconfig/iptables


Restart to verify persistence:

sudo systemctl restart iptables


Check:

sudo iptables -L -n --line-numbers


You should see:

ACCEPT from <LBR_IP> to port 8089

DROP for others on port 8089

✅ STEP 5: Verify
From LBR host:
curl http://stapp01:8089
curl http://stapp02:8089
curl http://stapp03:8089


→ ✅ must work