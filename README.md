Extended ECM Public Cloud Edition
================

Module for the Extended ECM Public Cloud Edition widgets.

Contents
--------

The directory structure of this module:

    ./               # Development helpers and settings
      pages/         # Various testing pages
      src/           # Package sources and configuration
        widgets/     # Contains all widgets
      test/          # Test configuration

Installation and First Build
----------------------------

The development has been tested on Windows, OSX and Ubuntu.

1. Install NodeJS 4.4.3 for your platform
2. Install NPM and Grunt command line for your platform:

*On Windows:*

    npm install -g npm@3.8.6
    npm install -g grunt-cli@1.2.0

*On OSX or other OS:*

    sudo npm install -g npm@3.8.6
    sudo npm install -g grunt-cli@1.2.0

3. Install Perforce for your platform and connect it to you nearest p4 proxy
4. Create a directory for the production environment and get the ixmk script:

*On Windows:*

    md xecm_cloud
    cd xecm_cloud
    p4 print //products/comp/Production/1.12-branch/pkg/BUILD/bin/ixmk.bat > ixmk.bat

*On OSX or other OS:*

    mkdir xecm_cloud
    cd xecm_cloud
    p4 print //products/comp/Production/1.12-branch/pkg/BUILD/bin/ixmk.sh > ixmk.sh
    chmod a+x ixmk.sh

5. Create ixmk client specification.  Restrict the build target and requested
   packages to prepare JavaScript development environment only; if you create
   clientspec for the entire component, OScript tools will be required too:

*On Windows:*

    ixmk client -c xecmcloud xecm.cloud:main:XECM_CLOUD_UI

*On OSX or other OS:*

    ./ixmk.sh client -c xecmcloud cs.xecmpf:main:XECM_CLOUD_UI

6. Produce the greeetings component; choose xecm.cloud:main from the p4env menu:

*On Windows:*

    p4env
    cd pkg\XECM_CLOUD_UI
    ixmk compile
    ixmk test

*On OSX or other OS:*

    . p4env
    cd pkg/XECM_CLOUD_UI
    ixmk compile
    ixmk test

Update and Regular Builds
-------------------------

Make sure that you have the latest sources of your component and that new
NodeJS modules added by your colleagues have been installed.  The following
commands run much faster than the full update:

    p4 sync
    npm install
    grunt

Update the complete environment including the CS UI Widgets sources and
produced output from time to time:

    ixmk client -u
    ixmk compile
    ixmk test

Develop
-------

Start the web server to be able to see the code running in the web browser.
You can also use other web server with the web root pointed to the project
root.

    # Start a HTTP server in project root
    node server.js

Open the HTML page to develop with; for example, the
[HelloView Demo](http://localhost:7777/src/widgets/hello/test/index.html).
Edit your sources and refresh the browser page to check the results.
