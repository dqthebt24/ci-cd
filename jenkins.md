# Jenkins knowledge

## Installation on Ubuntu
There are two ways to use Jenkins are using Docker and install directly to the machine.
The first one often use in the CI/CD process. This session will be about the second way.

1. System info

    This installation is on Ubuntu 16.04.

2. Install
s- Run these commands to install
```console
$wget -q -O - https://pkg.jenkins.io/debian-stable/jenkins.io.key
| sudo apt-key add –

$sudo echo “deb https://pkg.jenkins.io/debian-stable binary/” &gt;&gt;
/etc/apt/sources.list

$sudo apt-get update

$sudo apt-get install Jenkins

```
- Start Jenkins service

```console
$sudo apt-get install Jenkins
```
- Check Jenkins service using command

```console
$sudo service jenkins status
```

3. Open firewall port for Jenkins
- Accept firewall for port 8080 using command
```console
$sudo ufw allow 8080
```
- View Jenkins configs at: `/etc/default/jenkins`

- Restart Jenkins service
```console
$sudo service jenkins restart
```

- Open Jenkins web serive at: http://localhost:8080

## Tricks
- **How to exclude a file or folder from SVN monitoring in Jenkins build?**
    - In your **Job Configuration**, under **Source Code Management** section, click the **Advanced...** button.
    - This opens up **Excluded Regions** field. Click the question **?** icon next to it for more information. Add the excluded region as:
        > /exclude-folder/.*
        
    - **Note**: The pattern is relative from the **root of your repo**