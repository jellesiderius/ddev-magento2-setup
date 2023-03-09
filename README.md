# DDEV for Magento 2 and sharing my own configuration files (Mac)

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

### Setting up GULP style watching + LiveReload
1. Download and unzip the [https://github.com/jellesiderius/ddev-magento2-example-project/raw/main/google-chrome-extension-livereload-for-ddev.zip](google-chrome-extension-livereload-for-ddev.zip) file and install this for your Chrome Browser: https://support.google.com/chrome_webstore/answer/2664769?hl=en 
2. For your Magento 2 project, download https://github.com/bobmotor/magento-2-gulp and configure according to guide in the repo. Make sure to get at least version 1.5.2

### Configuring your Magento 2 project
Now that the global settings are done, you can start to configure a DDEV environment for a Magento 2 project, you can simply run these commands:
```shell
ddev config --project-type=magento2 --php-version=8.1 --docroot=pub --disable-settings-management --database=mysql:5.7
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
Simply run `DDEV configure-magento-env`. This will automatically setup your `app/etc/env.php` file with Redis configured

### Synchronising databases through SSH
Mage-DB-Sync is compatible with DDEV. Install this with documentation given at https://github.com/jellesiderius/mage-db-sync and your environment will be easily synchronized
