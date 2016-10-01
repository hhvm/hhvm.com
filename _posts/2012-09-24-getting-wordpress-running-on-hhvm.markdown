---
author: sgolemon
comments: true
layout: post
title: Getting WordPress running on HHVM
category: blog
redirect_from:
  - /blog/3095/getting-wordpress-running-on-hhvm
---

This article aims to walk through the installation process for getting WordPress running on HHVM (HipHop Virtual Machine).

<!--truncate-->

## Installing HHVM

For the sake of this case-study, I used Ubuntu "Precise" 12.04 as my linux distribution since I'd be able to [install from a simple binary package](https://github.com/facebook/hiphop-php/wiki/Prebuilt-packages-on-ubuntu-12.04).  Instructions are currently available for [building for Ubuntu 12.04](https://github.com/facebook/hiphop-php/wiki/Building-and-installing-HHVM-on-Ubuntu-12.04) yourself, or [building for CentOS 6.3](https://github.com/facebook/hiphop-php/wiki/Building-and-installing-HHVM-on-CentOS-6.3).  Other distros will probably work with some effort, and you're encouraged to try.

## Unpacking Wordpress

Head to [wordpress.org/download](http://wordpress.org/download) to grab the [latest tar.gz](http://wordpress.org/latest.tar.gz) version of Wordpress and unpack it in a suitable location.  For the purposes of this post, I'll be using _/var/www/wp/_


     $ cd /var/www
     $ wget 'http://wordpress.org/latest.tar.gz'
     $ tar -zxf latest.tar.gz
     $ mv wordpress wp

##  Making a few... tweaks

**Update:** As of WordPress 3.9, and HHVM 2.0 the following changes aren't necessary as WP have updated their codebase to play nice with HHVM, and HHVM has updated itself to support more PHP stuff.  Isnt' Open Source awesome? :)

<del>Wordpress doesn't quite work "right out of the box" with HHVM because a few of HipHop's behaviors differ from the PHP it was built for.</del>

<del>First, case-insensitive constants are simply not supported by HipHop.  They're a bit silly, rarely used, and are more expensive (computationally) than they're worth.  Fortunately, wordpress only uses this feature in one place (to maintain BC with older plugins), and we can work around it by defining the most common variants.</del>

<del>Open up _wp-includes/wp-db.php_ and look for the line which defines the _'OBJECT'_ constant (line 20 in my version).  We'll want to take off the third parameter saying to declare it case-insensitively, and add in the lower-case and drop-case versions as alternates. This should be enough to cover 99% of plugins out there.</del>

<pre>
<del>
define('OBJECT', 'OBJECT');
define('Object', 'OBJECT');
define('object', 'OBJECT');
</del>
</pre>


<del>The rest of the changes are actually just temporary work-arounds for fixes which will be in HipHop in the next week or so.  **I'll update this post as those fixes reach github.**</del>

<del>As of this writing,_ ini_get('post_max_size')_ will return an empty string, and _ini_get('upload_max_filesize')_ will return a size in megabytes, but without the '_M_' suffix, so it is interpreted as bytes.  Fixes for both of these are currently pending, so just set them both manually for now.</del>

<pre>
<del>
// wp-admin/includes/template.php in wp_max_upload_size()

#$u_bytes = wp_convert_hr_to_bytes(ini_get('upload_max_filesize'));
#$p_bytes = wp_convert_hr_to_bytes(ini_get('post_max_size'));
$u_bytes =
$p_bytes = 100 << 20; // 100MB, or whatever you'll be setting
</del>
</pre>


**Update**: Both _post_max_size_ and _upload_max_filesize_ have been updated to return sane values and these changes are no longer required.

<del>_magic_quotes_runtime_ is (happily) not supported by HipHop.  _get_magic_quotes_runtime_() probably should have just quietly returned false, but for whatever reason it was implemented as throwing a "not implemented" exception.  A fix for this is currently pending, so hard-code a zero (false) for now.</del>

<pre>
<del>
// wp-admin/includes/class-pclzip.php in privDisableMagicQuotes()
#$this->magic_quotes_status = @get_magic_quotes_runtime();
$this->magic_quotes_status = 0;</del>

// wp-includes/class-phpmailer.php in EncodeFile()
#$magic_quotes = get_magic_quotes_runtime();
$magic_quotes = 0;
</del>
</pre>

**Update**: _get_magic_quotes_runtime()_ has been updated to always return 0 (false) rather than throwing an exception.  This tweak no longer needs to be made.

## Create a config file

The syntax for HipHop's web server is pretty extensive, but the following placed in _/etc/hhvm.hdf_ should be enough to get you going.  Refer to [options.compiled](https://github.com/facebook/hiphop-php/blob/master/doc/options.compiled) for other settings.


    // /etc/hhvm.hdf

    Server {
      Port = 80
      SourceRoot = /var/www/
    }

    Eval {
      Jit = true
    }
    Log {
      Level = Error
      UseLogFile = true
      File = /var/log/hhvm/error.log
      Access {
        * {
          File = /var/log/hhvm/access.log
          Format = %h %l %u %t "%r" %>s %b
        }
      }
    }

    VirtualHost {
      * {
        Pattern = .*
        RewriteRules {
          dirindex {
            pattern = ^/(.*)/$
            to = $1/index.php
            qsa = true
          }
        }
      }
    }

    StaticFile {
      FilesMatch {
        * {
          pattern = .*.(dll|exe)
          headers {
            * = Content-Disposition: attachment
          }
        }
      }
      Extensions {
        css = text/css
        gif = image/gif
        html = text/html
        jpe = image/jpeg
        jpeg = image/jpeg
        jpg = image/jpeg
        png = image/png
        tif = image/tiff
        tiff = image/tiff
        txt = text/plain
      }
    }


You may wish to add other directives and static file extensions, but this will get you started.  The RewriteRule is to accomodate the fact that HipHop does not (currently) support a DirectoryIndex style directive.  While this feature is currently in development, we can get by with a general case rewrite rule.


## Start the webserver

Pretty straight-forward, just press go:


    sudo /usr/bin/hhvm --mode daemon --user web --config /etc/hhvm.hdf


Assuming of course you have a user designated for your web server to run as named 'web'.  Rename this one as needed.

## Wordpress setup


From here, setup follows the normal "[Famous 5 Minute Installation](http://codex.wordpress.org/Installing_WordPress)".  If you run into any trouble, check that you updated system files as described above, look into your error.log, or leave a comment here or on our [Facebook Page](https://www.facebook.com/pages/HipHop-for-PHP/282425744325).
