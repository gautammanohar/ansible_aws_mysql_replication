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