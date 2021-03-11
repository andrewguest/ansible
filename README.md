1. Create local user for Ansible to use (on the remote host):
    - `sudo useradd -c "Account for connecting with Ansible" -G sudo -m -s /bin/bash andrew && sudo passwd andrew`
2. Create an SSH key on the Ansible manager device as the user that will be connecting to the remote hosts (andrew):
    - `ssh-keygen -t ed25519 -C "Account for Ansible"`
3. Add the public key of the Ansible manager to the remote host:
    - `ssh-copy-id -i ~/.ssh/id_ed25519.pub andrew@<remote host>`
4. Copy the **hosts** file in this directory to `/etc/ansible/hosts`
5. Run a playbook:
    - `ansible-playbook -T 30 --ask-become-pass <name_of_playbook_file>.yml`
    - `-T 30` overrides the default timeout and sets a timeout of 30 seconds
    - `--ask-become-pass` ask for privilege escalation password