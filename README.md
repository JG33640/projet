# Déploiement du CMS JOOMLA sur une base de données Maria DB

ATTENTION, les packages par défaut pour la configuration **Debian Ubuntu** du rôle geerlingguy.mysql sont erronés.
La base de données n'est pas fonctionnelle avec les packages mysql.

Il faut vérifier dans le fichier **roles.d/geerlingguy.mysql/vars/Debian.yml** ci-dessous la présence des packages suivants : 
  - mariadb-client
  - mariadb-server
  - python3-mysqldb

```
---
__mysql_daemon: mysql
__mysql_packages:
  - mariadb-client
  - mariadb-server
  - python3-mysqldb
mysql_log_file_group: adm
__mysql_slow_query_log_file: /var/log/mysql/mysql-slow.log
__mysql_log_error: /var/log/mysql/mysql.err
__mysql_syslog_tag: mysql
__mysql_pid_file: /var/run/mysqld/mysqld.pid
__mysql_config_file: /etc/mysql/my.cnf
__mysql_config_include_dir: /etc/mysql/conf.d
__mysql_socket: /var/run/mysqld/mysqld.sock
__mysql_supports_innodb_large_prefix: true

```


Le playbook suivant doit être exécuté : 


```
---
- name: Installation de JOOMLA
  hosts: all 
  become: true

  roles:
    - role: joomla
      when: ansible_hostname == "srvweb"
    
    - role: geerlingguy.mysql
      mysql_root_password: joomla
      mysql_databases:
        - name: joomla
      mysql_users:
        - name: joomla
          host: '%' 
          password: joomla
          priv: "joomla.*:ALL"
      when: ansible_hostname == "srvdb"
```

