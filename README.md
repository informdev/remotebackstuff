The following allows me to passwordlessly connect to a remote server, rsync generated backups from that server, then it creates tar files of the backup, daily, and deletes any that are more than 5 days old.<br /><br />

**# create ssh key:**<br />
ssh-keygen

**copy ssh key to remote server:**<br />
ssh-copy-id -i ~/.ssh/id_rsa.pub ubuntu@111.111.111.111

**create file - name it backup.sh**<br />
rsync -a --rsync-path "sudo -u root rsync" ubuntu@111.111.111.111:/var/backup/greenarrow /home/take/;<br />
tar -zcf /home/backup/daily/backup-$(date +%Y%m%d).tar.gz -C /home/take/greenarrow/*;<br />
find /home/backup/daily/* -mtime +5 -delete<br />

**setup cron job**<br />
15 0 * * * sh /root/backup.sh
