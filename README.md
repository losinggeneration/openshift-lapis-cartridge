## Openshift Lapis Cartridge

A cartridge for openshift that enables Lapis with OpenResty to be used as the web server.


### Installation

To install this cartridge use the cartridge reflector when creating an app

	rhc create-app myapp http://lapis-losinggeneration.rhcloud.com/binary/manifest/0.1.0

Alternatively, to use a more bleeding edge version, you may use

	rhc create-app myapp http://lapis-losinggeneration.rhcloud.com/binary/manifest/master

The cartridge uses the CDK to build the binaries required for the cartridge. If, for some reason, http://lapis-losinggeneration.rhcloud.com ever goes away or you want to test/make changes, you can create your own CDK application and push this code there and create your own builds.

### Configuration

The cartridge installs two config files. One at <code>$OPENSHIFT_LAPIS_DIR/conf/nginx.conf</code> which gets loaded by the executable
and sets up specific app configuration such as logs and pid files.

The config then includes another nginx.conf which must exist at <code>$OPENSHIFT_REPO_DIR/nginx.conf</code>. This config should
contain all your server specific set up including which ip/port to listen on.

The repo nginx.conf is actually seen in your repository as <code>nginx.conf.erb</code> so environment variables can be used
in the config. Every time the server starts it first processes <code>nginx.conf.erb</code>.

The default template assumes your application is app.moon. The .openshift/action_hooks/build will use $MOONC to build app.moon upon push for deployments.

A <code>static/</code> folder is included where static content is served by default. However, as can be seen in the <code>nginx.conf.erb</code> file it is entirely configurable and only exists as a form of documentation.
