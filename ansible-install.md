# Installing Ansible from source (with fish shell)

1. Check python version `python --version` if python is not installed you should install it.
1. Install easy_install and pip `sudo apt-get install python-setuptools python-yaml python-pip`
1. Install c compiler `sudo apt-get install build-essential` and python dev `sudo apt-get install python-dev`
1. And install dependencies `sudo -H pip install paramiko PyYAML Jinja2 httplib2 six`
1. Move to directory where you want to install ansible (this should be directory that user has acces to because he will need to run set env script). I choose /opt and execute `sudo git clone git://github.com/ansible/ansible.git --recursive`
1. Then change directory group with `sudo chown root:users -R /opt/ansible/`
1. Then make sure that *users* group has write access to directory `sudo chmod g+w /opt/ansible/ -R`. You should also check that you are member of group *users* `groups`.
1. You should also correct error in /opt/ansible/hacking/env-setup.fish
1. Set running config script on login into shell (~/config/fish/config.fish)

  ```bash
  # Run script to set ansible to work
  # > redirects stdout and ^ redirects stderr
  . /opt/ansible/hacking/env-setup.fish -q > /dev/null ^ /dev/null
  ```
1. You should also add script to get latest version of ansible from git to /etc/init.d/
  I named script refresh-ansible

  ```bash
  #!/bin/sh

  # Help for setup: https://wiki.debian.org/LSBInitScripts

  ### BEGIN INIT INFO
  # Provides:          refresh-ansible
  # Required-Start:    $remote_fs $syslog
  # Required-Stop:     $remote_fs $syslog
  # Default-Start:     1 2 3 5
  # Default-Stop:      
  # Short-Description: Start refresh-ansible at boot time
  # Description:       Refreshes ansible instalation at boot time.
  ### END INIT INFO

  cd /home/mladen/lib/ansible
  git pull --rebase
  git submodule update --init --recursive
  ```
1. You should make this file executable `sudo chmod +x refresh-ansible` and run command `sudo update-rc.d refresh-ansible defaults`. This will add script to directory /etc/rc3.d/. If you later want to remove script from boot just run `sudo update-rc.d refresh-ansible remove`
1. Next you need to install boto `sudo -H pip install -U boto`
1. Create ~/.boto file with content

  ```
  [Credentials]
  aws_access_key_id = AKIAJTKAWVR5TELVR4VA
  aws_secret_access_key = wir9eklBfm8HQbDIlkxfIkOOpRb3VJ7mGFgVgu4a
  ```
1. Change .boto permissions `chmod 400 ~/.boto`
1. Last you need to put your aws credentials in .ssh directory (*.pem)
