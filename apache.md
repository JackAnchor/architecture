# apache notes

Apache is a web server software that's pre-installed with a Mac. Web servers (Apache) serve files, but they first must be requested by users (clients).

**Remember** to nderstand where Apache is running from to prevent conflicts and debug efficiently (MAMP, Mac, Homebrew).


## What can Apache deliver?
Some functionality includes:
- Set Default Directory for URLs
- Set Default Language
- Password Protect Login
- Require Specific IP
- Require SSL
- Force HTTP Compression
- Protect Sensitive Files
- Default Charset
- Server Signature
- Force Download


## Apache Configuration Files
Conceptually, .htaccess files override the main server configuration file Using .htaccess files also slows down your Apache server, so avoid if possible To work, .htaccess must be enabled in your pre-installed Apache configuration file. Most functionality is "commented out" by deleting '#'.

**Remember:** the ‘Main' server configuration can be overridden by <VirtualHost> definitions and containers

### Apache .htaccess File
The .htaccess file is an Apache alternative configuration file for Apache. It controls rewriting and other permissions (404 error, redirection, etc.) commonly used by CMS. Additional facts:
- The .htaccess is a hidden “dot” file
- Some plugins must access and modify the htaccess file (301 redirection, SEO, SSL plugins) 
- The .htaccess file should be **secure.** Explore ’ASCII’vs. ’BINARY’ mode to securely upload/transfer files.
- The .htaccess file should be **writable** and **executable.** Explore permissions (i.e. ’755’ or ‘executable’) to address.


#### Terminal Start / Stop Apache

```bash
sudo apachectl start
sudo apachectl stop
```

#### Terminal Apache Details

```bash
// Test for Apache version
httpd -v

// More information (if Apache’s running)
httpd -V

// Process info (if Apache’s running)
ps aux | grep httpd 

//Test for total Apache installs
which -a apachectl
```


#### Server Directory
You can deny access to the entirety of your server's filesystem
You must explicitly permit access to web content directories in other Directory blocks. Existing code:
		<Directory />
		    AllowOverride none
		    Require all denied
		</Directory>

#### Document Root
- The directory out of which you will serve your documents
- The default home for all requests are taken from this directory

	DocumentRoot "/Users/user/Sites"
	<Directory "/Users/user/Sites">
  	<—— additional code —->

#### Options Directive

  Options FollowSymLinks Multiviews
  MultiviewsMatch Any

  Allow Overrides & htaccess 
	AllowOverride None
	Require all granted
    <—— end nested code —->
    </Directory>

#### Directory Index
Files that Apache will serve if a directory is requested.

<IfModule dir_module>
    DirectoryIndex index.html
</IfModule>

#### Passwords protections or .htaccess
To prevent .htaccess viewed by Web clients.

<FilesMatch "^\.([Hh][Tt]|[Dd][Ss]_[Ss])">
    Require all denied
</FilesMatch>

#### Apple specific filesystem protection
<Files "rsrc">
	Require all denied
</Files>
<DirectoryMatch ".*\.\.namedfork">
	Require all denied
  </DirectoryMatch>

#### Error Logs Files
#### LogLevel 
#### LogFormat 
#### Custom Logs

#### Redirects
Allows you to tell clients about documents that used to exist on your server

#### Alias Paths
To access content that does not live under the DocumentRoot.

#### ScriptAlias
Controls which directories contain server scripts.

#### ScriptSocks
To designate the path to the UNIX on threaded servers

#### CGI-Executables
Should be changed to whatever your ScriptAliased CGI directory exists, if you have that configured.

<Directory "/Library/WebServer/CGI-Executables">
   AllowOverride None
 		Options None
   	Require all granted
</Directory>

#### Header Proxy
<IfModule headers_module>
 RequestHeader unset Proxy early
</IfModule>

#### Handlers, Modules, and MIME Types	
<IfModule mime_module>
TypesConfig /private/etc/apache2/mime.types


#### # AddType MIME configuration
#### # AddEncoding Compression Files
#### # AddHandlers
Create a “handlers” file extension to “handlers” to manage set-up (ie YAML)

 #AddHandler cgi-script .cgi
 #AddHandler type-map var
 #AddType SSL parsing overide 
 #AddOutputFilter

<—- end module ——>
</IfModule>

#### Magic Module
The mod_mime_magic module allows the server to use various hints from the contents of the file itself to determine its type.  The MIMEMagicFile directive tells the module where the hint definitions are located. (i.e. ErrorDocument 500 "The server made a boo boo.”)

#### MaxRanges:
Maximum number of Ranges in a request before returning the entire resource, or one of the special

#### EnableMMAP and EnableSendfile:
On systems that support it, memory-mapping or the sendfile syscall may be used to deliver files.  T

#### Supplemental configuration
The configuration files in the /private/etc/apache2/extra/ directory can be included to add extra features or to modify the default configuration of the serve

#### # Language settings
#### # User home directories
#### # Real-time info on requests and configuration
#### # Virtual hosts
#### # Local access to the Apache HTTP Server Manual
#### # Distributed authoring and versioning (WebDAV)
#### # Various default settings
#### # Multi-language error messages

#### Fancy directory listings
Include /private/etc/apache2/extra/httpd-autoindex.conf

#### Server-pool management (MPM specific)
Include /private/etc/apache2/extra/httpd-mpm.conf

#### Configure mod_proxy_html to understand HTML4/XHTML1
<IfModule proxy_html_module>
Include /private/etc/apache2/extra/proxy-html.conf
</IfModule>

#### Secure (SSL/TLS) connections
#Include /private/etc/apache2/extra/httpd-ssl.conf
The following must be present to support starting without SSL on platforms with no /dev/random equivalent
but a statically compiled-in mod_ssl.
<IfModule ssl_module>
	SSLRandomSeed startup builtin
	SSLRandomSeed connect builtin
</IfModule>
Include /private/etc/apache2/other/*.conf
