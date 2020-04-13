# Installing and configuring Digital Ocean on MacOS

## doctl is a command line interface for the DigitalOcean API.
```bash
## Doctl commands 

Usage:
  doctl [command]

Available Commands:
  account     account commands
  auth        auth commands
  completion  completion commands
  compute     compute commands
  databases   database commands
  help        Help about any command
  kubernetes  kubernetes commands
  projects    projects commands
  version     show the current version

```
```bash
Ashwarys-MBP:~ ashwarybhatt$ brew install doctl
Updating Homebrew...
==> Auto-updated Homebrew!
Updated 2 taps (homebrew/core and homebrew/cask).
==> New Formulae
---
--
==> Pouring doctl-1.39.0.high_sierra.bottle.tar.gz
==> Caveats
Bash completion has been installed to:
  /usr/local/etc/bash_completion.d

zsh completions have been installed to:
  /usr/local/share/zsh/site-functions
==> Summary
🍺  /usr/local/Cellar/doctl/1.39.0: 5 files, 26.4MB
Ashwarys-MBP:~ ashwarybhatt$ do
do          doctl       domainname  done        dot_clean
Ashwarys-MBP:~ ashwarybhatt$ doctl version
doctl version 1.39.0-release
Ashwarys-MBP:~ ashwarybhatt$

## In order to use doctl, you need to authenticate with DigitalOcean by providing an access token. Generated my personal access token.

Ashwarys-MBP:~ ashwarybhatt$ doctl auth init
Please authenticate doctl for use with your DigitalOcean account. You can generate a token in the control panel at https://cloud.digitalocean.com/account/api/token

Enter your access token:
Validating token... OK

Ashwarys-MBP:~ ashwarybhatt$


Ashwarys-MBP:~ ashwarybhatt$ doctl balance get
Month-to-date Balance    Account Balance    Month-to-date Usage    Generated At
1.01                     0.00               1.01                   2020-04-02T07:48:48Z
Ashwarys-MBP:~ ashwarybhatt$


Ashwarys-MBP:~ ashwarybhatt$ doctl compute droplet list
ID           Name    Public IPv4      Private IPv4    Public IPv6    Memory    VCPUs    Disk    Region    Image                       Status    Tags    Features    Volumes
185638308    bond    167.71.212.85                                   1024      1        25      sgp1      Ubuntu 18.04.3 (LTS) x64    active
Ashwarys-MBP:~ ashwarybhatt$
Ashwarys-MBP:~ ashwarybhatt$ doctl compute droplet create test --region sgp1 --image ubuntu-18-04-x64 --size 1gb
ID           Name    Public IPv4    Private IPv4    Public IPv6    Memory    VCPUs    Disk    Region    Image                       Status    Tags    Features    Volumes
188197645    test                                                  1024      1        30      sgp1      Ubuntu 18.04.3 (LTS) x64    new
Ashwarys-MBP:~ ashwarybhatt$

Ashwarys-MBP:~ ashwarybhatt$ doctl compute droplet list
ID           Name    Public IPv4        Private IPv4    Public IPv6    Memory    VCPUs    Disk    Region    Image                       Status    Tags    Features    Volumes
185638308    bond    167.71.212.85                                     1024      1        25      sgp1      Ubuntu 18.04.3 (LTS) x64    active
188197645    test    178.128.107.182                                   1024      1        30      sgp1      Ubuntu 18.04.3 (LTS) x64    active
Ashwarys-MBP:~ ashwarybhatt$

Ashwarys-MBP:~ ashwarybhatt$ doctl compute droplet delete test
Warning: Are you sure you want to Delete 1 droplet(s)? (y/N) ? y
Ashwarys-MBP:~ ashwarybhatt$ 
Ashwarys-MBP:~ ashwarybhatt$ doctl compute droplet list
ID           Name    Public IPv4      Private IPv4    Public IPv6    Memory    VCPUs    Disk    Region    Image                       Status    Tags    Features    Volumes
185638308    bond    167.71.212.85                                   1024      1        25      sgp1      Ubuntu 18.04.3 (LTS) x64    active
Ashwarys-MBP:~ ashwarybhatt$

```

# Install & set up Bitwarden CLI

## The Bitwarden CLI is a powerful tool to access and manage a Bitwarden vault through the command line. 

```bash

Ashwarys-MBP:~ ashwarybhatt$ bw --version
1.9.1 
Ashwarys-MBP:~ ashwarybhatt$ bw login
? Email address: shruti26.inbox@gmail.com
? Master password: [hidden]
You are logged in!


## Bitwarden Commands

Commands:

  login [options] [email] [password]          Log into a user account.
  logout                                      Log out of the current user account.
  lock                                        Lock the vault and destroy active session keys.
  unlock [options] [password]                 Unlock the vault and return a new session key.
  sync [options]                              Pull the latest vault data from server.
  list [options] <object>                     List an array of objects from the vault.
  get [options] <object> <id>                 Get an object from the vault.
  create [options] <object> [encodedJson]     Create an object in the vault.
  edit [options] <object> <id> [encodedJson]  Edit an object from the vault.
  delete [options] <object> <id>              Delete an object from the vault.
  share <id> <organizationId> [encodedJson]   Share an item to an organization.
  confirm [options] <object> <id>             Confirm an object to the organization.
  import [options] [format] [input]           Import vault data from a file.
  export [options] [password]                 Export vault data to a CSV or JSON file.
  generate [options]                          Generate a password/passphrase.
  encode                                      Base 64 encode stdin.
  config <setting> [value]                    Configure CLI settings.
  update                                      Check for updates.

Ashwarys-MBP:~ ashwarybhatt$ bw list items --search termius
? Master password: [hidden]
[{"object":"item","id":"ba5a5937-c2a8-4d89-b88c-ab7b00b1eac2","organizationId":null,"folderId":null,"type":1,"name":"account.termius.com","notes":null,"favorite":false,"login":{"uris":[{"match":null,"uri":"https://account.termius.com/sign-up"}],"username":"shruti26.inbox@gmail.com","password":"****","totp":null,"passwordRevisionDate":null},"collectionIds":[],"revisionDate":"2020-03-11T10:47:46.563Z"}]
Ashwarys-MBP:~ ashwarybhatt$

Ashwarys-MBP:~ ashwarybhatt$ bw get item teamviewer
? Master password: [hidden]
{"object":"item","id":"56b4d3f3-46bf-4771-a3f6-ab7b00bc69fb","organizationId":null,"folderId":null,"type":1,"name":"login.teamviewer.com","notes":null,"favorite":false,"login":{"uris":[{"match":null,"uri":"https://login.teamviewer.com/LogOn"}],"username":"shruti26.inbox@gmail.com","password":"****","totp":null,"passwordRevisionDate":null},"collectionIds":[],"revisionDate":"2020-03-11T11:25:59.660Z"}
Ashwarys-MBP:~ ashwarybhatt$

Ashwarys-MBP:~ ashwarybhatt$ bw sync --last
? Master password: [hidden]
2020-04-11T15:36:33.642Z

Ashwarys-MBP:~ ashwarybhatt$ bw sync
? Master password: [hidden]
Syncing complete.
Ashwarys-MBP:~

```