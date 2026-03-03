#### Task 1: Key-Value Pairs

person.yaml

```yaml
---
name: Sachin Thokal
role: DevOps Engineer
experinace: 5 years
learning: True
```
---
#### Task 2: Lists

```yaml
---
name: Sachin Thokal
role: DevOps Engineer
experinace: 5 years
learning: True
tools:
    - Kubernetes
    - Docker
    - Linux
    - Azure
    - Prometheus
    - Grafana
hobbies: [Playing, Watching Movies]

# Notes - we can write yml to ways 1st by using "-" and 2nd way is [item1, item2]
```
---
server.yaml
#### Task 3: Nested Objects

```yaml
server:
    name: devops_server
    ip: 192.168.1.1
    port: 22
database:
    host: devops_server.com
    name: devops_server
    credentials:
        user: devops_user
        password: devops_password
```
---
#### Task 4: Multi-line Strings
```yaml
server.yml
---
server:
    name: devops_server
    ip: 192.168.1.1
    port: 22
database:
    host: devops_server.com
    name: devops_server
    credentials:
        user: devops_user
        password: devops_password
# Using | (Literal style) to preserve newlines
startup_script_literal: |
  apt-get update
  apt-get install -y nginx
  systemctl start nginx

# Using > (Folded style) to fold lines into one
startup_script_folded: >
  This long command will be interpreted
  as a single line by the application,
  making it easier to read in this file.

# Notes - when we want run multiple cmd's in yml so we use | and any cmd if you want to run in one single line then use >
```
---
#### Task 6: Spot the Difference
```yml
# Block 1 - correct
name: devops
tools:
  - docker
  - kubernetes
```
```yml
# Block 2 - broken
name: devops
tools:
- docker
  - kubernetes
```
```bash
# Read both blocks and write what's wrong with the second one:
Ans: In 2nd block spacing is wrong in front of - docker.
```
---
What you learned (3 key points)

- I learned how to write yml in standard way.
- Ho we can use spaces while writing yml.
- I learned "list", "|", ">".