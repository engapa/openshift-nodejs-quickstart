Custom version Node[.js] on PDI's OpenShift PaaS QuickStart [![Build Status](https://travis-ci.org/engapa/openshift-nodejs-quickstart.png)](https://travis-ci.org/engapa/openshift-nodejs-quickstart)
=================================================
***

Create the server by RHC client
-------------------------------

<a href="https://broker.ose.hi.inet/">Create an account</a> and install the <a href="https://www.openshift.com/get-started">command-line client tools</a>.

Create a DIY application using **from-code** option:

    rhc app create -a tomcat -t diy-0.1 --from-code "https://github.com/engapa/openshift-tomcat-DIY-quickstart.git"

That's it, you can now checkout your tomcat at:
    http://tomcat-$yournamespace.rhcloud.com

The default managing account is **tomcat/tomcat**; this can be changed by altering the 
start action hook file, committing the change within your secure OpenShift
Git account and issuing another <code>git push</code>.

Create the server from web console
----------------------------------

Add this entry to file /etc/openshift/quickstarts.json in broker host :

```json
{"quickstart": {
    "id":"5",
    "href":"https://broker.ose.hi.inet/quickstarts/nodejs",
    "name":"PDI - Nodejs",
    "summary":"Custom Nodejs version application.",
    "body":"Change <b>.openshift/markers/NODEJS_VERSION<\/b> end-line value according to desired nodejs version  , default value is 0.6.20.",
    "cartridges":"nodejs-0.6",
    "website":"http://nodejs.org/",
    "language":"Java",
    "tags":"PDI, nodejs, script",
    "initial_git_url":"https://github.com/eng30/openshift-nodejs-quickstart.git",
    "provider":"PDI",
    "admin_tags":[]
  }}
```

An <a href="https://broker.ose.hi.inet/console/application_types/quickstart!5">item for this QuickStart</a> should be appear in OpenShift web console. You must to provide the name of this application only.

Selecting a Node version to install/use
---------------------------------------

The action_hooks in this application will use that NODEJS_VERSION marker
file to download and extract that Node version if it is available on
nodejs.org and will automatically set the paths up to use the node/npm
binaries from that install directory.

     See: .openshift/action_hooks/ for more details.

    Note: The last non-blank line in the .openshift/markers/NODEJS_VERSION
          file determines the version it will install (default version is 0.6.20.).

If you want to change Node.js version (example v0.10.10) then update the marker file **.openshift/markers/NODEJS_VERSION** and commit it:

    echo 0.10.10 >> .openshift/markers/NODEJS_VERSION
    git commit . -m 'Node version 0.10.10'
    git push

That's all, you can now checkout your application at:

    http://nodejs-$yournamespace.ose.hi.inet
    ( See env @ http://nodejs-$yournamespace.ose.hi.inet/env , or via **rhc ssh nodejs** from client and perform **node -v**)

License
-------
This code is dedicated to the PDI domain