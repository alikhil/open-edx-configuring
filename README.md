## Open Edx Configuring
Here, I am sharing my experience, ways of solving some problems faced in open edx.

I am using [Open edx Eucalyptus.2 on Ubuntu 12.04](https://openedx.atlassian.net/wiki/display/OpenOPS/Native+Open+edX+Ubuntu+12.04+64+bit+Installation), but my things that I describe below may be usefull for other versions/configurations. 

Also usefull links:
* (Frequently Asked Questions)[https://github.com/edx/edx-platform/wiki/Frequently-Asked-Questions]
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

## Solving problems with downloading .CSV reports
I have already described solution [here](https://groups.google.com/d/msg/edx-code/rTI8WO9q4f0/Mi8gmDNZAQAJ). 

## Creating superuser
[Look here](https://groups.google.com/d/msg/openedx-ops/M5ytgpw57EE/MZs41-yIFAAJ).

### Updating changes related with assets
CMS:
```
/edx/bin/edxapp-update-assets-cms
```
LMS:
```
/edx/bin/edxapp-update-assets-lms
```

### Restarting system
CMS:
```
sudo /edx/bin/supervisorctl restart edxapp:
```
LMS:
```
sudo /edx/bin/supervisorctl restart edxapp_worker:
```
