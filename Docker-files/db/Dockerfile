FROM mysql:8.0.33
LABEL "project"="Vpro_test"
LABEL "NAME"="madhava"
ENV MYSQL_ROOT_PASSWORD="testpasswd"
ENV MYSQL_DATABASE="accounts"
ADD db_backup.sql /docker-entrypoint-initdb.d/db_backup.sql
