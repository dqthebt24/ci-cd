# Jenkins knowledge

## Table of Contents
1. [Installation on Ubuntu](#ubuntu-installation)
1. [Manage Jenkins](#management)
    1. [Plugins installations](#mgm-plugin-install)
    1. [Email sending](#mgm-email-sending)
        1. [STMP server configuration](#mgm-smtp-config)
        1. [Config send email to a list of emails](#mgm-list-email-config)
    1. [Build on agents](#mgm-build-agent)
        1. [Add agent nodes](#mgm-build-agent-add)
        1. [Assign an agent for a job](#mgm-build-agent-assign)

## Installation on Ubuntu <a name="ubuntu-installation">
There are two ways to use Jenkins are using Docker and install directly to the machine.
The first one often use in the CI/CD process. This session will be about the second way.

#### 1. System info

   This installation is on Ubuntu 16.04.

#### 2. Install
- Run these commands to install
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

#### 3. Open firewall port for Jenkins
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

#### 4. First login to Jenkins 
- Copy password from `/var/lib/jenkins/secrets/initialAdminPassword` to login
- Select **“Install suggested plugins”**
- Create new user on Jenkins web

## Manage Jenkins <a name="management">

### Plugins installations <a name="mgm-plugin-install">
- Go to **“Manage Jenkins”** -&gt; **“Plugin Manage”**
- To install a plugin, select **"Available"** then search the name of the plugin and click install

### Email sending <a name="mgm-email-sending">
   This session config smtp for sending email after a build.
#### 1. STMP server configuration <a name="mgm-smtp-config">
To send an email (in a build configuration), we need to config STMP server. These bellow steps to config SMTP server
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

#### 2. Config send email to a list of emails <a name="mgm-list-email-config">
   
   This config is used in sending email to a group of emails. Do these steps to configure
- Go to **“Manage Jenkins”** -&gt; **“Configure System”**.
- Go to session **“Extended E-mail Notification”**
- Configure as bellow:
    - **SMTP**: smtp.gmail.com
    - **Default user E-mail suffix**: @gmail.com
    - Click **“Advanced…”** then configure as the session configure SMTP
mail server
    - **Default Content Type**: Plain Text (text/plain)
    - **Default Recipients**: Add email to receive email notifications, ex:
test1@gmail.com, test2@gmail.com, cc:test3@gmail.com

### Build on agents <a name="mgm-build-agent">
   This sesson to config setting for building on agents in local network.
#### 1. Add agent nodes <a name="mgm-build-agent-add">

   Go to **“Manage Jenkins”** -&gt; **“Manage Nodes and Clouds”**

- Select **“New Node”**
- Enter the **“Node name”** -&gt; check **“Permanent Agent”** -&gt; click **“OK”**
- Configure the new agent as bellow instructions:
    - **Labels**: Type label to remember, ex: John Agent
    - **Remote root directory**: Type the path on the agent that you will store
the project to build, ex: `/home/john`, then when Jenkins build, it will
write files to the folder at `/home/john`
    - **Launch method**: **“Launch agents via SSH”**
    - **Host**: &lt;Ip of host&gt;, ex: `10.20.12.79`
    - **Credentials**: Click button **Add** then select **Jenkins**
    - Configure **Credentials**:
        - **Domain**: Global credentials (unrestricted)
        - **Kind**: Username with password
        - **Scope**: Global
        - **Username**: *&lt;enter_login_username_on_master_ssh_machine&gt;*
        - **Password**: *&lt;enter_ssh_password&gt;*

- Click **“Add”** -&gt; **“Save”**

When agents are added, Jenkins will choose one of them to build a job. We can assign an agent for a job with instructions bellows
  
#### 2. Assign an agent for a job <a name="mgm-build-agent-assign">
   Go to job configuration, check **“Restrict where this project can be run”** -&gt; type the agent name. Ex: *John Agent*

## Tricks
- **How to exclude a file or folder from SVN monitoring in Jenkins build?**
    - In your **Job Configuration**, under **Source Code Management** section, click the **Advanced...** button.
    - This opens up **Excluded Regions** field. Click the question **?** icon next to it for more information. Add the excluded region as:
        > /exclude-folder/.*
        

    - **Note**: The pattern is relative from the **root of your repo**