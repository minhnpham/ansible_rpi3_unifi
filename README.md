# Ubiquiti UniFi software on a Raspberry Pi 3

An Ansible Playbook to auto provision Ubiquiti UniFi software on a Raspberry Pi 3.

# Requirements

+ Raspberry Pi 3
+ Raspbian or Raspbian Lite (on the Pi3)
+ Ansible 2.2+

# Configurations

### 1. Update RPi hostname/IP
Update the "hosts" file with your relevant Pi hostname/IP

### 2. Install Ansible
You will need Ansible installed on your local machine/control node, if not already installed, follow the guides here for [Ansible installation](http://docs.ansible.com/ansible/intro_installation.html).  

### 3. Setup SSH Keys for the Raspberry Pi

Create the .ssh directory on the RPi.  
<code>
$ ssh pi@<b>pi_host</b> 'mkdir -p ~/.ssh'
</code>

From the control/local host generate the ssh-keys required to control the RPi.  
`$ ssh-keygen -t rsa -C "Raspberry Pi" -f id_rsa_rpi -q -N ""`  

Then provision the ssh-key to the RPi.  
`$ cat ~/.ssh/id_rsa_rpi.pub | ssh pi@`**`pi_host`** `'cat >> ~/.ssh/authorized_keys'`

**NOTE:** Remember to replace **pi_host** with the RPi hostname/IP  

# Usage

`$ ansible-playbook -i hosts -u pi -s plays/unifi_on_rpi3.yml`

When the RPi reboot completes, use a web browser to view the UniFi setup wizard/admin page at:
`https://`**`pi_host`**`:8443`