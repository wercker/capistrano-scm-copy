capistrano-scm-copy
===================

A copy strategy for Capistrano 3, which mimics the `:copy` scm of Capistrano 2.

This will make Capistrano tar the current directory, upload it to the server(s) and then extract it in the release directory.

Requirements
============

Machine running Capistrano:

- Capistrano 3
- tar

Servers:

- mktemp
- tar

Installation
============

First make sure you install the capistrano-scm-copy by adding it to your `Gemfile`:

    gem "capistrano-scm-copy"

Add to Capfile:

    require 'capistrano/copy'
    
Then switch the `:scm` option to `:copy` in `config/deploy.rb`:

    set :scm, :copy
    
Remove files and directories that you don't want to copy:

    set :exclude_dir, ['tmp', 'config/*.yml']
    
TODO
====

I'm new to programming for Capistrano and even Ruby in general. So any feedback is appreciated. 

License
=======

The MIT License (MIT)

Changelog
=========

0.5.0
-----

- Fix issue related to `tar_roles` (see wercker/capistrano-scm-copy#15)

0.4.0
-----

- Add support for `tar_roles` (see wercker/capistrano-scm-copy#8)

0.3.0
-----

- Fix issue when running on Mac OS X (see wercker/capistrano-scm-copy#9)
- Allow exclude directory to be an Array (see wercker/capistrano-scm-copy#9)

0.2.0
-----

- Add `exclude_dir`

0.1.0
-----

- Add `:include_dir`

0.0.2
-----

- Add `task :set_current_revision` 

0.0.1
-----

- Initial release
