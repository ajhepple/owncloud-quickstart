OpenShift quickstarter for [OwnCloud](http://owncloud.org) with custom apps
===========================================================================

Originally an export of 
[OpenShift's own quickstart](https://github.com/openshift/owncloud-openshift-quickstart),
this repository simply adds my preferred owncloud apps and discards the
cumbersome history of that repository.  If you care more about using 
[OpenShift](http://www.openshift.com) maintained code than my choice of 
ownCloud apps and the size of your repository then use their quickstarter.

Running on OpenShift
--------------------

Create an account at https://www.openshift.com, install the client tools 
and set them up.

Create a PHP application with database and cron cartridges:

	$ rhc app create owncloud php-5.4 postgresql-9.2 cron-1.4 --from-code https://github.com/ajhepple/owncloud-quickstart.git

Head to your application at:

	http://owncloud-yourdomain.rhcloud.com

Default Credentials
-------------------

The default user is 'admin' and the password should be printed out to console
after deployment. Please change the default password after first login.

To download clients that will sync your ownCloud instance with desktop clients,
visit http://owncloud.org/install/#install-clients

To give your new ownCloud site a web address of its own, add your desired alias:

<<<<<<< 1496e66c8cdd86ce0d419d8ed72734fb7de30191
    $ rhc alias-add owncloud your.domain.com
=======
    rhc add alias owncloud your.domain.com
>>>>>>> Update README with quota issue

Then add a cname entry in your domain's dns configuration pointing your alias
to owncloud-domain.rhcloud.com

Apps
----

### Grauphel

[Grauphel](https://github.com/cweiske/grauphel) is a Tomboy notes 
synchronisation server. It depends upon the oauth PHP extension which,
at the time of writing, is not available as a PEAR package and therefore
not available OpenShift via its standard PHP cartridges. Consequently,
<<<<<<< 1496e66c8cdd86ce0d419d8ed72734fb7de30191
*the app is broken in this quickstarter*.

### GPX Viewer

A GPX file viewer is provided by
[files_gpx_viewer](https://github.com/Frank1604/files_gpxviewer_extended)
which appears to be a maintained fork of another similar
[plugin](https://github.com/Restless123/Owncloud-GPXviewer).
*this app is broken in this quickstarter*.

Issues
------

### Disk quota exceeded (June 2017)

The OwnCloud application failed to restart due to exceeding the openhift
disk quota of 1024MB.

To troubleshoot this issue, I logged in via SSH (command given when logged
into OpenShift website) and using the command

    du -hs *

to establish which directories/files were using the most storage space.
It turned out that the directory ~/app-root/data was using half of the storage
and the directories

    ~/app-root/data/anthony/files
    ~/app-root/data/anthony/files_trashbin
    ~/app-root/data/anthony/cache

comprised most of the exceeded quota.

I was then able to get the application started again by running the command

  `rhc app-tidy owncloud`

from the local working copy of owncloud (It may be necessary to install the
deprecated rhc tool.) but this did not solve the inherent problem of too many
files (real, deleted and cached). By logging on to the OwnCloud web interface
I was able to delete files in the trash and by removing many photographs from
remote (OwnCloud) storage I was able to free up enough space. I suspect that
I must live with the cache.

*Lesson learnt* OpenShift's basic free plan does not provide enough storage
for photographs, videos or other memory hogging files.
