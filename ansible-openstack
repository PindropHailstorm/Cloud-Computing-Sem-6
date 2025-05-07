# Openstack using Ansible

Reference https://docs.openstack.org/openstack-ansible/2024.1/user/aio/quickstart.html


Update all packages:
```bash
sudo apt update
sudo apt dist-upgrade
reboot
```

Setup openstack-ansible repo:
```bash
# Become root user
sudo -i

# clone openstack-ansible
git clone https://opendev.org/openstack/openstack-ansible \
  /opt/openstack-ansible
cd /opt/openstack-ansible

# take the latest stable release
git checkout 29.0.2
```
> use `master` branch for latest build.


bootstrap all in one setup:
```bash
./scripts/bootstrap-ansible.sh
./scripts/bootstrap-aio.sh
```

Update user config file:
```bash
vim /etc/openstack_deploy/openstack_user_config.yml
```

Update user variables:
```bash
vim /etc/openstack_deploy/user_variables.yml
```

Verify External IP for accessing horizon dashboard:
```
cat /etc/openstack_deploy/openstack_user_config.yml | grep external_lb_vip_address
```

Install everything, move to `/opt/openstack-ansible/playbooks` directory:
```bash
cd /opt/openstack-ansible/playbooks

openstack-ansible setup-hosts.yml
openstack-ansible setup-infrastructure.yml
openstack-ansible setup-openstack.yml

# OR
openstack-ansible setup-everything.yml
```

verify installation:
```bash
lxc-ls --fancy
```

Check all the VMs:
```bash
virsh list --all
```

login as `admin` user, password you can get:
```bash
cat /etc/openstack_deploy/user_secrets.yml | grep "keystone_auth_admin_password"
```

Get inside horizon container:
```bash
lxc-attach aio1-horizon-container-63d9ffa3
```
