OJS-CAS
=======

OJS-CAS is a plugin for [Open Journal Systems](http://pkp.sfu.ca/ojs/) that integrates the [Central Authentication Service](http://www.jasig.org/cas) (CAS) protocol via OJS' implicit authentication mechanism.  This document describes the config parameters that control the implicit authentication plugin in OJS. It does not describe how to set up CAS based authentication.

Setup
-----

1.	Place plug-in in "plugins/implicitAuth" relative to your OJS install.

2.	Either remove the shibbolth plugin, or comment out its implicitAuth hook in "ShibAuthPlugin.inc.php" on line 26

3.	Configure the casAuth.php file. Enter your CAS server settings near the top of the file on lines 6 - 9.

4.	Enable implicit auth in your OJS config (see below).


OJS Config File
---------------

In the [security] section of the config.inc.php file there are several parameters that affect the operation of the implicit auth plugin. They are all commented out - by default. They are shown here with their default settings like they are in the config file. When you enable implicit auth - you should uncomment all of these variables.

    implicit_auth = On

This setting turns on or off implicit authentication. If implicit_auth is not on - none of the other implicit_auth variables are consulted. The main effect of turning implicit_auth on - is that the login process goes through CAS and several of the forms are modified so that they do not ask the user for name and address type information.

Implicit Auth Header Variables. These variables supply the name of the header variable that contains a specific value. For example -- the user's first name - will be in the header variable HTTP_TDL_GIVENNAME.

	implicit_auth_header_email = HTTP_MAIL
	implicit_auth_header_uin = HTTP_UID
    
The implicit_auth_admin_list is a blank delimited list of email addresses that should be set up as an admin user. When a user logs in - if their email address is in this list then they are made an admin user. This list is checked every time a user logs in and if they are not in the list - then their admin privilege is revoked.

    implicit_auth_admin_list = "jdoe@email.ca jshmo@email.ca"

The implicit_auth_wayf_url is the URL of the CAS Authentication page. This should point to the casAuth.php file in the cas plugin folder, relative to the web server's root.

    implicit_auth_wayf_url = "/ojs/plugins/implicitAuth/cas/casAuth.php"

LICENSE
-------

This plugin is licensed under the terms of the [MIT Free Software license](http://en.wikipedia.org/wiki/MIT_License).  See the file LICENSE for more information.