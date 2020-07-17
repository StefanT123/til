# CRON for database backup

### Database backups

1. Create backup database
```sql
GRANT LOCK TABLES, SELECT, SHOW VIEW, REPLICATION CLIENT ON *.* TO 'db_user_backups'@'%' IDENTIFIED BY '{COMPLEX-PASSWORD}';
```

2. Configure MySQL to properly restore stored procedures
```sql
SET GLOBAL log_bin_trust_function_creators = 1;
```

3. Setup the necessarily directory structure and files needed
```bash
# create backup directory with environment and log file
sudo mkdir /backups && cd /backups
sudo touch .env db-backup.sh db-backup.log
sudo chmod -R 775 /backups
sudo chmod -R g+s /backups
sudo chmod +x db-backup.sh

# add mysql backup user credentials into environment file
echo "export MYSQL_USER=db_user_backups" > /backups/.env
echo "export MYSQL_PASS={COMPLEX-PASSWORD}" >> /backups/.env
```

4. Create `db-backup.sh`
```bash
DB_NAMES=( 'db1' 'db2' 'db3' ) #replace with your own database name(s)
BKUP_NAMES=()
BKUP_DIR="/backups"

# get total number of directories
total_dbs=${#DB_NAMES[@]}

# create backup file names
for (( i=0; i<${total_dbs}; i++ )); do
    BKUP_NAMES[$i]="`date +%Y%m%d%H%M`-backup-$${DB_NAMES[$i]}.sql.gz"
done

# get backup users credentials
source $BKUP_DIR/.env

# create backups
for (( i=0; i<${total_dbs}; i++ )); do
    # NOTE: --routines flag makes sure stored procedures are also backed up
    mysqldump --routines -u ${MYSQL_USER} -p${MYSQL_PASS} | gzip > ${BKUP_DIR}/${BKUP_NAMES[$i]}
done
```

### Setup Cronjob

1. Open crontab
```bash
crontab -e
```

2. Setup cron to run daily
```bash
0 0 * * * /usr/bin/env bash /backups/db-backup.sh &>> /backups/db-backup.log
```
To test it, we can set it up to run every minute
```bash
* * * * * /usr/bin/env bash /backups/db-backup.sh &>> /backups/db-backup.log
```
