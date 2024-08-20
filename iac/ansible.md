[Home](../README.md)

#### Ansible
**Installation**  
For Ubuntu
```
$ sudo apt update
$ sudo apt install software-properties-common
$ sudo apt-add-repository --yes --update ppa:ansible/ansible
$ sudo apt install ansible -y
```
Check Ansible version
```
$ ansible --version
```

**Playbook**  
```
$ mkdir playbooks
$ cd playbooks
$ vagrant init hashicorp/bionic64
$ vagrant up
```
Check machine / ssh-config
```
$ vagrant ssh
$ vagrant ssh-config
```
Confirm that you can SSH into machine using 
```
$ ssh vagrant@127.0.0.1 -p 2222 -i /home/sajid/learning/ansible/playbooks/.vagrant/machines/default/virtualbox/private_key
```

**Install Nginx on remote machine**  
We will use [these codes](https://gitlab.com/ahmadalsajid/ansible_playbook/-/tree/chapter_2) to demonstrate.
To execute that
```
$ ansible-playbook web-notls.yml -i hosts -b
``` 
Now, we can check that from http://127.0.0.1:8080  

**Install Nginx with TLS on remote machine**  
We will use [these codes](https://gitlab.com/ahmadalsajid/ansible_playbook/-/tree/chapter_2) to demonstrate.  

Generate Certificates
```
$ openssl req -x509 -nodes -days 3650 -newkey rsa:2048 -subj /CN=localhost -keyout files/nginx.key -out files/nginx.crt
```
To execute that
```
$ ansible-playbook web-tls.yml -i hosts -b
``` 
Now, we can check that from https://127.0.0.1:8443    

**Inventory**  
>Vagrant with multiple servers.  

We will use [these codes](https://gitlab.com/ahmadalsajid/ansible_playbook/-/tree/chapter_3) to demonstrate.   
We'll use 3 vagrant machines for this. Destroy previous vagrant using 
`vagrant destroy --force` and change the `Vagrantfile` according to the 
mentioned codes. Now, create three machines with `vagrant up`.

To check the machines are accessible, check with
```
$ ansible vagrant2 -i hosts -a "ip addr show dev eth0" 
```

#### References: 
* [Ansible documentation](https://docs.ansible.com/ansible/latest/index.html) 
* [Ansible: Up and Running](https://www.oreilly.com/library/view/ansible-up-and/9781491915318/)
