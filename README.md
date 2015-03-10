# jenkins-ansible-launch
This is a simple collection of scripts for launching ansible from jenkins


# No need for the Multiple SCM plugin
On default Jenkins only checks out SCM once..
You can then call this collection of script and:
- load a predefined SSH key from $JENKINS_HOME/.ssh
- use the git-ssh script to clone the actual ansible tasks
- do "stuff"

# no need to use the ssh-agent plugin
This script loads the key you specify

# Installation

There are a few files here... They should all reside in $JENKINS_HOME/.ssh

- ```git-ssh```
- ```id_rsa_```_**your_passphrase-less-key**
- ```ansible-time``` the bash script

## add a new script at the end of a job

![Jenkins add script](https://raw.githubusercontent.com/starkers/jenkins-ansible-launch/master/img/Selection_131.png "Add a script")


It should contain something like this:

```
export PKEY="$JENKINS_HOME/.ssh/id_rsa_deploy"          # SSH key to be used for git+ansible
export REPO="git@github.com:user/ansible-deploy.git"    # your repo of ansible tasks
export BRANCH="master"                                  # The branch
export TASKS="main.yml something.yml"                   # space seperated list of playbooks to be executed
export ARGS="--check"                                   # any flags you'd like to throw at "ansible-playbook"  (EG: -vv)

bash ~/.ssh/ansible-time
```

## a dedicted repo for ansible tasks/roles
Create an ansible repo containing stuff you'd like to do
See the /example directory for what this should contain

