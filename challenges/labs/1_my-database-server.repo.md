Install MariaDB
sudo yum install mariadb-server
Configurar MariaDB
sudo vi /etc/my.cnf
[mysqld]
transaction-isolation = READ-COMMITTED
# Disabling symbolic-links is recommended to prevent assorted security risks;
# to do so, uncomment this line:
# symbolic-links = 0

key_buffer = 16M
key_buffer_size = 32M
max_allowed_packet = 32M
thread_stack = 256K
thread_cache_size = 64
query_cache_limit = 8M
query_cache_size = 64M
query_cache_type = 1
max_connections = 550
#expire_logs_days = 10
#max_binlog_size = 100M

#log_bin should be on a disk with enough free space. Replace '/var/lib/mysql/mysql_binary_log' with an appropriate path for your system
#and chown the specified folder to the mysql user.
log_bin=/var/lib/mysql/mysql_binary_log

binlog_format = mixed

read_buffer_size = 2M
read_rnd_buffer_size = 16M
sort_buffer_size = 8M
join_buffer_size = 8M

# InnoDB settings
innodb_file_per_table = 1
innodb_flush_log_at_trx_commit  = 2
innodb_log_buffer_size = 64M
innodb_buffer_pool_size = 4G
innodb_thread_concurrency = 8
innodb_flush_method = O_DIRECT
innodb_log_file_size = 512M

[mysqld_safe]
log-error=/var/log/mariadb/mariadb.log
pid-file=/var/run/mariadb/mariadb.pid


Iniciar servicio

sudo systemctl enable mariadb 
$ sudo systemctl list-unit-files | grep mariadb
$ sudo service mariadb start

Ponerle password al root de la base de datos
sudo /usr/bin/mysql_secure_installation

aplicar privilegios
$ sudo /usr/bin/mysql_secure_installation

Instalar el driver de JDBC en todas las maquinas:
wget https://dev.mysql.com/get/Downloads/Connector-J/mysql-connector-java-5.1.31.tar.gz
sudo tar zxvf mysql-connector-java-5.1.31.tar.gz
sudo mkdir -p /usr/share/java/
$ sudo cp mysql-connector-java-5.1.31/mysql-connector-java-5.1.31-bin.jar /usr/share/java/mysql-connector-java.jar

Start the database service and create these databases
create database amon DEFAULT CHARACTER SET utf8;
grant all on scm.* TO 'scm'@'%' IDENTIFIED BY '123qweZ!';
create database scm DEFAULT CHARACTER SET utf8;
grant all on rman.* TO 'rman'@'%' IDENTIFIED BY '123qweZ!';
create database nav DEFAULT CHARACTER SET utf8;
grant all on nav.* TO 'nav'@'%' IDENTIFIED BY '123qweZ!';
create database hive DEFAULT CHARACTER SET utf8;
grant all on hive.* TO 'hive'@'%' IDENTIFIED BY '123qweZ!';
create database oozie DEFAULT CHARACTER SET utf8; 
grant all on oozie.* TO 'oozie'@'%' IDENTIFIED BY '123qweZ!'; 
create database hue DEFAULT CHARACTER SET utf8; 
grant all on hue.* TO 'hue'@'%' IDENTIFIED BY '123qweZ!'; 


