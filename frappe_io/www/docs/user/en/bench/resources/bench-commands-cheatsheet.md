<!-- base_template: frappe_io/www/frappe/frappe_base.html --><!-- add-breadcrumbs -->
# Bench Commands Cheatsheet

### General Usage

* `bench --version` - Show bench version
* `bench version` - Show version of all apps
* `bench src` - Show bench repo directory
* `bench --help` - Show all commands and help
* `bench [command] --help` - Show help for command
* `bench init [bench-name]` - Create a new bench (Run from home dir)
  * `--python TEXT`                   Path to Python Executable.
  * `--ignore-exist`                  Ignore if Bench instance exists.
  * `--apps_path TEXT`                path to json files with apps to install after init
  * `--frappe-path TEXT`              path to frappe repo
  * `--frappe-branch TEXT`            path to frappe repo
  * `--clone-from TEXT`               copy repos from path
  * `--clone-without-update`          copy repos from path without update
  * `--no-procfile`                   Pull changes in all the apps in bench
  * `--no-backups`                    Run migrations for all sites in the bench
  * `--no-auto-update`                Build JS and CSS artifacts for the bench
  * `--skip-redis-config-generation`  Skip redis config generation if already specifying the common-site-config file
  * `--verbose`                       Verbose output during install

* `bench --site [site-name] COMMAND` - Specify site for command
* `bench update` - Pulls changes for bench-repo and all apps, applies patches, builds JS and CSS, and then migrates.
  * `--pull`                Pull changes in all the apps in bench
  * `--patch`               Run migrations for all sites in the bench
  * `--build`               Build JS and CSS artifacts for the bench
  * `--bench`               Update bench
  * `--requirements`        Update requirements
  * `--restart-supervisor`  restart supervisor processes after update
  * `--no-backup`			  Don't take a backup before update
* `bench restart` Restart all bench services
* `bench backup` Create a backup of the default site.

  Backup will be saved to `~/frappe-bench/sites/{your site}/private/backups/`.

* `bench backup-all-sites` Backup all sites
  * `--with-files` Backup site with files
* `bench restore` Restore
  * `--with-private-files` Restore site with private files (Path to tar file)
  * `--with-public-files` Restore site with public files (Path to tar file)
* `bench migrate` Run patches, sync schema and rebuild files/translations
  * `--rebuild-website TEXT` Rebuild webpages after migration
* `bench migrate-env [python-version]` Will migrate the virtual environment to the desired python version
* `bench --site [sitename] set-admin-password [password]` Will reset the administrator password
* `bench destroy-all-sessions` Destroys all sessions


### Config

* `bench config` - Change bench configuration
  * `auto_update [on/off]`          Enable/Disable auto update for bench
  * `dns_multitenant [on/off]`      Enable/Disable DNS Multitenancy
  * `http_timeout`                  Set http timeout
  * `restart_supervisor_on_update`  Enable/Disable auto restart of supervisor
  * `serve_default_site`            Configure nginx to serve the default site on
  * `update_bench_on_update`        Enable/Disable bench updates on running bench...
* `bench setup` - Setup components
  * `auto-update`  Add cronjob for bench auto update
  * `backups    `  Add cronjob for bench backups
  * `config     `  overwrite or make config.json
  * `env        `  Setup virtualenv for bench
  * `nginx      `  generate config for nginx
  * `procfile   `  Setup Procfile for bench start
  * `production `  setup bench for production
  * `redis      `  generate config for redis cache
  * `socketio   `  Setup node deps for socketio server
  * `sudoers    `  Add commands to sudoers list for execution...
  * `supervisor `  generate config for supervisor
  * `add-domain `  add custom domain for site
  * `firewall `    setup firewall and block all ports except 22, 80 and 443
  * `ssh-port `    change the default ssh connection port
  * `requirements `Update Python and Node packages
    * `--node ` Update only Node packages
    * `--python ` Update only Python packages
* `bench set-nginx-port [sitename] [port]` - Set site's port in Production


### Development

* `bench new-app [app-name]` Creates a new app
* `bench get-app [repo-link]` - Downloads an app from a git repository and installs it
  * `--branch [branch-name]`    Fetches specific branch of app
* `bench install-app [app-name]` Installs existing app
* `bench remove-from-installed-apps [app-name]` Remove app from the list of apps
* `bench uninstall-app [app-name]` Delete app and everything linked to the app (Bench needs to be running)
* `bench remove-app [app-name]` Remove app from the bench entirely
* `bench --site [sitename] --force reinstall ` Reinstall with fresh database (Caution: Will wipe out old database)
* `bench new-site [sitename]` - Creates a new site
  * `--db-name`                Database name
  * `--mariadb-root-username`  Root username for MariaDB
  * `--mariadb-root-password`  Root password for MariaDB
  * `--admin-password`         Administrator password for new site
  * `--verbose`                     Verbose
  * `--force`                       Force restore if site/database already exists
  * `--source_sql`             Initiate database with a SQL file
  * `--install-app`            Install app after installation`
* `bench use [site]` Sets a default site
* `bench drop-site` Removes site from disk and database completely
  * `--root-login`
  * `--root-password`
* `bench set-config [key] [value]`   Adds a key-value pair to site's config file
* `bench console`   Opens a IPython console in the bench venv
* `bench execute`   Execute a method inside any app.
  * Eg : `bench execute frappe.utils.scheduler.enqueue_scheduler_events`
* `bench --site [sitename] mariadb`  Opens SQL Console
* `bench --site [sitename] export-fixtures`  Exports fixtures
* `bench run-tests`  Run tests
  * `--app` App Name
  * `--doctype` DocType to run tests for
  * `--test` Specific Test
  * `--module` Run a particular module that has tests
  * `--profile` Runs a Python profiler on the test
* `bench disable-production`  Disables production environment


### Scheduler

* `bench enable-scheduler` - Enables Scheduler that will run scheduled tasks
* `bench doctor` - Get diagnostic info about background workers
* `bench show-pending-jobs`- Get pending jobs
* `bench purge-jobs` - Destroy all pending jobs
