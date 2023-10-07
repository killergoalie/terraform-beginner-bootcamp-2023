# Terraform Beginner Bootcamp 2023

## Semantic Versioning :mage:

This project is going to utilize semantic versioning for its tagging.
[semver.org](https://semver.org/)

The general format:

**MAJOR.MINOR.PATCH**, eg. `1.0.1`

 - MAJOR version when you make incompatible API changes
 - MINOR version when you add functionality in a backward compatible manner
 - PATCH version when you make backward compatible bug fixes


## Install the Terraform CLI

### Considerations with the Terraform CLI changes
Terraform CLI installation instructions have changed due to gpg keyring changes. Updated to match current install instructions, also moved into external script in [./bin/install_terraform_cli](./bin/install_terraform_cli)


[Install Terraform CLI](https://developer.hashicorp.com/terraform/tutorials/aws-get-started/install-cli)

### Considerations for Linux Distros

This project is built on or with gitpod running in Ubuntu.  
How to check your linux version:
`cat /etc/os-release`:
```
PRETTY_NAME="Ubuntu 22.04.3 LTS"
NAME="Ubuntu"
VERSION_ID="22.04"
VERSION="22.04.3 LTS (Jammy Jellyfish)"
VERSION_CODENAME=jammy
ID=ubuntu
ID_LIKE=debian
HOME_URL="https://www.ubuntu.com/"
SUPPORT_URL="https://help.ubuntu.com/"
BUG_REPORT_URL="https://bugs.launchpad.net/ubuntu/"
PRIVACY_POLICY_URL="https://www.ubuntu.com/legal/terms-and-policies/privacy-policy"
UBUNTU_CODENAME=jammy
```
or `uname -a`
```
Linux username-terraformbe-9n03s51dybc 6.1.54-060154-generic #202309200834 SMP PREEMPT_DYNAMIC Wed Sep 20 09:14:42 UTC 2023 x86_64 x86_64 x86_64 GNU/Linux
```

### Refactoring into Bash Scripts

While fixing the deprecated issue, created a new bash script to handle install.  This allowed a line reduction for the gitpod yaml file, making it more readable.

New Script can be found at: [./bin/install_terraform_cli](./bin/install_terraform_cli)

#### Additional Resources  
- [Linux Scripting Shebang](https://en.wikipedia.org/wiki/Shebang_(Unix))
- [Linux Chmod](https://en.wikipedia.org/wiki/Chmod) 

## Execution Considerations

When executing the bash script we can use the `./` shorthand notiation to execute the bash script.

ie `./bin/install_terraform_cli`

If we are using a script in .gitpod.yml we need to point the script to a program to interpret it.

ie `source ./bin/install_terraform_cli`

#### Linux Permissions Considerations

In order to make our bashh scripts executable we need to change linux permissions for the file to be executable.  
`chmod 0744 ./bin/install_terraform_cli`

[Linux Chmod](https://en.wikipedia.org/wiki/Chmod)

### Gitpod Lifecycle (Before, Init, Command)

We need to be carefule with using Initg, as it won't rerun when restarting an existing workspace.

[Gitpod Lifecycle](https://www.gitpod.io/docs/configure/workspaces/workspace-lifecycle)

### Working w/ Env Vars

We can list out all Environment Variables (Env Vars) using the `env` command.

We can filter specific env vars using grep ie `env | grep -i AWS_`

#### Setting and Unsetting Env Vars

In the terminal we can set using `export HELLO='world'`

In the terminal we can unset using `unset HELLO`

We can set an env var temporarily, by just running a command:
```sh
HELLO='world' ./bin/print_message
```
Within a bash script we can set env without writing export ie
```sh
#!/usr/bin/env bash

HELLO='world'

echo $HELLO
```

#### Printing Vars

We can print an env var using `echo` ie 
`echo $HELLO`

#### Scoping of Env Vars

When you open up new bash terminals in VSCode it will not be aware of env vars that you have set in another window.

If you want to Env Var to persist across all future terminal, you need to set env var in your terminal profile/s.

#### Persisting Env Vars in Gitpod

We can persist env vars in gitpod by storing them in Gitpod Secrets Storage.

```
gp env HELLO='world'
```

All future workspaces launched will set the env vars for all bash terminals opened in those workspaces.

You can also set env vars in the `.gitpod.yml` bit this should only contain non-sensitive env vars.