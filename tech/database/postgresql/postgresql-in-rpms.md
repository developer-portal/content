---
title: PostgreSQL in RPMs
subsection: postgresql
order: 1
---

# Raw 'README.rpm-dist' text file generated for Fedora 22

```
|                                   PostgreSQL in RPMs
|    
|       --------------------------------------------------------------------------
|    
|    INTRODUCTION
|    
|       This document exists to explain the layout of the RPMs for PostgreSQL, to
|       describe various RPM specifics, and to document special features found in
|       the RPMset.
|    
|       This document is written to be applicable to version 9.4 of PostgreSQL,
|       which is the current version of the RPMs as of this writing. More to the
|       point, versions prior to 9.4 are not documented here.
|    
|       This document is intended for use only with the RPMs supplied in Red Hat
|       Enterprise Linux, CentOS and Fedora. Note that there are also "PGDG" RPMs
|       available directly from the upstream PostgreSQL project. Those are
|       slightly different.
|    
|       --------------------------------------------------------------------------
|    
|    QUICKSTART
|    
|       For a fresh installation, you will need to initialize the cluster first
|       (as a postgres user):
|    
|             $ postgresql-setup --initdb
|    
|       and it will prepare a new database cluster for you. Then you will need to
|       start PostgreSQL. Now, as 'root', run:
|    
|             $ systemctl start postgresql.service
|    
|       This command will start a postmaster that will listen on localhost and
|       Unix socket 5432 only. Edit /var/lib/pgsql/data/postgresql.conf and
|       pg_hba.conf if you want to allow remote access -- see the section on Grand
|       Unified Configuration. You will probably also want to do
|    
|             $ systemctl enable postgresql.service
|    
|       so that the postmaster is automatically started during future reboots.
|    
|       The file /var/lib/pgsql/.bash_profile is packaged to help with the setting
|       of environment variables. You may edit this file, and it won't be
|       overwritten during an upgrade. However, enhancements and bugfixes may be
|       added to this file, so be sure to check .bash_profile.rpmnew after
|       upgrading.
|    
|       The user 'postgres' is created during installation of the server
|       subpackage. This user by default is UID and GID 26. The user has the
|       default shell set to bash, and the home directory set to /var/lib/pgsql.
|       This user also has no default password, so the only way to become this
|       user is to su to it from root. If you want to be able to su to it from a
|       non-root account or log in directly as 'postgres' you will need to set a
|       password using passwd. Test section 2.
|    
|       --------------------------------------------------------------------------
|    
|    UPGRADING AN INSTALLATION
|    
|       For a minor-version upgrade (such as 9.3.1 to 9.3.4; last number changes),
|       just install the new RPMs; there's usually nothing more to it than that.
|       Upgrading across a major release of PostgreSQL (for example, from 9.2.x to
|       9.3.x) requires more effort.
|    
|       If you are upgrading across more than one major release of PostgreSQL (for
|       example, from 8.3.x to 9.0.x), you will need to follow the "traditional"
|       dump and reload process to bring your data into the new version. That is:
|       *before* upgrading, run pg_dumpall to extract all your data into a SQL
|       file. Shut down the old postmaster, upgrade to the new version RPMs,
|       perform initdb, and run the dump file through psql to restore your data.
|    
|       In some major releases, the RPMs also support faster upgrade from concrete
|       subset of previous releases. You can run the:
|    
|             $ postgresql --upgrade-ids
|    
|       to see what previous versions you are able to upgrade from. This is much
|       faster than a dump and reload. To do a faster upgrade:
|    
|        1. shut down the old postmaster running against old data
|    
|        2. optionally make a backup of data directory (recommended!)
|    
|        3. install the new version's RPMs (install all the ones you had before,
|           plus postgresql-upgrade)
|    
|        4. as root, run "postgresql-setup --upgrade [--upgrade-from ID]"
|    
|        5. update the configuration files /var/lib/pgsql/data/*.conf with any
|           customizations you had before (your old configuration files are in old
|           data directory or in /var/lib/pgsql/data-old/ if you've done in-place
|           upgrade)
|    
|        6. as root, run "systemctl start postgresql.service"
|    
|        7. the postgresql-upgrade package can be removed after the update is
|           complete, as can old data directory
|    
|       NOTE: The in-place upgrade process is new and relatively poorly tested, so
|       if your data is critical it's a really good idea to make a tarball backup
|       of old data directory before running the upgrade. This will let you get
|       back to where you were in case of disaster.
|    
|       --------------------------------------------------------------------------
|    
|    POSTGRESQL RPM PACKAGES AND RATIONALE
|    
|       PostgreSQL is split up into multiple packages so that users can 'pick and
|       choose' what pieces are needed, and what dependencies are required.
|    
|       Table 1. Sub-package list
|    
|       +------------------------------------------------------------------------+
|       |        Package        |                  Description                   |
|       |-----------------------+------------------------------------------------|
|       | postgresql:           | Key client programs and basic documentation    |
|       |-----------------------+------------------------------------------------|
|       | postgresql-libs:      | Client shared libraries                        |
|       |-----------------------+------------------------------------------------|
|       | postgresql-server:    | Server executables and data files              |
|       |-----------------------+------------------------------------------------|
|       | postgresql-test:      | The regression tests and associated files      |
|       |-----------------------+------------------------------------------------|
|       | postgresql-upgrade:   | Support files for upgrading from previous      |
|       |                       | major version                                  |
|       |-----------------------+------------------------------------------------|
|       | postgresql-docs:      | Full documentation in HTML and PDF, the        |
|       |                       | tutorial files                                 |
|       |-----------------------+------------------------------------------------|
|       | postgresql-contrib:   | Add-on loadable modules and programs           |
|       |-----------------------+------------------------------------------------|
|       | postgresql-plperl:    | PL/Perl procedural language                    |
|       |-----------------------+------------------------------------------------|
|       | postgresql-plpython:  | PL/Python procedural language (for Python 2)   |
|       |-----------------------+------------------------------------------------|
|       | postgresql-plpython3: | PL/Python procedural language (for Python 3)   |
|       |-----------------------+------------------------------------------------|
|       | postgresql-pltcl:     | PL/Tcl procedural language                     |
|       +------------------------------------------------------------------------+
|    
|       You have to install postgresql and postgresql-libs to do anything.
|       postgresql-server is needed unless you only plan to use the clients to
|       work with a remote PostgreSQL server. The others are optional.
|    
|       Note that there are no postgresql-perl, postgresql-jdbc, postgresql-odbc,
|       postgresql-python, postgresql-tcl, or postgresql-tk subpackages any
|       longer. Those programs have been split off into separate source
|       distributions. They are still available, but in some cases not under those
|       RPM names.
|    
|       --------------------------------------------------------------------------
|    
|    RPM FILE LOCATIONS
|    
|       To be in compliance with the Linux FHS, the PostgreSQL RPMs install files
|       in a manner not consistent with most of the PostgreSQL documentation.
|       According to the standard PostgreSQL documentation, PostgreSQL is
|       installed under the directory /usr/local/pgsql, with executables, source,
|       and data existing in various subdirectories.
|    
|       Different distributions have different ideas of some of these file
|       locations. In particular, the documentation directory can be /usr/doc,
|       /usr/doc/packages, /usr/share/doc, /usr/share/doc/packages, or some other
|       similar path.
|    
|       However, this installation (which usually matches the Red Hat / CentOS /
|       Fedora RPM's) install the files like:
|    
|       Table 2. Filesystem layout
|    
|       +------------------------------------------------------------------------+
|       |      Description      |                   Directory                    |
|       |-----------------------+------------------------------------------------|
|       | Executables           | /usr/bin                                       |
|       |-----------------------+------------------------------------------------|
|       | Libraries             | /usr/lib64                                     |
|       |-----------------------+------------------------------------------------|
|       | Documentation         | /usr/share/doc/postgresql/html                 |
|       |-----------------------+------------------------------------------------|
|       | PDF documentation     | /usr/share/doc/postgresql-docs                 |
|       |-----------------------+------------------------------------------------|
|       | Contrib documentation | /usr/share/doc/postgresql-contrib              |
|       |-----------------------+------------------------------------------------|
|       | Source                | not installed                                  |
|       |-----------------------+------------------------------------------------|
|       | Data                  | /var/lib/pgsql/data                            |
|       |-----------------------+------------------------------------------------|
|       | Backup area           | /var/lib/pgsql/backups                         |
|       |-----------------------+------------------------------------------------|
|       | Templates             | /usr/share/pgsql                               |
|       |-----------------------+------------------------------------------------|
|       | Procedural Languages  | /usr/lib64/pgsql                               |
|       |-----------------------+------------------------------------------------|
|       | Development Headers   | /usr/include/pgsql                             |
|       |-----------------------+------------------------------------------------|
|       | Other shared data     | /usr/share/pgsql                               |
|       |-----------------------+------------------------------------------------|
|       | Regression tests      | /usr/lib64/pgsql/test/regress (in the -test    |
|       |                       | package)                                       |
|       +------------------------------------------------------------------------+
|    
|       While it may seem gratuitous to place these files in different locations,
|       the FHS requires it -- distributions should not ever touch /usr/local. It
|       may also seem like more work to keep track of where everything is -- but,
|       that's the beauty of RPM -- you don't have to keep track of the files, RPM
|       does it for you.
|    
|       These RPMs are designed to be LSB-compliant -- if you find this not to be
|       the case, please let us know by way of the pgsql-pkg-yum@postgresql.org
|       mailing list.
|    
|       --------------------------------------------------------------------------
|    
|    MULTIPLE POSTMASTERS
|    
|       The postgresql-server package contains a systemd "unit" files
|       postgresql.service and postgresql@.service. The first file is used solely
|       to start the default PostgreSQL server. The second one is designed to
|       allow instantiating additional PostgreSQL servers on same machine.
|    
|       As an example, let us create a secondary PostgreSQL service called,
|       creatively enough, 'postgresql@secondary'. Here are the steps:
|    
|        1. Run the following command to create the necessary configuration and to
|           initialize the new database cluster
|    
|             $ postgresql-setup --initdb \
|                 --unit postgresql@secondary \
|                 --new-systemd-unit \
|                 --datadir /path/to/data/directory \
|                 --port NNNN
|    
|    
|           Replace the "/path/to/data/directory" path and NNNN port with
|           appropriate settings that don't conflict with any other PostgreSQL
|           setup. Make sure that the parent directory of specified path has
|           appropriate ownership and permissions. Note the SELinux issues
|           mentioned below.
|    
|        2. Edit postgresql.conf in the target 'datadir' directory to change
|           settings as needed.
|    
|        3. Start the new service with this command:
|    
|             $ systemctl start postgresql@secondary.service
|    
|           You will probably also want to run the command
|    
|             $ systemctl enable postgresql@secondary.service
|    
|           so that the new service is automatically started in future reboots.
|    
|       When doing a major-version upgrade of a secondary service, add the service
|       name to the postgresql-setup command, for example:
|    
|             $ postgresql-setup --upgrade --unit postgresql@secondary
|    
|       This will let postgresql-setup find the correct data directory from the
|       proper configuration file.
|    
|       If you are running SELinux in enforcing mode (which is highly recommended,
|       particularly for network-exposed services like PostgreSQL) you will need
|       to adjust SELinux policy to allow the secondary server to use non-default
|       PGPORT or PGDATA settings. To allow use of a non-default port, say 5433,
|       do this as root:
|    
|             $ semanage port -a -t postgresql_port_t -p tcp 5433
|    
|       To allow use of a non-default data directory, say /special/pgdata, do:
|    
|             $ semanage fcontext -a -t postgresql_db_t "/special/pgdata(/.*)?"
|    
|       If you already created the directory, follow that with:
|    
|             $ restorecon -R /special/pgdata
|    
|       These settings are persistent across reboots. For more information see
|       "man semanage".
|    
|       --------------------------------------------------------------------------
|    
|    REGRESSION TESTING
|    
|       If you install the postgresql-test RPM then you can run the PostgreSQL
|       regression tests. These tests stress your database installation and
|       produce results that give you assurances that the installation is
|       complete, and that your database machine is up to the task.
|    
|       To run the regression tests under the RPM installation, make sure that the
|       PostgreSQL server has been started (if not, su to root and do
|    
|             $ systemctl start postgresql.service
|    
|       su to postgres, cd to /usr/lib64/pgsql/test/regress and execute "make
|       check". This command will start the regression tests and will both show
|       the results to the screen and store the results in the file regress.out.
|    
|       If any tests fail, see the file regression.diffs in that directory for
|       details, and read the "Regression Tests" section of the PostgreSQL
|       documentation to find out whether the differences are actually
|       significant. If you need help interpreting the results, contact the
|       pgsql-general list at postgresql.org.
|    
|       After testing, run "make clean" to remove the files generated by the test
|       script. Then you can remove the postgresql-test RPM, if you wish.
|    
|       --------------------------------------------------------------------------
|    
|    STARTING POSTMASTER AUTOMATICALLY AT SYSTEM STARTUP
|    
|       Fedora / Red Hat / CentOS use the systemd package to manage server
|       startup. A systemd unit file for PostgreSQL is provided in the server
|       package, as /usr/lib/systemd/system/postgresql.service. To start the
|       postmaster manually, as root run
|    
|             $ systemctl start postgresql.service
|    
|       To shut the postmaster down,
|    
|             $ systemctl stop postgresql.service
|    
|       These two commands only change the postmaster's current status. If you
|       want the postmaster to be started automatically during future system
|       startups, run
|    
|             $ systemctl enable postgresql.service
|    
|       To undo that again,
|    
|             $ systemctl disable postgresql.service
|    
|       See "man systemctl" for other possible subcommands.)
|    
|       --------------------------------------------------------------------------
|    
|    GRAND UNIFIED CONFIGURATION (GUC) FILE
|    
|       The PostgreSQL server has many tunable parameters -- the file
|       /var/lib/pgsql/data/postgresql.conf is the master configuration file for
|       the whole system.
|    
|       The RPM ships with a mostly-default file -- you will need to tune the
|       parameters for your installation. In particular, you might want to allow
|       nonlocal TCP/IP socket connections -- in order to allow these, you will
|       need to edit the postgresql.conf file. The line in question contains the
|       string 'listen_addresses' -- you need to both uncomment the line and set
|       the value to '*' to get the postmaster to accept nonlocal connections.
|       You'll also need to adjust pg_hba.conf appropriately.
|    
|       --------------------------------------------------------------------------
|    
|    LOGGING SET UP
|    
|       By default, the postmaster's stderr log is directed into files placed in a
|       pg_log subdirectory of the data directory (ie,
|       /var/lib/pgsql/data/pg_log). The out-of-the-box configuration rotates
|       among seven files, one for each day of the week. You can adjust this by
|       changing postgresql.conf settings.
|    
|       --------------------------------------------------------------------------
|    
|    REBUILDING FROM SOURCE RPM
|    
|       If your distribution is not supported by the binary RPMs from
|       PostgreSQL.org, you will need to rebuild from the source RPM.
|    
|       If you have not previously rebuilt any RPMs, set up the required
|       environment: make a work directory, say ~/rpmwork, then cd into it and do
|    
|             $ mkdir BUILD BUILDROOT RPMS SOURCES SPECS SRPMS
|    
|       Then make a file ~/.rpmmacros containing
|    
|     %_topdir full_path_to_work_directory_here
|    
|       Download the postgresql .src.rpm for the release you want and place it in
|       the SRPMS subdirectory, then cd there and execute
|    
|             $ rpmbuild --rebuild postgresql-nnn.src.rpm
|    
|       The results will appear under the RPMS subdirectory.
|    
|       You will have to have a full development environment to rebuild the RPM
|       set. If rpmbuild complains of lack of certain packages, install them and
|       try again. In some cases, you can disable features to avoid needing some
|       development packages, as detailed next.
|    
|       This release of the RPMset includes the ability to conditionally build
|       sets of packages. The parameters, their defaults, and the meanings are:
|    
|       Table 3. SRPM configuration options
|    
|       +------------------------------------------------------------------------+
|       |  Variable    Default                      Comment                      |
|       | beta         0        build with cassert and do not strip the binaries |
|       | runselftest  1        do "make check" during the build                 |
|       | test         1        build the postgresql-test package                |
|       | upgrade      1        build the postgresql-upgrade package             |
|       | plpython     1        build the PL/Python procedural language package  |
|       | plpython3    1        build the PL/Python3 procedural language package |
|       | pltcl        1        build the PL/Tcl procedural language package     |
|       | plperl       1        build the PL/Perl procedural language package    |
|       | ssl          1        build with OpenSSL support                       |
|       | kerberos     1        build with Kerberos 5 support                    |
|       | ldap         1        build with LDAP support                          |
|       | nls          1        build with national language support             |
|       | pam          1        build with PAM support                           |
|       | sdt          1        build with SystemTap support                     |
|       | xml          1        build with XML support                           |
|       | pgfts        1        build with --enable-thread-safety                |
|       | selinux      1        build contrib/selinux                            |
|       | uuid         1        build contrib/uuid-ossp                          |
|       +------------------------------------------------------------------------+
|    
|       To use these defines, invoke a rebuild like this:
|    
|         $ rpmbuild --rebuild \
|               --define 'plpython 0' \
|               --define 'pltcl 0' \
|               --define 'test 0' \
|               --define 'runselftest 0' \
|               --define 'kerberos 0' \
|               postgresql-9.2.0-1.src.rpm
|    
|    
|       This command would disable the plpython, pltcl, and test subpackages,
|       disable the regression test run during build, and disable kerberos
|       support.
|    
|       You might need to disable runselftest if there is an installed version of
|       PostgreSQL that is a different major version from what you are trying to
|       build. The self test tends to pick up the installed libpq.so shared
|       library in place of the one being built :-(, so if that isn't compatible
|       the test will fail. Also, you can't use runselftest when doing the build
|       as root.
|    
|       More of these conditionals will be added in the future.
|    
|       --------------------------------------------------------------------------
|    
|    CONTRIB FILES
|    
|       The contents of the contrib tree are packaged into the -contrib subpackage
|       and are processed with make and make install. There is documentation in
|       /usr/share/doc/postgresql-contrib for these modules. Most of the modules
|       are in /usr/lib64/pgsql for loadable modules, and binaries are in
|       /usr/bin. In the future these files may be split out, depending upon
|       function and dependencies.
|    
|       --------------------------------------------------------------------------
|    
|    MORE INFORMATION
|    
|       You can get more information at http://www.postgresql.org and
|       http://yum.postgresql.org
|    
|       Please help make this packaging better -- let us know if you find
|       problems, or better ways of doing things. You can reach us by e-mail at
|       pgsql-pkg-yum@postgresql.org or fail a bug against postgresql component on
|       bugzilla.redhat.com.
```
