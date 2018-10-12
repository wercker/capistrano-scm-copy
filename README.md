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

    
Configuration
=============

Since this tool involve tar to create a depolyable archive. A bit of tar understanding is required.

`set :include_dir`
------------------
    
The directories you wich to archive. Path is relative to capistrano root project.
Default to '*'

This is passed as file list (last argument) to tar, see man tar

`set :exclude_dir`
------------------

Directories you want to exclude from you archive.
Those are added to tar command line as --exclude arguments.

`set :build_dir`
----------------

The root directory of the archive. This use the `-C` tar option to set archive's root dir.
It default to current directory.
eg: 

Let say you want to deploy redmine with a bunch of plugins.
You will need to fetch redmine source, plugins, and place custom config files.
For this you have a build script that place the assembled redmine within a subdirectory like CAP_ROOT/build_out

Then you'll need capistrano to deploy the content of build directory, not the whole current root directory.

To achieve this you'll apply this setup

```ruby
set :include_dir, 'build_out/*'  # we want all within build_out
set :exclude_dir, { %w(vendor tmp log).map {|f| File.join(f,'*')} } # except content of vendor log and tmp
set :build_dir, { 'build_out' } # we want to use build_out as archive root
```

this way files like
 ./build_out/Gemfile
 ./build_out/app
 ...

Will be archive and deployed as
  ./Gemfile
  ./app


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
