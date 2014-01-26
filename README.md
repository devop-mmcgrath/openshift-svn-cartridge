# OpenShift subversion cartridge

This cartridge can be added to an OpenShift application to give it SVN support instead of git support.  Basically this adds svn binaries to the gear, sets up the correct hooks in svn and calls builds, etc just as git would.  You really should not use this and git at the same time.

This cartridge was intentionally omitted from the [OpenShift Cartridge Guide](http://openshift.github.io/documentation/oo_cartridge_guide.html).
