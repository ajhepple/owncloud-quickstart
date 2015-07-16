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

	rhc app create owncloud php-5.4 postgresql-9.2 cron-1.4 --from-code https://github.com/ajhepple/owncloud-quickstart.git

Head to your application at:

	http://owncloud-$yourdomain.rhcloud.com

Default Credentials
-------------------

The default user is 'admin' and the password should be printed out to console
after deployment. Please change the default password after first login.

To download clients that will sync your ownCloud instance with desktop clients,
visit http://owncloud.org/install/#install-clients

To give your new ownCloud site a web address of its own, add your desired alias:

  rhc add alias owncloud your.domain.com

Then add a cname entry in your domain's dns configuration pointing your alias
to owncloud-domain.rhcloud.com

Apps
----

### Grauphel

[Grauphel](https://github.com/dweiske/grauphel) is a Tomboy notes 
synchronisation server. It depends upon the oauth PHP extension which,
at the time of writing, is not available as a PEAR package and therefore
not available OpenShift via its standard PHP cartridges. Consequently,
*this app is broken in this quickstarter*.
