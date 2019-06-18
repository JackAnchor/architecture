# Apache notes
Apache is a web server software that's pre-installed on most Macs. Web servers (Apache) serve files, but they must first be requested by users (clients).  To **prevent conflicts** and **debug** efficiently, it's important to understand where Apache is running from **(MAMP, Mac, Homebrew)** and whether it's running or needs restarting.

## What can Apache deliver?
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


## Apache configuration files
Apache has two primary configuration files. The .htaccess file is an alternative configuration file that overrides the main server configuration file. Using this file slows-down your Apache server, so it's best to avoid if possible. It's often required by most CMS systems.

To enable .htaccess, it must be declared in your pre-installed Apache configuration file. Most functionality is "commented out" by deleting '#' or modifying minor keywords.

**Remember:** the ‘Main' server configuration can be overridden by <VirtualHost> definitions and containers.

### Apache .htaccess file
The .htaccess file controls rewriting and other permissions (404 error, redirection, etc). Additional facts:
- The .htaccess is a hidden “dot” file
- Some plugins must access and modify the .htaccess file (301 redirection, SEO, SSL plugins) 
- The .htaccess file should be **secure.** Explore ’ASCII’vs. ’BINARY’ mode to securely upload/transfer files.
- The .htaccess file should be **writable** and **executable.** Explore permissions (i.e. ’755’ or ‘executable’) to address.


### SEO friendly URLs and Apache
Having a website with "SEO friendly URLs" is a fairly straightforward concept. Informative, user-friendly urls have been known to impact click-through-rates on search. If you're unfamiliar, [Google provides some resources here.](http://www.google.com/support/webmasters/bin/answer.py?answer=76329)

Apache mod_rewrite can help you convert URLs into a more SEO-friendly format.
- http://httpd.apache.org/docs/current/mod/mod_rewrite.html
- https://www.digitalocean.com/community/tutorials/how-to-set-up-mod_rewrite


#### Terminal Start / Stop Apache

```
sudo apachectl start
sudo apachectl stop
```

#### Terminal Apache Details

```
// Test Apache version
httpd -v

// More information (if Apache’s running)
httpd -V

// Process info (if Apache’s running)
ps aux | grep httpd 

//Test total Apache installs
which -a apachectl
```


#### Server Directory
You can deny access to the entirety of your server's filesystem
You must explicitly permit access to web content directories in other Directory blocks.
```
<Directory />
AllowOverride none
Require all denied
</Directory>
```

#### Document Root
- The directory out of which you will serve your documents
- The default home for all requests are taken from this directory
- Local dev change

```
DocumentRoot "/Users/user/Sites"
<Directory "/Users/user/Sites">
<—— .code —->
```

#### Options Directive
```
Options FollowSymLinks Multiviews
MultiviewsMatch Any

Allow Overrides & htaccess
AllowOverride None
Require all granted
<—— .end —->
</Directory>
  ```

#### Directory Index
Files that Apache will serve if a directory is requested.

```
<IfModule dir_module>
DirectoryIndex index.html
</IfModule>
```

#### Passwords protections or .htaccess
To prevent .htaccess viewed by Web clients.
```
<FilesMatch "^\.([Hh][Tt]|[Dd][Ss]_[Ss])">
Require all denied
</FilesMatch>
```

#### Apple specific filesystem protection
```
<Files "rsrc">
Require all denied
</Files>
<DirectoryMatch ".*\.\.namedfork">
  Require all denied
</DirectoryMatch>
 ```

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
```
<Directory "/Library/WebServer/CGI-Executables">
AllowOverride None
Options None
Require all granted
</Directory>
```

#### Header Proxy
```
<IfModule headers_module>
 RequestHeader unset Proxy early
</IfModule>
```

#### Handlers, Modules, and MIME Types	
```
<IfModule mime_module>
TypesConfig /private/etc/apache2/mime.types
```

#### # AddType MIME configuration
#### # AddEncoding Compression Files
#### # AddHandlers
Create a “handlers” file extension to “handlers” to manage set-up (ie YAML)

 #AddHandler cgi-script .cgi
 #AddHandler type-map var
 #AddType SSL parsing overide 
 #AddOutputFilter

```
<—- .end ——>
</IfModule>
```

#### Magic Module
The mod_mime_magic module allows the server to use various hints from the contents of the file. (i.e. ErrorDocument 500 "The server made a boo boo.”)

#### MaxRanges
Maximum number of Ranges in a request before returning the entire resource, or one of the special


#### EnableMMAP and EnableSendfile
On systems that support it, memory-mapping or the sendfile syscall may be used to deliver files.


#### Supplemental configuration
The configuration files in the /private/etc/apache2/extra/ directory can be included to add extra features or modify the default configuration of the server


#### # Language settings
#### # User home directories
#### # Real-time info on requests and configuration
#### # Virtual hosts
#### # Local access to the Apache Server Manual
#### # Distributed authoring and versioning (WebDAV)
#### # Default settings
#### # Multi-language error messages


#### Fancy directory listings
```
Include /private/etc/apache2/extra/httpd-autoindex.conf
```

#### Server-pool management
```
Include /private/etc/apache2/extra/httpd-mpm.conf
```

#### Configure mod_proxy_html
```
<IfModule proxy_html_module>
Include /private/etc/apache2/extra/proxy-html.conf
</IfModule>
```

#### Secure (SSL/TLS) connections
To support starting without SSL on platform.
```
<IfModule ssl_module>
 SSLRandomSeed startup builtin
 SSLRandomSeed connect builtin
</IfModule>
Include /private/etc/apache2/other/*.conf
```
