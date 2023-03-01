Role Name
=========

Le rôle installe le CMS JOOMLA et les paquets Apache, php sur l'hôte srvweb défini dans l'inventaire. 

Role Variables
--------------
Ci-dessous le contenu du fichier default/main.yml.
L'url de téléchargement doit être précisée avec la variable **joomla_dist_url**


```
---
# defaults file for roles.d/joomla

# Url de téléchargement de JOOMLA
joomla_dist_url: "https://downloads.joomla.org/cms/joomla4/4-2-8/Joomla_4-2-8-Stable-Full_Package.zip"

# Si True , téléchargement depuis {{joomla_dist_url}}
# Si False, l'archive d'installation doit être dans ~/projet
joomla_deploy_from_web: true

# Force reinstall - Force l'écrasement de la dernière archive installée
joomla_force_reinstall: false

# Nom du site
joomla_site_name: "joomla"
# Propriétaire et groupe affectés au site
joomla_site_owner: "www-data"
joomla_site_group: "www-data"

# Répertoire d'installation de JOOMLA
joomla_install_dir: "/var/www/html/{{joomla_site_name}}"

# Nom de domaine
joomla_domain: "joomla.mycompany.com"

```

Exemple de Playbook
----------------

    - hosts: srvweb
      roles:
         - joomla

License
-------

BSD

