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
<pre><code>
$ ssh pi@<b>pi_host</b> 'mkdir -p ~/.ssh'
</code></pre>

From the control/local host generate the ssh-keys required to control the RPi.
<pre><code>
$ ssh-keygen -t rsa -C "Raspberry Pi" -f id_rsa_rpi -q -N ""
</code></pre>

Then provision the ssh-key to the RPi.
<pre><code>
$ cat ~/.ssh/id_rsa_rpi.pub | ssh pi@<b>pi_host</b> 'cat >> ~/.ssh/authorized_keys'
</code></pre>

**NOTE:** Remember to replace <mark>pi_host</mark> with the RPi hostname/IP  

# Usage
<pre><code>
$ ansible-playbook -i hosts -u pi -s plays/unifi_on_rpi3.yml
</code></pre>

When the playbook finishes execution and the RPi reboot completes, use a web browser to view the UniFi setup wizard/admin page at:  
[https://pi_host:8443](https://pi_host:8443)