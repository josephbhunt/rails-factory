# rails-factory
Build new Rails apps in a Docker container without having Rails or Ruby installed on the host machine.

# Purpose
In order to create a new Rails app in a Docker container, the desired versions of Ruby and Rails must be installed on the host machine. The standard recommendation is to run `rails new` on the host machine and then build the Docker image, thus containerizing the app. This project aims to give the user the ability to build a new Rails app in a container, without ever installing or upgrading their version of Ruby on their host machine.

`rails-factory` is a simple script for creating a containerized Rails app without having Ruby installed on the host machine. This is meant to be a portable way to create Rails apps. The host machine does not need to have any application dependencies installed - only Bash and Docker, which are common on Unix-like systems.

# Installation
1. Download rails-factory and copy to a hidden directory in your user home directory. `/Users/YourUsername/.rails_factory/rails-factory` for OSX or `/home/YourUsername/.rails_factory/rails-factory` for Linux. 
2. Ensure that the directory is added to your path PATH. In .bashrc, .bash_profile, or .zshrc: `export PATH="$HOME/.rails_factory:$PATH"`

# Usage

### Examples:
```
$ rails-factory --build path/to/your/app/app_name
# Will build the Docker image and create a new Rails app in path/to/your/app/app_name
```

```
$ rails-factory --build -p "--devcontainer" path/to/your/app/app_name
# Will build the Docker image and create a new Rails app with the --devcontainer option.
```

```
$ rails-factory -b -V 3.3 -v 7.2 path/to/your/app/app_name
# Will build the Docker image and create a Rails app using Ruby version 3.3 and Rails version 7.2
```

### Options
| Option   | Description   |
|------------|------------|
| -b \| --build | Build the container used to run `rails new` |
| -V \| --ruby-version | Set the ruby version that will be installed in the Docker container |
| -v \| --rails-version | Set the Rails version to be installed in the Docker container |
| -p \| --rails-params | String list of params that will be passed to `rails new` |
| -h \| --help | Print this help text |

# Requirements
- OS: Linux or OSX
- Bash: 3.3 or greater
- Docker: 4.20 or greater