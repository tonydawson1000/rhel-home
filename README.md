# rhel-home Repo
This repo contains some simple ansible playbooks to help get a 'fresh' RHEL 8 install setup

## Prereqs
- Before you can run Ansible against a 'host' you must add your local ssh key to the 'host' (so it knows who you are)
- `ssh-copy-id <username>@<machinename>`
- e.g. `ssh-copy-id user1@server1`

## Run Ansible Ping
In this repo the 'hosts.ini' file is configured in `ansible.cfg` so we dont need to specifiy this with every command
- `ansible all -m ping`
- `ansible physicalnodes -m ping`

## Activate the Web Console
Playbook to Activate the web console (same as with: `systemctl enable --now cockpit.socket`)
- `ansible-playbook playbook-rhel-cockpit.yml -e "hostlist=physicalnodes" --ask-become-pass`

You can now browse to the web 'cockpit' on `http://<machine-name>:9090`

## Add to Red Hat Subscription
You need to setup the username and password (for your RHEL Account) as local ENV Vars
-   `rhel_username=<your-rhel-registered-email>`
-   `rhel_password=<your-password>`

-   `ansible-playbook playbook-rhel-registration.yml -e "hostlist=physicalnodes rhel_username=$rhel_username rhel_password=$rhel_password" --ask-become-pass`

## Register with Red Hat Insights
Playbook to register this system (same as with `insights-client --register`)
-   `ansible-playbook playbook-rhel-insights.yml -e "hostlist=physicalnodes" --ask-become-pass`
