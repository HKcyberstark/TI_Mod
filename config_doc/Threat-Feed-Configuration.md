## Minemeld Installation

Minemeld Can be easily and directly installed with their Ansible playbook.  more details in their Minemeld-Github

CentOS would be used for this demonstration and it is good to have root access for ease of installation.

```
$ Git clone https://github.com/PaloAltoNetworks/minemeld-ansible.git
$ sudo yum install -y wget git gcc python-devel libffi-devel openssl-devel zlib-dev sqlite-devel bzip2-devel
$ wget https://bootstrap.pypa.io/get-pip.py
$ sudo -H python get-pip.py
$ sudo -H pip install ansible
$ git clone https://github.com/PaloAltoNetworks/minemeld-ansible.git
$ cd minemeld-ansible
$ ansible-playbook -K -i 127.0.0.1, local.yml
$ usermod -a -G minemeld <your user> # add your user to minemeld group, useful for development
```


Upon complete Installation, Check if all services running

```
$ sudo -u minemeld /opt/minemeld/engine/current/bin/supervisorctl -c    /opt/minemeld/supervisor/config/supervisord.conf status
```

Minemeld Web UI is installed along with the core engine using above Ansible playbook.  Access the web UI (http://[serverIP] ) with default credentials of **username: admin and password: minemeld**. Different users and authorization can be configured within minemeld GUI depending on your compliance needs

![1](https://user-images.githubusercontent.com/40884455/56400753-1641dc00-6288-11e9-87b7-d4c6c2e3e77e.JPG)

## Minemeld - Threat Feed Configuration

* Navigate to Config tab  and view the list of prototypes that can be used.

![2](https://user-images.githubusercontent.com/40884455/56400786-45584d80-6288-11e9-85b4-7253acbf536e.JPG)

Select the prototype you wish to add. I will be adding Ipv4 indicators as miners that are not available by default.
  - if you wish to add the Ipv4 miner –  select clone and click ok

  - if you wish to customise the miner by adding your own data feed inputs – select new and edit the config

![3](https://user-images.githubusercontent.com/40884455/56400830-7c2e6380-6288-11e9-8fb8-12e7d02fd174.JPG)

* Select Ipv4 processor prototype if not available by default. Processor node can also be customized/renamed if needed.
* Select Stdlib.local.Logstash output prototype to configure Logstash output node
  - select new and edit the logstash host and port if you wish to customize from default.

![4](https://user-images.githubusercontent.com/40884455/56400852-9cf6b900-6288-11e9-9007-c32fe003581c.JPG)

![5](https://user-images.githubusercontent.com/40884455/56400860-a5e78a80-6288-11e9-80a9-6e3019d7dfd9.JPG)

* Once the prototypes configured , navigate to Config tab
* Select input field from Processor node and add the miner

Below example is a customized Ipv4 processor and logstash output config.

![6](https://user-images.githubusercontent.com/40884455/56400901-e21aeb00-6288-11e9-99eb-86b975f165e2.JPG)

Once the Threat feeds are configured – The changes should be Saved by Clicking “Commit” button at right top corner of config tab.  [ **But wait**]

*Once the threat feeds are committed to process, Logstash output node would be continuously sending data to the configured Logstash host. So it is important to configure your Logstash instance ready before committing the threat feeds.*
