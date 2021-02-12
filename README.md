Drupal Developer
================

This cookbook adds developer friendly tools for the drupal-lamp project.

Requirements
------------

This cookbook is designed to work with drupal-lamp https://github.com/newmediadenver/drupal-lamp

### Platform:

Ubuntu

### Cookbooks:

php

Attributes
----------
````
"vampd_developer" {
  "xdebug": false,
  "phpmyadmin": false
}
````

Recipes
-------
#### vampd-developer::xdebug

Adds and configures xdebug php extension

#### vampd-developer::phpmyadmin

Adds phpmyadmin

#### vampd-developer::copy

Copies files from a src to a destination
```
"vampd_developer": {
    "copy": {
        "/vagrant/.gitconfig": ["/root/.gitconfig", "/home/vagrant/.gitconfig"]
    }
}
```

#### vampd-developer:user_groups

Puts users in groups.
```
"vampd_developer": {
    "user_groups": {
        "group": [users]
    }
}
```

#### vampd-developer::zsh
Adds zsh for the root user.
```
"vampd_developer": {
    "zsh": true
}
```


Usage
-----
To get it working with drupal-lamp:
* Open Berksfile in your drupal-lamp directory and place the following line in there
````
cookbook "drupal-developer", git: "https://github.com/arknoll/drupal-developer", branch: "master"
````
* Open chef/roles/drupal_lamp.rb in your drupal-lamp directory and add "recipe[drupal-developer]", to the end of env_run_lists run list array

* Add and configure the attributes above to your drupal_lamp.json file.

* run either 'vagrant up' or 'vagrant provision'

#### phpmyadmin
When phpmyadmin is set to true, phpmyadmin will be installed on your server. To access phpmyadmin go to your site's url/phpmyadmin. You will be able to login to phpmyadmin with the username and password found in chef/data_bags/users/mysql.json

Testing
-------

[![Build Status](https://travis-ci.org/arknoll/drupal-developer.png?branch=master)](https://travis-ci.org/arknoll/drupal-developer)

The cookbook provides the following Rake tasks for testing:

    rake foodcritic                   # Lint Chef cookbooks
    rake integration                  # Alias for kitchen:all
    rake kitchen:all                  # Run all test instances
    rake kitchen:default-centos-64    # Run default-centos-64 test instance
    rake kitchen:default-ubuntu-1204  # Run default-ubuntu-1204 test instance
    rake rubocop                      # Run RuboCop style and lint checks
    rake spec                         # Run ChefSpec examples
    rake test                         # Run all tests

License and Author
------------------

Author:: Alex Knoll (arknoll@gmail.com)

Copyright:: 2014, Alex Knoll

Licensed under the Apache License, Version 2.0 (the "License");
you may not use this file except in compliance with the License.
You may obtain a copy of the License at

    http://www.apache.org/licenses/LICENSE-2.0

Unless required by applicable law or agreed to in writing, software
distributed under the License is distributed on an "AS IS" BASIS,
WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
See the License for the specific language governing permissions and
limitations under the License.

Contributing
------------

We welcome contributed improvements and bug fixes via the usual workflow:

1. Fork this repository
2. Create your feature branch (`git checkout -b my-new-feature`)
3. Commit your changes (`git commit -am 'Add some feature'`)
4. Push to the branch (`git push origin my-new-feature`)
5. Create a new pull request
