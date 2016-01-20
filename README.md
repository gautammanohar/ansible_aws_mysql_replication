### AWS multi-master circular replication

This playbook attempts to achieve the following :

- Create 3 Ubuntu 14.04 instances
- Each of these instances are created in a separate region. The ami's used are :
  - Oregon [ami-5189a661]
  - Ireland [ami-47a23a30]
  - Singapore [ami-96f1c1c4]
- For the purpose of this test, I used t2.micro instances. You may change this as required.
- For each region and the instance that is hosted in that region, the playbook creates a VPC and a public subnet inside the VPC
- The playbook also creates a security group, with relevant ports opened.

### Usage
```sh
$ ansible-playbook provisioner.yml
```

### Master/Slave maps.
As the heading suggests, this playbook implements circular replication. Therefore each master is also a slave of another master. In group_vars/all, attention should be paid to the slave_maps dict. For instance this dict :
```sh
slave_maps:
  oregon: ireland
  ireland: singapore
  singapore: oregon

```
suggests that the instance in Oregon is the master of the instance in Ireland, one in Ireland is the master of Singapore and finally , instance in Singapore is the master of the instance in Oregon.


This playbook can manage 3+ masters given that the **slave_maps** is correctly set.