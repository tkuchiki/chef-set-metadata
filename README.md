chef-set-metadata
============

Append "depends" and "name" to a metadata.rb

## Example

### depends

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
$ ./chef-set-metadata --cookbook ./cookbook -d
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

### name

~~~~
$ tree cookbooks/
cookbooks/
├── mysql
└── nginx
    └── metadata.rb

2 directories, 1 file
~~~~

~~~~
$ cat ./cookbooks/nginx/metadata.rb
maintainer       'YOUR_COMPANY_NAME'
maintainer_email 'YOUR_EMAIL'
license          'All rights reserved'
description      'Installs/Configures s3cmd'

version          '0.1.0'
~~~~

~~~~
$ ./chef-set-metadata --cookbook ./cookbook -n
** Creating metadata for cookbook: mysql
Added name 'nginx' in cookbooks//nginx/metadata.rb
~~~~

~~~~
$ cat cookbooks/nginx/metadata.rb
maintainer       'YOUR_COMPANY_NAME'
maintainer_email 'YOUR_EMAIL'
license          'All rights reserved'
description      'Installs/Configures nginx'

version          '0.1.0'
name             'nginx'

$ cat cookbooks/mysql/metadata.rb
name             'mysql'
maintainer       'YOUR_COMPANY_NAME'
maintainer_email 'YOUR_EMAIL'
license          'All rights reserved'
description      'Installs/Configures mysql'

version          '0.1.0'
~~~~

## Usage

~~~~
$ ./chef-set-metadata -h
Usage: chef-set-metadata [options]
    -c, --config FILE_PATH           The configuration file to use
        --cookbook COOKBOOK_DIR      Path to cookbook
        --copyright [COPYRIGHT]      Copyright (default YOUR_COMPANY_NAME)
    -e, --email [MAIL]               Email (default YOUR_EMAIL)
    -l, --license [LICENSE]          License (default none)
    -r, --readme-format [FORMAT]     README format (default .md)
    -d, --set-depends                Set depends
    -n, --set-name                   Set name
    -v, --version                    Show version
~~~~

