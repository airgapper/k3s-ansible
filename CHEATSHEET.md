# Install ansible in python venv
```
pip install virtualenv
virtualenv ansible
source ansible/bin/activate
pip install ansible
```

# Setup cluster
`ansible-playbook site.yml -i inventory/cluster/hosts.ini`

# Reset all nodes
`ansible-playbook reset.yml -i inventory/cluster/hosts.ini`

# Upgrade cluster
- Update inventory/cluster/group_vars/all.yml with the expected k3s version
- Run upgrade on master `ansible-playbook upgrade-k3s.yml --limit "master"  -i inventory/cluster/hosts.ini`
- Run upgrade on worker nodes `ansible-playbook upgrade-k3s.yml --limit "node"  -i inventory/cluster/hosts.ini` 

# Reset a single node, remove from cluster
`ansible-playbook reset.yml --limit "worker1"  -i inventory/cluster/hosts.ini`

# Add node to existing cluster - master is included here for the k3s token fact
`ansible-playbook add-node.yml --limit "master,worker1"  -i inventory/cluster/hosts.ini`

# Apply wireguard playbook to single host
`ansible-playbook site.yml --limit "192.168.1.102"  -i inventory/cluster/hosts.ini  --tags=wireguard`

# Apply a configuration update to a single host
`ansible-playbook site.yml --limit "master"  -i inventory/cluster/hosts.ini  --tags=config_update`
