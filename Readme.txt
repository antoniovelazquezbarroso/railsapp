#  README

# To provision with vagrant just run vagrant up


# To provision with digital ocean or AWS
# Uncomment in /playbooks/provision.yml file the provisioner to be used
# Play the /playbooks/provision.yml playbook on the corresponding inventory file
    $ ansible-playbook -i inventories/digitalocean/inventory playbooks/provision.yml
    $ ansible-playbook -i inventories/aws/inventory playbooks/provision.yml


# To install the required roles defined at requirements.yml
    $ ansible-galaxy install -r requirements.yml
# The installation folder is /roles because of the configuration in ansible.cfg

# =========================================================================================================
# IF YOU REINSTALL THE ROLES (from ansible-galaxy), CHECK FOR REQUIRED AMMENDMENTS at:

#   role mysql/tasks/users.yml, añadir ignore_errors= true en linea 13

#   role nrpe-client/tasks/main.yml añadir validate_certs=no al final de linea 17 (task Get NRPE)

#   role backup/templates/backup.sh.j2, incluir monit check
#        (añadir NOW=$(date +"%T"), y
#         echo "LAST BACKUP RUN WAS $NOW" > /home/backup/backup_conf/backups_timestamp_monit_watch ,
#         para poder vigilar la antiguedad de este archivo, y alertar si > 3h [ proceso de backup fallando])

#   role backup/templates/backup.sh.j2, corregir errata
#        (sobra 1 espacio trás signo = en MYSQL_CREDENTIALS= "-u {{... , lo que hace fallar los MysqlDumps)


#   role backup/defaults/main.yml, cambiar backup_mysql a false para no hacer por default MysqlDump,
#        lo que daría errores en los equipos sin MySQL. Así es fácil hacer override a true de backup_mysql,
#        asignándola de modo condicional [ p.e. backup_mysql: ('db' in groupnames)] ver common/backup/vars.yml
#        o definirla con host_vars/group_vars adecuados.
# ==========================================================================================================

## Building the VMs

  1. Download and install [VirtualBox](https://www.virtualbox.org/wiki/Downloads).
  2. Download and install [Vagrant](http://www.vagrantup.com/downloads.html).
  3. [Mac/Linux only] Install [Ansible](http://docs.ansible.com/intro_installation.html).
  4. Run `ansible-galaxy install -r requirements.yml` in this directory to get the required Ansible roles.
  5. Run `vagrant up` to build the VMs and configure the infrastructure.
