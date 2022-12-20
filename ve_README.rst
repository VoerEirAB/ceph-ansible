#Follow steps to creata a ceph cluster using ceph-ansible
source venv/bin/activate
ansible-playbook -vv  -i inventory infrastructure-playbooks/purge-cluster.yml
ansible -i inventory osds -m command -a 'sudo lvcreate -n osd -l 100%FREE vgroot'
ansible-playbook -vv  -i inventory site.yml
