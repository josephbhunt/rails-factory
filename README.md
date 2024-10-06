# rails-factory
Build new Rails apps in a Docker container without having Rails or Ruby installed on the host machine.

# Purpose
In order to create a new Rails app in a Docker container, the desired versions of Ruby and Rails must be installed on the host machine. The standard recommendation is to run `rails new` on the host machine and then build the Docker image, thus containerizing the app. This project aims to give the user the ability to build a new Rails app in a container, without ever installing or upgrading their version of Ruby on their host machine.

`rails-factory` is a simple script for creating a containerized Rails app without having Ruby installed on the host machine. This is meant to be a portable way to create Rails apps. The host machine does not need to have any application dependencies installed - only Bash and Docker, which are common on Unix-like systems.

# Installation

### Install script
Copy and paste this to your terminal and press enter. It will download rails-factory, copy it to `$HOME/bin/`, and add it to your `$PATH` via your `.bashrc` or `.zshrc`. If you don't have either of those files on your system, then you will 

```
mkdir -p $HOME/bin && curl -L -o $HOME/bin/rails-factory https://raw.githubusercontent.com/josephbhunt/rails-factory/main/rails-factory && chmod +x $HOME/bin/rails-factory && { ! echo $PATH | grep -q "$HOME/bin" && { [ -f ~/.zshrc ] && echo 'export PATH=$PATH:$HOME/bin' >> ~/.zshrc && source ~/.zshrc; } || { [ -f ~/.bashrc ] && echo 'export PATH=$PATH:$HOME/bin' >> ~/.bashrc && source ~/.bashrc; }; } 
```

### Manual Install
1. Download rails-factory and copy to a hidden directory in your user home directory. `/Users/YourUsername/bin/rails-factory` for OSX or `/home/YourUsername/bin/rails-factory` for Linux. 
2. Ensure that the directory is added to your path PATH. In .bashrc, .bash_profile, or .zshrc: `export PATH="$PATH:$HOME/bin"`

# Usage

### Examples:
```
$ rails-factory path/to/your/app/app_name
# Build the Docker image and create a new Rails app in path/to/your/app/app_name
```

```
$ rails-factory path/to/your/app/app_name -- --devcontainer --skip-action-mailer
# Build the Docker image and create a new Rails app with the --devcontainer and --skip-action-mailer options
```

```
$ rails-factory -V 3.3 -v 7.2 path/to/your/app/app_name
# Build the Docker image and create a Rails app using Ruby version 3.3 and Rails version 7.2
```

```
$ rails-factory -s -V 3.3 -v 7.2 path/to/your/app/app_name
# Skip building the Docker image and create a Rails app using Ruby version 3.3 and Rails version 7.2
# Assumes the Docker image for Ruby version 3.3 and Rails version 7.2 exists, otherwise returns an error
```

#### Use your own Rails gem build
You mush first build the Rails gem on the host machine.
The name of the gem file must be `rails.gem`.
```
$ rails-factory -g path/to/rails.gem path/to/your/app/app_name
# Builds an image and installs the Rails gem from the given host machine path
# Then runs `rails new` and creates a Rails app in path/to/your/app/app_name
```

### Options
| Option   | Description   |
|------------|------------|
| -g \| --rails-gem-path | Path to the a Rails gem file on the host machine |
| -h \| --help | Print this help text |
| -s \| --skip-build | Skip building the Docker image used to run `rails new` |
| -V \| --ruby-version | Set the ruby version that will be installed in the Docker container |
| -v \| --rails-version | Set the Rails version to be installed in the Docker container |

### Arguments
| Argument | Description |
|----------|-------------|
| path/to/new/rails/app | The path where the new Rails app will be installed on the host machine |
| -- | End of options. All following arguments will be passed to rails new |

# Requirements
- OS: Linux or OSX
- Bash: 3.3 or greater
- Docker: 4.20 or greater