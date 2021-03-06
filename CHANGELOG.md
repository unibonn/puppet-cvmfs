## 2020-08-13 - Release 7.3.0
- New `cvmfs_repositories` parameter to exactly specify `CVMFS_REPOSITORIES` in
  `default.local` as used by `cvmfs_config probe` for instance.

## 2020-08-11 - Release 7.2.0
- New `cvmfs_repository_tag` parameter to mount command.

## 2020-06-34 - Release 7.1.0
- New pararmeter `cvmfs_instrument_fuse` parameter.
- Enable cmvfs-fsck.timer so it starts on boot.
- Remove legacy limits module requirement.

## 2020-02-10 - Release 7.0.1
- Bugfix on CentOS 8 only. Files in `/etc/autofs.master.d/`
  must end in .autofs to be included.
## 2020-01-06 - Release 7.0.0
- remove SLC5 support
- Add CentOS 8 support
- fsck cron jobs are now a systemd timer on 8
- A file is placed in auto.master.d rather than editing auto.master
- New parameters `cvmfs_shared_cache` and `cvmfs_alien_cache`
- Docs - correct cvmfs mount hash example
- `cvmfs_yum_includepkgs` now accepts an array of packages. Setting it as a string
  of packages is deprecated.

## 2019-03-14 - Release 6.2.0
- Support cvmfs_http_proxy on a mount

## 2019-01-28 - Release 6.1.0
- Support EXTERNAL repository parameters

## 2018-12-03 - Release 6.0.1
- Rely on $PATH to find `nice` command in fsck cron.

## 2018-12-03 - Release 6.0.0
- New parameters `cvmfs_dns_min_ttl` and `cvmfs_dns_max_ttl`.
  Unit is in seconds, support added in `cvmfs-2.5.2`
- New parameter `cvmfs_yum_priority` to set yum repo priority.
  The default is the existing value so no change.
- Fixtures for Puppet6 support.
- All the deprecated explicit hiera calls that were issuing
  notify calls for the last year have been completely removed.
- Puppet 4 types have now been added and much stronger
  type checking of input is now done. e.g while a 
  `cvmfs_quota_limit` of `'1234'` or `1234` used to be permitted only
  the latter is now permitted.

## 2018-06-28 - Release 5.2.0
- New stratum one configuration `mime_expire` defaulting 61 seconds.

## 2018-06-28 - Release 5.1.0
- `cvmfs_force_singing` parameter removed. Not used by cvmfs for years.
- The selinux context for the cache is now correctly set to `cvmfs_cache_t`
- The tmpclean of quarantine directory only runs if quarantine directory exists.
- Fix paths to awk, nice.
- Support debian based distributions for the first time.


## 2018-01-24 - Release 5.0.0
- Deprecates the following explicit hiera variables:

  `cvmfs_quota_limit`, `cvmfs_quota_ratio`, `cvmfs_http_proxy`, `cvmfs_server_url`, `cvmfs_cache_base`,
  `cvmfs_timeout`, `cvmfs_timeout_direct`, `cvmfs_nfiles`, `cvmfs_public_key`, `cvmfs_force_signing`,
  `cvmfs_syslog_level`, `cvmfs_tracefile`, `cvmfs_debuglog`, `cvmfs_max_ttl`, `cvmfs::mount`,
  `cvmfs_yum`, `cvmfs_yum_testing`, `cvmfs_yum_testing_enabled`, `cvmfs_kernel_version`, `cvmfs_yum_kernel`,
  `cvmfs_yum_kernel_enabled`, `cvmfs_sync_minute`.

  In almost every case the existing conventional class parameter can be used instead. 
  e.g `cvmfs_quota_limit` becomes `cvmfs::cvmfs_quota_limit`. The class parameter
  can be specified via hiera if so wished.
  These parameters have been available, documented and advised for sometime.

  Any use of the above explicit hiera lookups will work for now but a `notify` will be issued offering
  advice on what action to take.

  The next version `puppet-cvmfs` will completely drop thier support as well as support for puppet3.

## 2017-05-18 - Release 4.2.0
- New paramter `mime_expire` to `cvmfs::zero` to specify 
  expirey headers for cvmfs files in apache. Defaults 
  to `120`. Unit is seconds.
- New optional parameter `cvmfs_claim_ownership` to main class
  and to mount type.
- Bugfixes for latest concat modules.


## 2017-04-04 - Release 4.1.0
- New parameter `cvmfs_memcache_size` to main class and 
  to mount type.

## 2017-02-15 - Release 4.0.0
- cvmfs::server is now deprecated and will be removed 
  at next release. README.md contains details
  for migating to cvmfs::zero defined type.

## 2017-02-08 - Release 3.2.0
- Updates for cvmfs_server version 2.3

## 2016-09-14 - Release 3.1.0
- Wrap autofs service with ensure_resource to make co-existing
  easier.

## 2016-08-18 - Release 3.0.1
- Bug fix fact for ruby 1.8

## 2016-08-18 - Release 3.0.0

- DEPRCATION: Variable `cvmfs::config_automounter` is now deprecated.
  If it is set to the non default `false` compilation will fail.
- New variable `cvmfs::mount_method` is a string defaulting
  to `autofs` and provides the current default behaviour to use
  automounter configuration. It can also be set to `mount`
  in which will use the puppet mount type which currently
  mounts and adds an `/etc/fstab` entry.
  It can also be set to `none` in which case no mount
  configuration will be applied.
- Fixes #56 tmpwatch is now installed if fsck crons are
  enabled.

## 2016-04-29 - Release 2.0.0

- Remove all support for cvmfs 2.0.
- Only one rather than two puppet runs are now
  requied.
- Drop bundled augeas automaster lens. 
- Stratum 1 apache file update for cvmfs 2.2.


## 2016-03-07 - Release 1.0.3

- Stratum 1 cron jobs more frequent.

## 2016-03-07 - Release 1.0.2

- Puppetforge publish problem

## 2016-03-04 - Release 1.0.0

- New parameter `cvmfs::cvmfs_yum_manage_repo` defaults to true
  allows all yum managment to be disabled. Baptiste Grenier
- Package installations now wrapped in ensure_package to
  ease duplicate declarations
  Pat Riehecky
- Stratum 0 only, new parameter `cvmfs::zero::creator_version` defaults
  to `2.1.19`.
- Stratum 0 only, new json mime types to support cvmfs 2.2.
- Stratum 0 only, rdonly directory no longer mounted at boot time.
- Stratum 0 only, backwards incompatible change, the gid and group
  name now *MUST* be specified.
- Fixes for puppet 4 support.


## 2015-08-04 - Release 0.9.0

- A tmpwatch -f 30d now runs as weekly cron withing
  cvmfs::fsck to purge quarentined files.

## 2015-07-07 - Release 0.8.0

## Features
- Tests now check default configuration do not change.
- CVMFS_FOLLOW_REDIRECTS can now be set globally, per repo or per domain.
- New onreboot paramter to fsck module runs an fsck on reboot. Default false.
- zfs kernel module built for aufs kernel may now be installed on stratum0s.

## 2015-06-22 - Release 0.7.0
## Features
- New option defaults cvmfs::fsck::options allows
  an option, e.g. -p to parsed to cvmfs_fsck cron.

## Bugfixes
- Reintroduce $::concat_basedir in tests since
  puppetlabs-concat was reverted to version 1.

## 2015-06-10 - Release 0.6.0
## Features
- Garbage collection parameters for stratum 0.
- CVMFS_IGNORE_XDIR_HARDLINKS can be set on stratum 0.

##2015-05-06 - Release 0.5.0
## Deprecations
- All the hiera variables explicity called from params.pp
  file are now deprecated. These variables include.
  `cvmfs_config_automaster`, `cvmfs_quota_limit`, 
  `cvmfs_quota_limit`, `cvmfs_quota_ratio`, `cvmfs_http_proxy`,
  `cvmfs_server_url`, `cvmfs_cache_base`, `cvmfs_timeout`,
  `cvmfs_nfiles`, `cvmfs_public_key`, `cvmfs_force_signing`,
  `cvmfs_syslog_level`, `cvmfs_tracefile`, `cvmfs_debuglog`
  `cvmfs_max_ttl`, `cvmfs::mount`, `cvmfsversion`, 
  `cvmfs_yum`, `cvmfs_yum_testing`, `cvmfs_yum_proxy`
  `cvmfs_kernel_version`, `cvmfs_yum_kernel`, `cvmfs_yum_kernel_enabled`
  Instead use the hiera binding that maps to one of the paramters
  of the `cvmfs` class, e.g `cvmfs_quota_limit` becomes `cvmfs::cvmfs_quota_limit`
  A future version of this module will print a warning if these
  variables are still being used.


## Features
- Beaker acceptence tests now added for client. Configures
  a client and mounts the cms.cern.ch and atlas.cern.ch
  repositories. 
- The fact ::operatingsystemmajrelease is used everywhere now
  to determine major OS version.
- Unit tests for yumrepos.
- The GPG key location for packages in the cvmfs yum repositories
  can now be specified. 
- The GPG check of packages can be disabled in the yum repository 
  configuration.
- The new cvmfs-config repository is now configured but is disabled
  by default.


## Bugfixes
- The examples in the README now work.

## 2015-04-30 - Release 0.4.4
### Bugfixes
- Correct erwbgy-limits version dependency.

##2015-04-30 - Release 0.4.3
### Bugfixes
- Fix github to puppetforge publishing.

## 2015-04-30 - Release 0.4.2
### Bugfixes
- Fix github to puppetforge publishing.

## 2015-04-29 - Release 0.4.1
### Bugfixes
- Fix github to puppetforge publishing.

## 2015-04-29 - Release 0.4.0

### Features
- New paramter `cvmfs_repo_list` allows entries of CVMFS_REPOSITORIES to be fine
  tuned per cvmfs::mount. https://github.com/cvmfs/puppet-cvmfs/pull/22
- New paramter `manage_autofs_service` controls if autofs service should
  be managed module. Existing paramter `config_automaster` now only configures
  `auto.master file` - @jcpunk.
- New type cvmfs::zero to configure a CvmFS stratum 0. The existing
  class cvmfs::server for stratum 0s will be deprecated at some 
  future date.
- Doc changes for latest PL style guide. CHANGELOG is now markdown.
  Docs for classes and types being migrated from them to README.md.
- puppet-cvmfs is now autodeployed to puppetforge once tagged.
- CvmFS env settings can now be set globally as well per domain or mount.
- New variable `cvmfs_domain_hash` allows a hash of CvmFS domains to 
  loaded from hiera.
- New variable `cvmfs_use_geoapi` can be set globally, per domain or
  mount to influence `CVMFS_USE_GEOAPI`
- rspec functional tests now exist for class cvmfs and types 
  cvmfs::zero, cvmfs::mount and cvmfs::domain.


### Bugfixes
- cvmfs-config* packages can now be installed on cvmfs servers.
- All references to deprecated concat::setup removed - @berghaus.
- Vague use of undef was failing under furture parser or puppet
  4.0

## 2015-03-06 - Release 0.3.3

### Features
- do not control autofs service when asked not to.
- Install mod_wsgi and configure for geoip on stratum 1.
- Allow a http proxy for yum repos to be configured.
- Migrate to puppetlabs lint tests.

### Bugfixes

## 2014-06-18 - Release 0.3.2

### Features
- server - seperate yum configuration for server and client.
- server - Add `nofiles` paramter to server class to allow no open files to 
  be specified for the user running the cvmfs server.
- server - An exact kernel version is no longer specified.
- README file converted to markdown, now README.md.
- client - new defined type cvmfs::domain to create <domain>.local file in 
  /etc/cvmfs/domain.d.
- client - cvmfs::init class is now paramatised so supports that in addition to hiera.

### Bugfixes
- server - force a public key file location to be specified.
- server - when disabling selinux on server specify an augeas scope

## 2014-03-27 - Release 0.2.2

### Features

### Bugfixes
- bugfix for cvmfs_public_key variable.

## 2014-01-16 - Release 0.2.1

### Features

### Bugfixes
-  Puppet 3.4 compatability for ensure_resources.
