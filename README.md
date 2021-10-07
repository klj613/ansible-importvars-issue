# Repo to demonstrate a potential Ansible bug

## Setup

```
python -m venv venv
source venv/bin/activate

pip install -rrequirements.txt
```

## Reproduction steps:

```
cd ./roles/role1
ansible-playbook -i 127.0.0.1, ../../playbook.yml
```

Expected result: Get prompted by "role2 imported task" task as per roles/role2/tasks/imported_tasks.yml

Actual result: Got prompted by "role1 imported task" task. roles/role1/tasks/imported_tasks.yml is imported instead of roles/role2/tasks/imported_tasks.yml

Notes:
  - This only happens when import_tasks is used within a import_tasks, which is the reason roles/role2/tasks/middle.yml exists
  - Why are we running ansible from within ./roles/role1? This is what molecule does when testing a role and this issue was first encounted when writing molecule tests for a role
