# OpenShift subversion cartridge

This cartridge can be added to an OpenShift application to give it SVN support instead of git support.  Basically this adds svn binaries to the gear, sets up the correct hooks in svn and calls builds, etc just as git would.  You really should not use this and git at the same time.

This is a community supported cartridge looking for additional maintainers, let me know if you actually use SVN and want to take ownership of the community cart.  My SVN-fu is weak

# How to use

Create an app:

    rhc app create svnkitchensink -t jbossas-7


Add SVN:

    rhc cartridge add -a svnkitchensink https://raw.github.com/mmcgrath-openshift/openshift-svn-cartridge/master/metadata/manifest.yml

Follow the directions to clone new svn repo and remove your git repo (Note, you can't sanely use both svn and git together)

    rm -rf svnkitchensink
    svn co svn+ssh://52e68ea64382ec116d000cf6@svnkitchensink-mmcgrath.rhcloud.com/svnkitchensink

Get some sourcecode and populate your repo!  (In this case rails)

    wget -O /tmp/master.zip https://github.com/openshift/kitchensink-example/archive/master.zip
    unzip -d /tmp/master /tmp/master.zip
    rsync -av /tmp/master/kitchensink-example-master/ ./svnkitchensink/
    rm -rf ./svnkitchensink/.git/
    cd svnkitchensink
    svn add * .openshift/ --force

Commit and push.  Note this will build in the background.  It takes some time.

    svn commit -m "initial svn push"

# TODO
* Get build output, right now svn squashes it
* Test all frameworks
* Fix the SVN binaries that are stored in the git repo (ick)
* Ruby behaves strangely (it's slow)
* Figure out jenkins builds
