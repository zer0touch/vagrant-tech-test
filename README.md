![Vagrant Logo](assets/Vagrant.png)]
# Vagrant Tech Test 
The following repo has been setup for a vagrant tech test.

## Requirements
- virtualbox (because its free)
- vagrant > 1.7.0
- ansible = 2.5.0
- python => 2.7.10
- terminal emulator (this will be your standard mac/linux or windows terminal emulator)
- 4GB+ ram (Sonar struggled to come up with anything less than 2GB as the elasticsearch can take a fair chunck of the memory)
- vagrant hostmanager plugin

> This has not been tested on windows hosts or guests other than ubuntu/debian

## Please refer to the video below on how to install vagrant 
[![Watch the video](assets/video.jpg)](https://youtu.be/PlObCAS_E_E)

## Resources
- image: https://app.vagrantup.com/bento/boxes/ubuntu-16.04
- ansible docker role: https://github.com/geerlingguy/ansible-role-docker

## How to use this repo
### Bring up the environment
1. Clone this repo
2. Once you have the relevant dependencies installed vagrant/virtualbox you need to install the vagrant hostmanager plugin
   ```vagrant plugin install vagrant-hostmanager```
3. Navigate to the appropriate directory
   ```vagrant up```
   
   Please note this may take some time to deploy so please be patient. 

### Updating 
1. Navigate to the appropriate directory
   ```vagrant provision```

### Tearing it down
1. Navigate to the appropriate directory
   ```vagrant destroy```

> The below is a screencast of the vagrant up command.
[![demo](https://asciinema.org/a/igxL4H6POcNEz8vh02FNa8vWR.png)](https://asciinema.org/a/igxL4H6POcNEz8vh02FNa8vWR?autoplay=1)

## Useful Urls
Some convenience port forwards have been added

Service       | URL                   | User/Pass    |
------------- | --------------------- |------------- |
Jenkins       | http://localhost:8081 | admin:admin  |
Sonar         | http://localhost:9001 | admin:admin  |
Selenoid ui   | http://localhost:8083 | none         |
Hello World   | http://localhost:8082 | none         |

## Issues
- adding clear text passwords to your source is undersireable.  This has been done for convenience's sake.   



