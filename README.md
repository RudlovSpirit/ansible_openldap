Ansible OpenLDAP Установка
Быстрый запуск
1. Подготовка файлов
# Создать файлы:
# inventory.ini, playbook.yml, vars.yml
# Папку templates/ с group.ldif.j2 и user.ldif.j2
2. Настройка inventory
inventory.ini:

[ldap_servers]
ldap-server ansible_host=192.168.3.90 ansible_user=ubuntu

[ldap_servers:vars]
ansible_ssh_private_key_file=~/.ssh/id_rsa
ansible_python_interpreter=/usr/bin/python3
3. Настройка переменных
vars.yml:

ldap_admin_password: "admin123"
ldap_domain: "nodomain"
ldap_organization: "Example Company"
ldap_base_dn: "dc=nodomain"
# ... пользователи и группы
4. Запуск
# Основной запуск:
ansible-playbook -i inventory.ini playbook.yml

# С паролем sudo:
ansible-playbook -i inventory.ini playbook.yml --ask-become-pass

# С подробным выводом:
ansible-playbook -i inventory.ini playbook.yml -vvv
5. Проверка
ssh ubuntu@192.168.3.90 "ldapsearch -x -b dc=nodomain -D cn=admin,dc=nodomain -w admin123"