## Open Edx Configuring
Here, I am sharing my experience, ways of solving some problems faced in open edx.

I am using [Open edx Eucalyptus.2 on Ubuntu 12.04](https://openedx.atlassian.net/wiki/display/OpenOPS/Native+Open+edX+Ubuntu+12.04+64+bit+Installation), but my things that I describe below may be usefull for other versions/configurations. 

Also usefull links:
* [Frequently Asked Questions](https://github.com/edx/edx-platform/wiki/Frequently-Asked-Questions)
* [Tools for Open Edx] (https://github.com/edx/edx-tools/wiki)
* 

### First steps to do after installation Open edx
* Change name of platform
* Change organization logo
* Change urls like `localhost:8000` to `my-open-edx.com`
* 

### Configuring SMTP server for sending mails
[Look here](https://openedx.atlassian.net/wiki/display/OpenOPS/How+to+make+SMTP+work+in+your+Open+EdX+fullstack+instance).

Also don't forget to change sender mails.

### Control course creation rights

[Look here](https://github.com/edx/edx-platform/wiki/Controlling-course-creation-rights).

### Solving problems with downloading .CSV reports
I have already described solution [here](https://groups.google.com/d/msg/edx-code/rTI8WO9q4f0/Mi8gmDNZAQAJ). 

### Creating superuser
[Look here](https://groups.google.com/d/msg/openedx-ops/M5ytgpw57EE/MZs41-yIFAAJ).

### Backuping server and restoring it another machine

On first machine, where server is running now:
```
mkdir backup

# backing up mysql db
mysqldump edxapp -u root --single-transaction > backup/backup.sql
cd backup

# backing up mongo db
mongodump --db edxapp
mongodump --db cs_comments_service_development
cd ..

# Packing it to single file for easy copying to second sever
tar -zcvf backup.tar.gz backup/
```

Now, copy backup.tar.gz to second server. For example using `scp`:

`scp backup.tar.gz root@second-server-ip:~/backup.tar.gz`

And then restore backup on second machine:
```
# unpacking
tar -zxvf backup.tar.gz
cd backup

# restoring mysql
mysql -u root edxapp < backup.sql', dir: 'mysql

# cleaning up mongo db and restoring
mongo edxapp --eval "db.dropDatabase()"
mongorestore dump/

```
That's all!

### Updating changes related with assets
```
# CMS:
/edx/bin/edxapp-update-assets-cms
# LMS:
/edx/bin/edxapp-update-assets-lms
```

### Restarting system
```
# CMS:
sudo /edx/bin/supervisorctl restart edxapp:
# LMS:
sudo /edx/bin/supervisorctl restart edxapp_worker:
```
