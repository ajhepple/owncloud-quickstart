[ownCloud](http://owncloud.org) quickstarter for OpenShift with custom apps
=========================

Originally an export of [OpenShift's own quickstart](https://github.com/openshift/owncloud-openshift-quickstart),
this repository simply adds my preferred owncloud apps and discards the
cumbersome history of that repository.  If you care more about using OpenShift
maintained code than my choice of ownCloud apps and the size of your repository
then use their quickstarter.

Running on OpenShift
--------------------

Create an account at https://www.openshift.com

Create a PHP application with a MySQL cartridge:

	rhc app create owncloud php-5.4 mysql-5.5 cron-1.4

or with PostgreSQL cartridge:

	rhc app create owncloud php-5.4 postgresql-9.2 cron-1.4

Add this upstream ownCloud quickstart repo

	cd owncloud
	git remote add upstream -m master git://github.com/ajhepple/owncloud-openshift-quickstart.git
	git pull -s recursive -X theirs upstream master

Push back to your OpenShift repo

	git push        

Head to your application at:

	http://owncloud-$yourdomain.rhcloud.com

Default Credentials
-------------------

The default user is 'admin' and the password should be printed out to console
after deployment. Please change the default password after first login.

To download clients that will sync your ownCloud instance with desktop clients, visit http://owncloud.org/sync-clients/

To give your new ownCloud site a web address of its own, add your desired alias:

	rhc app add-alias -a owncloud --alias "$whatever.$mydomain.com"

Then add a cname entry in your domain's dns configuration pointing your alias to $whatever-$yourdomain.rhcloud.com.

Apps
----

### Grauphel

[Grauphel](https://github.com/dweiske/grauphel) is a Tomboy notes 
synchronisation server. It depends upon the oauth PHP extension which,
at the time of writing, is not available as a PEAR package and therefore
not available OpenShift via its standard PHP cartridges. Consequently,
*this app is broken in this quickstarter*.
