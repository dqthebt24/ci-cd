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

4. First login to Jenkins
- Copy password from `/var/lib/jenkins/secrets/initialAdminPassword` to login
- Select **“Install suggested plugins”**
- Create new user on Jenkins web

## Manage Jenkins

1. Install plugins
- Go to **“Manage Jenkins”** -&gt; **“Plugin Manage”**
- To install a plugin, select "Available" then search the name of the plugin and click install

## Config SMTP
   This session config smtp for sending email after a build. Follow these steps.
- Go to **“Manage Jenkins”** -&gt; **“Configure System”**.
- Go to session **“E-mail Notification”**.
- Configure as bellow instructions:
    - **SMTP server**: stmp.gmail.com
    - **Default user e-mail suffix**: @gmail.com
    - Click **“Advanced…”**
    - Check **“Use SMTP Authentication”**
    - **Username**: &lt;your-email@gmail.com&gt;
    - **Password**: &lt;gmail-password&gt;
    - Check **“Use SSL”**
    - Uncheck **“Use TSL”**
    - **SMTP Port**: 465
    - **Reply-To Address**: &lt;empty&gt;
    - **Charset**: UTF-8
- To test the configuration:
    - Check **“Test configuration by sending test e-mail”**
    - **Test e-mail recipient**: Provide an email address to receive the test
email, ex: test@terralogic.com
    - Check inbox email from the target email address.
- **Note:** User need to enable "Gmail for less secure apps". Do the steps in this [tutorial](https://hotter.io/docs/email-accounts/secure-app-gmail/) to enable.
## Tricks
- **How to exclude a file or folder from SVN monitoring in Jenkins build?**
    - In your **Job Configuration**, under **Source Code Management** section, click the **Advanced...** button.
    - This opens up **Excluded Regions** field. Click the question **?** icon next to it for more information. Add the excluded region as:
        > /exclude-folder/.*
        

    - **Note**: The pattern is relative from the **root of your repo**