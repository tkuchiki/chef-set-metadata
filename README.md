chef-depends
============

Append "depends" to a metadata.rb

## Example

~~~~
$ tree ./cookbooks
./cookbooks
├── mysql
│   └── attributes
│       └── default.rb
└── nginx
    └── recipes
        └── default.rb
~~~~

~~~~
$ cat ./cookbooks/nginx/recipes/default.rb
include_recipe "foobar"

$ cat ./cookbooks/mysql/attributes/default.rb
include_attribute "hoge"
~~~~

~~~~
$ ./chef-depends --cookbook ./cookbook
** Creating metadata for cookbook: mysql
Added depends hoge in ./cookbooks/mysql/metadata.rb
** Creating metadata for cookbook: nginx
Added depends foobar in ./cookbooks/nginx/metadata.rb
~~~~

~~~~
$ tree ./cookbooks
./cookbooks
├── mysql
│   ├── attributes
│   │   └── default.rb
│   └── metadata.rb
└── nginx
    ├── metadata.rb
    └── recipes
        └── default.rb
~~~~

~~~~
$ cat cookbooks/nginx/metadata.rb
name             'nginx'
maintainer       'YOUR_COMPANY_NAME'
maintainer_email 'YOUR_EMAIL'
license          'All rights reserved'
description      'Installs/Configures nginx'

version          '0.1.0'
depends          'foobar'

$ cat cookbooks/mysql/metadata.rb
name             'mysql'
maintainer       'YOUR_COMPANY_NAME'
maintainer_email 'YOUR_EMAIL'
license          'All rights reserved'
description      'Installs/Configures mysql'

version          '0.1.0'
depends          'hoge'
~~~~

## Usage

~~~~
$ ./chef-depends -h
Usage: chef-depends [options]
    -c, --config FILE_PATH           The configuration file to use
        --cookbook COOKBOO_DIR       Path to cookbook
        --copyright [COPYRIGHT]      Copyright (default YOUR_COMPANY_NAME)
    -e, --email [MAIL]               Email (default YOUR_EMAIL)
    -l, --license [LICENSE]          License (default none)
    -r, --readme-format [FORMAT]     README format (default .md)
    -v, --version                    Show version
~~~~
