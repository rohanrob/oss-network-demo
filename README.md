# oss-network-demo

Try an open source software based network, using OPNsense and Cumulus.

### Install vagrant-vbguest plugin on host

    wget -c https://releases.hashicorp.com/vagrant/2.2.4/vagrant_2.2.4_x86_64.deb
    sudo dpkg -i vagrant_2.2.4_x86_64.deb
    vagrant plugin install vagrant-vbguest

### Run vagrant up on host
   
    # Start switches:
    oss-network-demo/switches> vagrant up

    # Start firewalls:
    oss-network-demo/firewalls> vagrant up

    # Start workstations:
    oss-network-demo/workstations> vagrant up

### Install lxml on oob-mgmt-server

    oss-network-demo/topology_converter> vagrant ssh oob-mgmt-server
    sudo pip3 install lxml

### Download git repo on oob-mgmt-server
    oss-network-demo/switches> vagrant ssh oob-mgmt-server
    sudo -s
    su cumulus
    git clone https://github.com/naturalis/oss-network-demo/
    cd oss-network-demo/ansible

### Install Ansible roles on oob-mgmt-server
    oss-network-demo/switches> vagrant ssh oob-mgmt-server
    oss-network-demo/ansible/roles$ ansible-galaxy install -r requirements.yml --roles-path .

### Run ansible commands from oob-mgmt-server
    ansible -c paramiko -m command -a "uptime" firewalls
    ansible all -c paramiko -m shell -a 'uptime' -l firewalls

    # Deploy switches:
    ansible-playbook switches.yml

    # Deploy firewalls:
    ansible-playbook -c paramiko firewalls.yml

### Test
    mtr --tcp 172.16.1.1
    mtr --udp 172.16.1.1

### VirtualBox commands
    vboxmanage showvminfo 1552905337_firewall2
