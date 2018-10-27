ansible-aws-ecs-task-service
=========

This role create AWS elastic container services task and service integrated with ALB

Requirements
------------

```sh
Ansible >= 2.4.0.0
boto
boto3
botocore
json
```


Role Variables
--------------
In vars/main.yml

```sh
#Example var file for create ecs task definition and service, attach to target group and run task
task_service:
  #AWS region where run ecs cluster
  aws_ecs_region: "eu-central-1"
  #Example task name
  aws_ecs_task_name: "example-task"
  #Example application name
  aws_ecs_app_name: "example-app"
  #Example target group where are your to want attach service. The target group should be created.
  #To create the target group you can use https://github.com/unicanova/ansible-lc-asg-aws 
  aws_ecs_tg_name: "exapmle-tg"
  #Example ecs cluster name where are your to want attach service. The ecs ecs cluster should be created.
  #To create the ecs ecs cluster you can use https://github.com/unicanova/ansible-lc-asg-aws 
  aws_ecs_cluster_name: "example-ecs-cluster"
  #Example ecs service name
  aws_ecs_service_name: "example-service"
  #Example ecs role
  aws_ecs_ecs_role: "arn:aws:iam::123456789012:role/ecsServiceRole"
  #Image name, you can use image from docker public hub or private registry
  aws_ecs_image: "nginx"
  #A revision number for the ecs task definition
  aws_ecs_revision_namber: "1"
  #Container port
  aws_ecs_container_port: "80"
  #Host port for mapping to container port
  aws_esc_host_port: "80"
  #The number of cpu units to reserve for the container. Max 1024 * vCPU
  aws_esc_cpu: "100"
  #The amount (in MiB) of memory used by the task.
  aws_ecs_memory: "500"
```

Example Playbook
----------------

Export enviroment variables with AWS credentials:
```sh
export AWS_ACCESS_KEY_ID=YOUR_AWS_ACCESS_KEY_ID
export AWS_SECRET_ACCESS_KEY=YOUR_AWS_SECRET_ACCESS_KEY
```

Create dir when you clone ansible role from github:
```sh
mkdir -p example/Roles
cd example
```

Clone role repository from github and configure ansible:
```sh
cd Roles
git clone https://github.com/unicanova/ansible-aws-ecs-task-service
cd ..
```

Edit ansible.cfg
```sh
[defaults]
hostfile = ./hosts.cfg
remote_user = root
host_key_checking = False
timeout = 5
pipelining = True
roles_path = Roles
```

Edit site.yaml
```sh
- hosts: 127.0.0.1
  connection: local
  roles:
   - { role: ansible-aws-ecs-task-service, tags: 'test' }
```

Run anisble:
```sh
ansible-playbook site.yaml -t test
```

License
-------

MIT

Author Information
------------------
Author: Sergey Ovsienko 

Email: so@unicanova.com

Company: UnicaNova 

Website: https://unicanova.com/

