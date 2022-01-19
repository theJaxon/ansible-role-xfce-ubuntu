![Ubuntu](https://img.shields.io/badge/-ubuntu-E95420?style=for-the-badge&logo=ubuntu&logoColor=white)
![XFCE](https://img.shields.io/badge/-xfce-2284F2?style=for-the-badge&logo=xfce&logoColor=white)

- Ansible role for setting XFCE GUI For Ubuntu 20.04
- Based on the tutorial [How to Use a GUI with Ubuntu Linux on AWS EC2](https://www.youtube.com/watch?v=6x_okhl_CF4) which is based on an Amazon tutorial that by now is already deleted but the bash script exists in the video description 

<details>
<summary> Original Bash Script </summary>
<p>

```bash
#!/bin/bash
sudo apt update -y &&  sudo apt upgrade -y

sudo sed -i 's/^PasswordAuthentication no/PasswordAuthentication yes/' /etc/ssh/sshd_config

sudo /etc/init.d/ssh restart

# This section was slightly modified to allow for non-interactive installation
sudo apt-get  install xfce4 --no-install-recommends -y

sudo DEBIAN_FRONTEND=noninteractive apt-get install -y lightdm

sudo apt-get install -y xrdp xfce4-goodies tightvncserver

echo xfce4-session > /home/ubuntu/.xsession  

sudo cp /home/ubuntu/.xsession /etc/skel

sudo service xrdp restart

sudo passwd ubuntu
```

</p>
</details>


---

### How to use 

- It's expected to pass the packer user password via the variable `packer_password` so the full command to execute the role can be 
```bash
ansible-playbook xfce-ubuntu.yaml --extra-vars packer_password=<password>
```
- The role was made for AWS Ubuntu Instance, the security Group should enable RDP Port number **3389**
- After the role is executed, you should be able to reach the instance using a remote desktop client tool like [`Remmina`](https://remmina.org/)