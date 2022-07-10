---
- name: setup application server
  hosts: dbservers
  remote_user: ubuntu
  become: true

  tasks:
    - name: enable epel repository
      yum: name=epel-release state=present
    
    - name: install basic tools
      yum: name={{ item }} state=present
      with_items: 
        - git 
        - nmap