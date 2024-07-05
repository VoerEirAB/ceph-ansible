#Follow steps to creata a ceph cluster using ceph-ansible
source venv/bin/activate
ansible-playbook -vv  -i inventory infrastructure-playbooks/purge-cluster.yml
ansible -i inventory osds -m shell -a 'sudo ln -sf /dev/sda /dev/disk/by-id/osd;sudo wipefs --all /dev/sda' -l "compute11,compute13,compute14,compute15"
## In case of Voereir16
ansible -i inventory osds -m shell -a 'sudo ln -sf /dev/sdb /dev/disk/by-id/osd;sudo wipefs --all /dev/sdb' -l "compute16"
ansible-playbook -vv  -i inventory site.yml --extra-vars "yes_i_know=true"

##########################
Make sure you have setup the letsencrypt ca-cert in /etc/ssl/certs/ca-certificates.
Otherwise you will get issue of 404 error ceph client unable to connect monitoring tools.
########################
