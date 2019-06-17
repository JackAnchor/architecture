# apache notes

Apache is a web server software that's pre-installed with a Mac. Web servers (Apache) serve files, but they first must be requested by users (clients).

##### Remember
**Understand where Apache is running from to prevent conflicts (MAMP, Mac, Homebrew)

### Apache Modifications & Permissions in .htaccess File
Web projects generally need Apache rewriting permissions (404 error, redirection, etc.) 
- Modify Apache Permissions in .htaccess File
- Website needs Apache rewriting permissions (404 error, redirection, etc.) 
- The .htaccess file is an Apache (web server) configuration file that controls these rewriting permissions
- The .htaccess is a hidden “dot” file
- Some plugins must access and modify the htaccess file (301 redirection, SSL ), etc. 
- The .htaccess file should be secure. Explore ’ASCII’vs. ’BINARY’ mode to securely upload/transfer files.
- The .htaccess file should be writable and executable. Explore permissions (i.e. ’755’ or ‘executable’) to address.

## What can Apache modifications deliver?
Web projects generally need Apache rewriting permissions (404 error, redirection, etc.) 
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



#### Start / Stop Apache

```bash
sudo apachectl start
sudo apachectl stop
```

#### Apache Details

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
