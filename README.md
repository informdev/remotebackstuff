The following allows me to passwordlessly connect to a remote server, rsync generated backups from that server, then it creates tar files of the backups, daily, and deletes any that are more than 5 days old.

**# create ssh key:**
ssh-keygen

**copy ssh key to remote server:**<br />
ssh-copy-id -i ~/.ssh/id_rsa.pub ubuntu@111.111.111.111

**create file - name it backup.sh**
rsync -a --rsync-path "sudo -u root rsync" ubuntu@111.111.111.111:/var/backup/greenarrow /home/take/;
tar -zcf /home/backup/daily/backup-$(date +%Y%m%d).tar.gz -C /home/take/greenarrow/*;
find /home/backup/daily/* -mtime +5 -delete

**setup cron job**
15 0 * * * sh /root/backup.sh
