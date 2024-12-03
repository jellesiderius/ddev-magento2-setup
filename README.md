# DDEV for Magento 2 and sharing my own configuration files

## Before you start
Install DDEV through installation guide: https://ddev.readthedocs.io/

## Setting up DDEV configuration files
After installing DDEV, follow the following steps

### Setting up .bashrc for your DDEV shell environment
1. Navigate to `~/.ddev`
2. If the folder `~/.ddev/homeadditions` is not present yet, create this
3. Now navigate to `~/.ddev/homeadditions`
4. Create a `~/.ddev/homeadditions/.bashrc` file, containing the following:
```bash
parse_git_branch() {
     git branch 2> /dev/null | sed -e '/^[^*]/d' -e 's/* \(.*\)/[\1]/'
}
export PS1='\[\e[00;33m\][\t]\[\e[0m\]\[\e[00;37m\]-\[\e[0m\]\[\e[00;36m\][\h]\[\e[0m\]\[\e[00;37m\]-$(parse_git_branch)-\[\e[0m\]\[\e[00;31m\][\w]\[\e[0m\]\[\e[0m\]$ \[\e[0m\]'
export LS_COLORS='rs=0:di=38;5;27:ln=38;5;51:mh=44;38;5;15:pi=40;38;5;11:so=38;5;13:do=38;5;5:bd=48;5;232;38;5;11:cd=48;5;232;38;5;3:or=48;5;232;38;5;9:mi=05;48;5;232;38;5;15:su=48;5;196;38;5;15:sg=48;5;11;38;5;16:ca=48;5;196;38;5;226:tw=48;5;10;38;5;16:ow=48;5;10;38;5;21:st=48;5;21;38;5;15:ex=38;5;34:*.tar=38;5;9:*.tgz=38;5;9:*.arc=38;5;9:*.arj=38;5;9:*.taz=38;5;9:*.lha=38;5;9:*.lz4=38;5;9:*.lzh=38;5;9:*.lzma=38;5;9:*.tlz=38;5;9:*.txz=38;5;9:*.tzo=38;5;9:*.t7z=38;5;9:*.zip=38;5;9:*.z=38;5;9:*.Z=38;5;9:*.dz=38;5;9:*.gz=38;5;9:*.lrz=38;5;9:*.lz=38;5;9:*.lzo=38;5;9:*.xz=38;5;9:*.bz2=38;5;9:*.bz=38;5;9:*.tbz=38;5;9:*.tbz2=38;5;9:*.tz=38;5;9:*.deb=38;5;9:*.rpm=38;5;9:*.jar=38;5;9:*.war=38;5;9:*.ear=38;5;9:*.sar=38;5;9:*.rar=38;5;9:*.alz=38;5;9:*.ace=38;5;9:*.zoo=38;5;9:*.cpio=38;5;9:*.7z=38;5;9:*.rz=38;5;9:*.cab=38;5;9:*.jpg=38;5;13:*.jpeg=38;5;13:*.gif=38;5;13:*.bmp=38;5;13:*.pbm=38;5;13:*.pgm=38;5;13:*.ppm=38;5;13:*.tga=38;5;13:*.xbm=38;5;13:*.xpm=38;5;13:*.tif=38;5;13:*.tiff=38;5;13:*.png=38;5;13:*.svg=38;5;13:*.svgz=38;5;13:*.mng=38;5;13:*.pcx=38;5;13:*.mov=38;5;13:*.mpg=38;5;13:*.mpeg=38;5;13:*.m2v=38;5;13:*.mkv=38;5;13:*.webm=38;5;13:*.ogm=38;5;13:*.mp4=38;5;13:*.m4v=38;5;13:*.mp4v=38;5;13:*.vob=38;5;13:*.qt=38;5;13:*.nuv=38;5;13:*.wmv=38;5;13:*.asf=38;5;13:*.rm=38;5;13:*.rmvb=38;5;13:*.flc=38;5;13:*.avi=38;5;13:*.fli=38;5;13:*.flv=38;5;13:*.gl=38;5;13:*.dl=38;5;13:*.xcf=38;5;13:*.xwd=38;5;13:*.yuv=38;5;13:*.cgm=38;5;13:*.emf=38;5;13:*.axv=38;5;13:*.anx=38;5;13:*.ogv=38;5;13:*.ogx=38;5;13:*.aac=38;5;45:*.au=38;5;45:*.flac=38;5;45:*.mid=38;5;45:*.midi=38;5;45:*.mka=38;5;45:*.mp3=38;5;45:*.mpc=38;5;45:*.ogg=38;5;45:*.ra=38;5;45:*.wav=38;5;45:*.axa=38;5;45:*.oga=38;5;45:*.spx=38;5;45:*.xspf=38;5;45:'
alias ls='ls --color=auto'
```

### Setting up custom commands for DDEV 
Now navigate to `~/.ddev/commands/web`. If this folder structure is not present yet, create this. You should create the following files:

`~/.ddev/commands/web/magerun`:
```bash
#!/bin/bash

#ddev-generated
## Description: Run Magerun CLI inside the web container
## Usage: magerun [flags] [args]
## Example: "ddev magerun list" or "ddev magerun maintenance:enable" or "ddev magerun sampledata:reset"
## ProjectTypes: magento2
## ExecRaw: true

if [ ! -f bin/magento ]; then
  echo 'bin/magento does not exist in your project root directory.'
  echo 'Please verify that you installed the shop in your project directory.'
  exit 1
fi

magerun "$@"
```

`~/.ddev/commands/web/magerun2`:
```bash
#!/bin/bash

#ddev-generated
## Description: Run Magerun2 CLI inside the web container
## Usage: magerun2 [flags] [args]
## Example: "ddev magerun2 list" or "ddev magerun2 maintenance:enable" or "ddev magerun2 sampledata:reset"
## ProjectTypes: magento2
## ExecRaw: true

if [ ! -f bin/magento ]; then
  echo 'bin/magento does not exist in your project root directory.'
  echo 'Please verify that you installed the shop in your project directory.'
  exit 1
fi

magerun2 "$@"
```

`~/.ddev/commands/web/configure-magento-env`:
```bash
#!/bin/bash

#ddev-generated
## Description: Configures the env.php file
## Usage: configure-magento-env
## Example: "configure-magento-env"
## ProjectTypes: magento2
## ExecRaw: true

if [ ! -f bin/magento ]; then
  echo 'bin/magento does not exist in your project root directory.'
  echo 'Please verify that you installed the shop in your project directory.'
  exit 1
fi

bin/magento setup:config:set --db-host=db \
--db-name=db \
--db-user=db \
--db-password=db \
--cache-backend-redis-server=redis \
--cache-backend-redis-port=6379 \
--cache-backend-redis-db=0 \
--session-save=redis \
--session-save-redis-host=redis \
--session-save-redis-port=6379 \
--session-save-redis-log-level=3 \
--session-save-redis-db=1 \
--session-save-redis-disable-locking=1 \
--backend-frontname=admin \
-n;
```

`~/.ddev/commands/web/watch-cache`:
```bash
#!/bin/bash

#ddev-generated
## Description: Magento 2 Cache Watcher
## Usage: watch-cache [flags] [args]
## Example: "ddev watch-cache"
## ProjectTypes: magento2
## ExecRaw: true

if [ ! -f ~/.composer/vendor/mage2tv/magento-cache-clean/bin/cache-clean.js ]; then
    composer global require mage2tv/magento-cache-clean
fi

~/.composer/vendor/mage2tv/magento-cache-clean/bin/cache-clean.js --watch
```

`~/.ddev/commands/web/watch-styles`:
```bash
#!/bin/bash

#ddev-generated
## Description: Watches LESS changes for your Magento project
## Usage: watch-styles --THEME_NAME
## Example: "ddev watch-styles"
## ProjectTypes: magento2
## ExecRaw: true

gulp exec --$@;
gulp less --$@;
gulp watch-styles --$@ --live;
```

You have now added the following commands for DDEV:
- `ddev magerun`
- `ddev magerun2`
- `ddev configure-magento-env`
- `ddev watch-cache`
- `ddev watch-styles`

### Setting up GULP style watching + LiveReload
1. Download and unzip the [google-chrome-extension-livereload-for-ddev.zip](google-chrome-extension-livereload-for-ddev.zip) file and install this for your Chrome Browser: https://support.google.com/chrome_webstore/answer/2664769?hl=en 
2. For your Magento 2 project, download https://github.com/bobmotor/magento-2-gulp and configure according to guide in the repo. Make sure to get at least version 1.5.2
3. Now after setting up step 1 & 2, your browser extension should be available to watch your style changes in Magento. Click on the LiveReload chrome extension button after your project is fired up and `ddev watch-styles YOURTHEMENAME` is started

### Configuring your Magento 2 project
Now that the global settings are done, you can start to configure a DDEV environment for a Magento 2 project, you can run these commands:
```shell
ddev config --project-type=magento2 --php-version=8.3 --docroot=pub --disable-settings-management --database=mysql:8.0
ddev get ddev/ddev-elasticsearch
ddev get ddev/ddev-redis
```

After setting up the config files, add this to your project's `MAGENTO_ROOT_FOLDER/.ddev/config.yaml`:
```yaml
web_extra_exposed_ports:
  - name: LiveReload
    container_port: 35729
    http_port: 35729
    https_port: 35730
```

Make sure to add a `app/etc/env.php` file with the correct database settings:
```php
'db' => [
    'table_prefix' => '',
    'connection' => [
        'default' => [
            'host' => 'db',
            'dbname' => 'db',
            'username' => 'db',
            'password' => 'db',
            'model' => 'mysql4',
            'engine' => 'innodb',
            'initStatements' => 'SET NAMES utf8;',
            'active' => '1',
            'driver_options' => [
                1014 => false
            ]
        ]
    ]
]
```

### Starting up your DDEV project
Now that everything is set up, you can start the project by running `ddev start`

### Configuring Redis for your project
Run `DDEV configure-magento-env`. This will automatically setup your `app/etc/env.php` file with Redis configured

### Configuring Varnish for your project
1. Run `ddev get ddev/ddev-varnish`
2. In magento set caching to varnish in admin config
3. Add VCL file to .ddev/varnish/default.vcl:
```bash
# VCL version 5.0 is not supported so it should be 4.0 even though actually used Varnish version is 6
vcl 4.0;

import std;
# The minimal Varnish version is 6.0
# For SSL offloading, pass the following header in your proxy server or load balancer: 'X-Forwarded-Proto: https'

backend default {
    .host = "web";
    .port = "80";
    .first_byte_timeout = 600s;
}

acl purge {
    "web";
}

sub vcl_recv {
    if (req.restarts > 0) {
        set req.hash_always_miss = true;
    }

    if (req.method == "PURGE") {
        if (client.ip !~ purge) {
            return (synth(405, "Method not allowed"));
        }
        # To use the X-Pool header for purging varnish during automated deployments, make sure the X-Pool header
        # has been added to the response in your backend server config. This is used, for example, by the
        # capistrano-magento2 gem for purging old content from varnish during it's deploy routine.
        if (!req.http.X-Magento-Tags-Pattern && !req.http.X-Pool) {
            return (synth(400, "X-Magento-Tags-Pattern or X-Pool header required"));
        }
        if (req.http.X-Magento-Tags-Pattern) {
          ban("obj.http.X-Magento-Tags ~ " + req.http.X-Magento-Tags-Pattern);
        }
        if (req.http.X-Pool) {
          ban("obj.http.X-Pool ~ " + req.http.X-Pool);
        }
        return (synth(200, "Purged"));
    }

    if (req.method != "GET" &&
        req.method != "HEAD" &&
        req.method != "PUT" &&
        req.method != "POST" &&
        req.method != "TRACE" &&
        req.method != "OPTIONS" &&
        req.method != "DELETE") {
          /* Non-RFC2616 or CONNECT which is weird. */
          return (pipe);
    }

    # We only deal with GET and HEAD by default
    if (req.method != "GET" && req.method != "HEAD") {
        return (pass);
    }

    # Bypass customer, shopping cart, checkout
    if (req.url ~ "/customer" || req.url ~ "/checkout") {
        return (pass);
    }

    # Bypass health check requests
    if (req.url ~ "^/(pub/)?(health_check.php)$") {
        return (pass);
    }

    # Set initial grace period usage status
    set req.http.grace = "none";

    # normalize url in case of leading HTTP scheme and domain
    set req.url = regsub(req.url, "^http[s]?://", "");

    # collect all cookies
    std.collect(req.http.Cookie);

    # Remove all marketing get parameters to minimize the cache objects
    if (req.url ~ "(\?|&)(gclid|cx|ie|cof|siteurl|zanpid|origin|fbclid|mc_[a-z]+|utm_[a-z]+|_bta_[a-z]+)=") {
        set req.url = regsuball(req.url, "(gclid|cx|ie|cof|siteurl|zanpid|origin|fbclid|mc_[a-z]+|utm_[a-z]+|_bta_[a-z]+)=[-_A-z0-9+()%.]+&?", "");
        set req.url = regsub(req.url, "[?|&]+$", "");
    }

    # Static files caching
    if (req.url ~ "^/(pub/)?(media|static)/") {
        # Static files should not be cached by default
        return (pass);

        # But if you use a few locales and don't use CDN you can enable caching static files by commenting previous line (#return (pass);) and uncommenting next 3 lines
        #unset req.http.Https;
        #unset req.http.X-Forwarded-Proto;
        #unset req.http.Cookie;
    }

    # Bypass authenticated GraphQL requests without a X-Magento-Cache-Id
    if (req.url ~ "/graphql" && !req.http.X-Magento-Cache-Id && req.http.Authorization ~ "^Bearer") {
        return (pass);
    }

    return (hash);
}

sub vcl_hash {
    if ((req.url !~ "/graphql" || !req.http.X-Magento-Cache-Id) && req.http.cookie ~ "X-Magento-Vary=") {
        hash_data(regsub(req.http.cookie, "^.*?X-Magento-Vary=([^;]+);*.*$", "\1"));
    }

    # To make sure http users don't see ssl warning
    if (req.http.X-Forwarded-Proto) {
        hash_data(req.http.X-Forwarded-Proto);
    }


    if (req.url ~ "/graphql") {
        call process_graphql_headers;
    }
}

sub process_graphql_headers {
    if (req.http.X-Magento-Cache-Id) {
        hash_data(req.http.X-Magento-Cache-Id);

        # When the frontend stops sending the auth token, make sure users stop getting results cached for logged-in users
        if (req.http.Authorization ~ "^Bearer") {
            hash_data("Authorized");
        }
    }

    if (req.http.Store) {
        hash_data(req.http.Store);
    }

    if (req.http.Content-Currency) {
        hash_data(req.http.Content-Currency);
    }
}

sub vcl_backend_response {

    set beresp.grace = 3d;

    if (beresp.http.content-type ~ "text") {
        set beresp.do_esi = true;
    }

    if (bereq.url ~ "\.js$" || beresp.http.content-type ~ "text") {
        set beresp.do_gzip = true;
    }

    if (beresp.http.X-Magento-Debug) {
        set beresp.http.X-Magento-Cache-Control = beresp.http.Cache-Control;
    }

    # cache only successfully responses and 404s that are not marked as private
    if ((beresp.status != 200 && beresp.status != 404) || beresp.http.Cache-Control ~ "private") {
        set beresp.uncacheable = true;
        set beresp.ttl = 86400s;
        return (deliver);
    }

    # validate if we need to cache it and prevent from setting cookie
    if (beresp.ttl > 0s && (bereq.method == "GET" || bereq.method == "HEAD")) {
        # Collapse beresp.http.set-cookie in order to merge multiple set-cookie headers
        # Although it is not recommended to collapse set-cookie header,
        # it is safe to do it here as the set-cookie header is removed below
        std.collect(beresp.http.set-cookie);
        # Do not cache the response under current cache key (hash),
        # if the response has X-Magento-Vary but the request does not.
        if ((bereq.url !~ "/graphql" || !bereq.http.X-Magento-Cache-Id)
         && bereq.http.cookie !~ "X-Magento-Vary="
         && beresp.http.set-cookie ~ "X-Magento-Vary=") {
           set beresp.ttl = 0s;
           set beresp.uncacheable = true;
        }
        unset beresp.http.set-cookie;
    }

    # If page is not cacheable then bypass varnish for 2 minutes as Hit-For-Pass
    if (beresp.ttl <= 0s ||
        beresp.http.Surrogate-control ~ "no-store" ||
        (!beresp.http.Surrogate-Control &&
        beresp.http.Cache-Control ~ "no-cache|no-store") ||
        beresp.http.Vary == "*") {
        # Mark as Hit-For-Pass for the next 2 minutes
        set beresp.ttl = 120s;
        set beresp.uncacheable = true;
    }

    # If the cache key in the Magento response doesn't match the one that was sent in the request, don't cache under the request's key
    if (bereq.url ~ "/graphql" && bereq.http.X-Magento-Cache-Id && bereq.http.X-Magento-Cache-Id != beresp.http.X-Magento-Cache-Id) {
        set beresp.ttl = 0s;
        set beresp.uncacheable = true;
    }

    return (deliver);
}

sub vcl_deliver {
    if (obj.uncacheable) {
        set resp.http.X-Magento-Cache-Debug = "UNCACHEABLE";
    } else if (obj.hits) {
        set resp.http.X-Magento-Cache-Debug = "HIT";
        set resp.http.Grace = req.http.grace;
    } else {
        set resp.http.X-Magento-Cache-Debug = "MISS";
    }

    # Not letting browser to cache non-static files.
    if (resp.http.Cache-Control !~ "private" && req.url !~ "^/(pub/)?(media|static)/") {
        set resp.http.Pragma = "no-cache";
        set resp.http.Expires = "-1";
        set resp.http.Cache-Control = "no-store, no-cache, must-revalidate, max-age=0";
    }

    if (!resp.http.X-Magento-Debug) {
        unset resp.http.Age;
    }
    unset resp.http.X-Magento-Debug;
    unset resp.http.X-Magento-Tags;
    unset resp.http.X-Powered-By;
    unset resp.http.Server;
    unset resp.http.X-Varnish;
    unset resp.http.Via;
    unset resp.http.Link;
}

sub vcl_hit {
    if (obj.ttl >= 0s) {
        # Hit within TTL period
        return (deliver);
    }
    if (std.healthy(req.backend_hint)) {
        if (obj.ttl + 300s > 0s) {
            # Hit after TTL expiration, but within grace period
            set req.http.grace = "normal (healthy server)";
            return (deliver);
        } else {
            # Hit after TTL and grace expiration
            return (restart);
        }
    } else {
        # server is not healthy, retrieve from cache
        set req.http.grace = "unlimited (unhealthy server)";
        return (deliver);
    }
}
```
4. Run `bin/magento setup:config:set --http-cache-hosts=varnish:80`

### Setting up multistore configuration
In your project folder `MAGENTO_ROOT_FOLDER/.ddev/nginx_full` add a `magento-stores.conf` containing the following:
```nginx
map $http_host $mage_run_code {
    default '';
    store1.ddev.site storecode1;
    store2.ddev.site storecode2;
    store3.ddev.site storecode3;
}
```
Next, open up your project's `MAGENTO_ROOT_FOLDER/.ddev/config.yaml` and add additional hostnames:
```yaml
additional_hostnames:
  - store1
  - store2
  - store3
```
If you're using [Mage-DB-Sync](https://github.com/jellesiderius/mage-db-sync), your can add a `.mage-db-sync-config.json` to your Magento root folder:
```json
{
  "core_config_data": {
    "0": {
      "web/unsecure/base_url": "https://store.ddev.site/",
      "web/secure/base_url": "https://store.ddev.site/"
    },
    "1": {
      "web/unsecure/base_url": "https://store1.ddev.site/",
      "web/secure/base_url": "https://store1.ddev.site/"
    },
    "2": {
      "web/unsecure/base_url": "https://store2.ddev.site/",
      "web/secure/base_url": "https://store2.ddev.site/"
    },
    "3": {
      "web/unsecure/base_url": "https://store3.ddev.site/",
      "web/secure/base_url": "https://store3.ddev.site/"
    }
  }
}
```
_Note: The "1", "2", "3" are your store codes._

### Synchronising databases through SSH
[Mage-DB-Sync](https://github.com/jellesiderius/mage-db-sync) is compatible with DDEV. Install this with documentation given at https://github.com/jellesiderius/mage-db-sync and your environment will be easily synchronized
