# custom-httpd-cartridge
Openshift Custom Apache Cartridge

````
rhc cartridge-add https://raw.githubusercontent.com/dol-leodagan/custom-httpd-cartridge/master/metadata/manifest.yml
````

Create _${OPENSHIFT_REPO_DIR}.openshift/custom-httpd.d_ directory, add any _*.conf_ or _*.conf.erb_ files to be parsed by the custom Apache httpd process.


Cartridge Web Root
````
http://${OPENSHIFT_GEAR_DNS}/csthttp/
````


WSGI Example _${OPENSHIFT_REPO_DIR}.openshift/custom-httpd.d/wsgi.conf.erb_ will be available at _/csthttp/my-wsgi_
````
LoadModule wsgi_module modules/python27-mod_wsgi.so
<Directory "<%= ENV['OPENSHIFT_REPO_DIR'] %>/wsgi">
  Order deny,allow
  Allow from all
</Directory>

WSGISocketPrefix run/wsgi
WSGIDaemonProcess processes=2 threads=10
WSGIPassAuthorization On
WSGIScriptAlias /my-wsgi <%= ENV['OPENSHIFT_REPO_DIR'] %>/wsgi/app.wsgi

````


Custom Document Root
````
$OPENSHIFT_CUSTOMHTTPD_DOCUMENT_ROOT
````
