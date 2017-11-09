# Ansible Elasticsearch

This is a Ansible role to install Elasticsearch (Support Ubuntu14/16, CentOS7)

## Requirements

Ansible 2.x

## Role Variables

|Variable|Default Value|Description|
|---|---|---|
```es_cluster_name```|es_cluster|elasticsearch cluster name.
```es_api_port```|9200|the api listen port.
```es_transport_port```|9300|the transport listen port.
```elasticsearch_hosts```|['127.0.0.1']|you must replace this value, enter the listen address of each elasticsear node. or pass to ansible-playbook as extra variable: {'elasticsearch_address':['10.89.155.78','10.89.155.79']}.
```curator_venv_path```|/home/curator_env|virtualenv path for curator.
```curator_log_path```|/home/curator_env/curator.log|log path for curator.
```curator_index_keep_day```|3|elasticsearch index keep days.
```curator_packages```|['click==6.7','elasticsearch==2.4.1', 'PyYAML==3.12', 'voluptuous==0.9.3', 'elasticsearch-curator==4.2.5']|package lists for curator.

## Example
```
### create a requirements.yml
- src: git+https://github.com/willyhutw/ansible-role-elasticsearch.git
  name: elasticsearch

### create a playbook.yml
- hosts: all
  become: yes
  roles:
    - roles/elasticsearch

### install this role
ansible-galaxy install -r requirements.yml -p ./roles

### run it!
ansible-playbook -i '192.168.33.101,' playbook.yml \
-e "ansible_ssh_user=willyhu ansible_ssh_pass=secret ansible_become_pass=secret" \
-e '{"elasticsearch_hosts":["10.0.2.11"]}'

### run it with multi-node cluster mode
ansible-playbook -i '192.168.33.101,192.168.33.102,192.168.33.103,' playbook.yml \
-e "ansible_ssh_user=willyhu ansible_ssh_pass=secret ansible_become_pass=secret" \
-e '{"elasticsearch_hosts":["192.168.33.101","192.168.33.102","192.168.33.103"]}'

## License

MIT / BSD

## Author Information

willyhu.tw@gmail.com
