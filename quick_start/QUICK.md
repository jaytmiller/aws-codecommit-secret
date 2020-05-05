# Quick Start

## Overview

These instructions and scripts are not a replacement for the README, just
a codification of the process and system explained there in more detail.

## Prerequisites

In order to use these scripts you will need to install and appropriately
configure:

1. The AWS CLI.

   Version 2 has a dedicated installer vs. pip install.

   https://docs.aws.amazon.com/cli/latest/userguide/install-cliv2.html

   Version 1 is a simple pip install but doesn't support YAML output formatting

   ```$ pip install awscli boto3```

2. git-remote-codecommit

   ```$ pip install git-remote-codecommit```

3. SOPS

   https://github.com/mozilla/sops

   I installed golang and built sops from source as shown in git.

4. awsudo (https://github.com/meltwater/awsudo)

   Install nodejs,  then

   ```$ npm install -g awsudo```

5. You must have permission to assume AWS IAMRoleAdministrator.

## Define your repo

Customize the input files `your-vars.env` and `your-vars.tfvars`.

It's critical to use the same repository name, account, and region in both.

## Standing up your repo

This is all that is required to set up huploy secrets,  check out your repo
into this directory,  and test a first push.

```./setup```

## Encrypting Files

The commands below will create *MyFirstSecretsFile* by opening an EDITOR
window and letting you type in secrets.   Afterwards, MyFirstSecretsFile
is added to the repo and pushed to CodeCommit using the encryption role
created during *./setup* above.

```
cd <your-repo-name>
./encrypt MyFirstSecretsFile
```

## Decrypting Files

The commands below will decrypt MyFirstSecretsFile and display the result
in an EDITOR window.

```
cd <your-repo-name>
./decrypt MyFirstSecretsFile
```

## Tearing Down

Tearing down all the terraform artifacts and DELETING YOUR SECRETS REPO
is easy:

```
./teardown
```

It deletes all copies of your repo because once the Terraform artifacts
are torn down neither the CodeCommit repo nor your local copy can be
decrypted.
