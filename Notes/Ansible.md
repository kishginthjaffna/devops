---

# 🧠 DevOps with Ansible on AWS — Notes for Beginners

## 🚨 1. Problem in Traditional Server Management

### 🔧 The Challenge:

Managing many servers (Linux, Windows) usually means writing different scripts for each system.

* 🐌 Time-consuming
* 😵 Error-prone
* 🏗️ Hard to scale

### 💡 The Solution: Configuration Management

These tools help automate server setup, updates, and configurations.

**Popular Tools:**

* 🐍 Ansible
* 🐶 Puppet
* 🍳 Chef
* 🩢 SaltStack

---

## 🌟 2. Why Ansible is Best for AWS DevOps

### ✅ Advantages:

* 🐍 Written in Python → Easy to understand and extend
* 🌌 Ansible Galaxy → Use shared roles/modules
* 🚀 Push-Based → Control machine sends instructions to others directly
* 👻 Agentless → No need to install agents on target servers
* 📜 YAML syntax → Easy to read and write
* 🪠 & 🐧 Works on both Windows (WinRM) and Linux (SSH)
* 🔄 Dynamic Inventory → Use AWS tags to target machines
* 🧱 Backed by Red Hat
* 🌍 Huge community

---

## 🔁 Push vs Pull Mechanism

### ▶️ Ansible (Push Model)

* Admin machine (Control Node) pushes config to other machines (Nodes)
* Uses SSH (Linux) or WinRM (Windows)
* No agents required
* Good for quick updates

### ⬅️ Puppet (Pull Model)

* Nodes pull config from Puppet Master
* Requires agent installation
* Better for enforcing rules continuously

---

## 🔬 3. How Ansible Works

### Key Terms:

* **Inventory**: List of target machines
* **Modules**: Pre-made tasks (e.g., install a package)
* **Tasks**: Use modules to do work
* **Playbook**: YAML file containing tasks

### 📝 Sample Playbook:

```yaml
- name: Install nginx on EC2
  hosts: webservers
  become: yes
  tasks:
    - name: Install nginx
      apt:
        name: nginx
        state: present
```

---

## 📊 4. Ansible vs Puppet

| Feature           | Ansible          | Puppet             |
| ----------------- | ---------------- | ------------------ |
| Architecture      | Push (Agentless) | Pull (Agent-based) |
| Language          | YAML             | Puppet DSL         |
| OS Support        | Linux & Windows  | Mostly Linux       |
| Cloud Integration | Easy & flexible  | Manual             |
| Debugging         | Basic            | Advanced           |

---

## 🚧 5. Disadvantages of Ansible

* 🐛 Debugging is harder
* 🪟 Windows support not as strong as Linux
* 👒 Slower at large scale (no agents)

---

## ☁️ 6. Using Ansible on AWS

* Launch EC2 machines
* SSH or WinRM access needed
* Use tags for dynamic inventory
* Use Ansible modules to:

  * Install software
  * Configure servers
  * Set up networking

---

## 🧪 7. Ad-hoc Commands vs Playbooks

### ⚡ Ad-hoc Commands:

* Run one-off tasks on demand
* Useful for testing or quick fixes

```bash
ansible -i inventory all -m shell -a "df -h"
```

### 📘️ Playbooks:

* Structured YAML files
* Reusable and version-controllable
* Ideal for automation and CI/CD

```bash
ansible-playbook -i inventory playbook.yml
```

---

## 🛠️ 8. Step-by-Step with Ansible

### ✅ Setup:

```bash
ssh-keygen  # Generate SSH keys
```

### ✅ Sample Commands:

```bash
ansible -i inventory all -m shell -a "df"
ansible -i inventory webservers -m shell -a "nproc"
ansible-playbook -i inventory first-playbook.yml
ansible-playbook -vvv -i inventory first-playbook.yml  # Verbose logs
```

---

## ⚙️ 9. Kubernetes Role Folder Structure with Sample Files

Create a role:

```bash
ansible-galaxy role init kubernetes
```

This will create:

```
kubernetes/
├── defaults/main.yml        # Default role variables
├── files/                   # Static files to be copied
├── handlers/main.yml        # Handlers for notifying actions
├── meta/main.yml            # Role dependencies and metadata
├── tasks/main.yml           # List of tasks
├── templates/               # Jinja2 templates
├── tests/                   # Test playbooks
│   ├── inventory
│   └── test.yml
└── vars/main.yml            # Other variables
```

### 📁 `defaults/main.yml`

```yaml
---
install_kube: true
```

### 📁 `handlers/main.yml`

```yaml
---
- name: restart kubelet
  service:
    name: kubelet
    state: restarted
```

### 📁 `meta/main.yml`

```yaml
---
dependencies: []
```

### 📁 `tasks/main.yml`

```yaml
---
- name: Install Docker
  apt:
    name: docker.io
    state: present
  become: true

- name: Add Kubernetes APT key
  apt_key:
    url: https://packages.cloud.google.com/apt/doc/apt-key.gpg
    state: present

- name: Add Kubernetes repo
  apt_repository:
    repo: deb http://apt.kubernetes.io/ kubernetes-xenial main
    state: present

- name: Install Kubernetes components
  apt:
    name: ['kubeadm', 'kubelet', 'kubectl']
    state: present
  become: true
```

### 📁 `vars/main.yml`

```yaml
---
kube_version: "1.29.0"
```

### 📁 `tests/test.yml`

```yaml
---
- hosts: all
  roles:
    - kubernetes
```

### 📁 `tests/inventory`

```ini
[all]
localhost ansible_connection=local
```

---

## 📚 Helpful Documentation for DevOps with Ansible on AWS

### 🧠 Core Concepts

* [What is Configuration Management?](https://www.redhat.com/en/topics/automation/what-is-configuration-management)
* [Introduction to Ansible](https://docs.ansible.com/ansible/latest/user_guide/index.html)
* [Ansible for Beginners (Official Docs)](https://docs.ansible.com/ansible/latest/getting_started/index.html)

### ☁️ Using Ansible with AWS

* [Ansible EC2 Dynamic Inventory Guide](https://docs.ansible.com/ansible/latest/collections/amazon/aws/aws_ec2_inventory.html)
* [Managing AWS with Ansible](https://docs.ansible.com/ansible/latest/scenario_guides/guide_aws.html)
* [AWS EC2 Documentation](https://docs.aws.amazon.com/ec2/)
* [Using SSH with EC2](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/AccessingInstancesLinux.html)

### 🔁 Push vs Pull Tools

* [Ansible vs Puppet](https://www.redhat.com/en/topics/automation/ansible-vs-puppet)

### 🛠️ Key Ansible Features

* [Ansible Playbooks Guide](https://docs.ansible.com/ansible/latest/user_guide/playbooks.html)
* [Ansible Galaxy Roles](https://galaxy.ansible.com/)
* [Ad-hoc Commands Documentation](https://docs.ansible.com/ansible/latest/user_guide/intro_adhoc.html)
* [Ansible Role Directory Structure](https://docs.ansible.com/ansible/latest/dev_guide/developing_roles.html)

---

### ❤️ Made with love by **Kishgi**