# Create your own email server

## Installing CyberPanel

### Requirements

- Server with a fresh install of Centos 7.x (Not recommended for new installs), Centos 8.x, Ubuntu 18.04, Ubuntu 20.04, AlmaLinux 8, Ubuntu 22.04 (we use CentOS 7 in this tutorial)
- Python 3.x
- 1024MB RAM, or higher
- 10GB Disk Space

### 1. Update packages

`yum update -y`

### 2. Run the installation script

`sh <(curl https://cyberpanel.net/install.sh || wget -O - https://cyberpanel.net/install.sh)`

Please choose `OpenLiteSpeed`

Note: All the steps that ask you to make a choice can be made default.

The installation would be a very long time. So if possible, choose vultr for you VPS.

### 3. Change your password

You can use `adminPass [your new password]` to change the pw.

## Configuring

### 1. Access your CyberPenal

Input `[your domin]:8090` to log in. Your username will be `admin`

### 2. Create Website

| Item               | Setting                 |
| ------------------ | ----------------------- |
| Select Package     | Default                 |
| Select Owner       | admin                   |
| Domain Name        | [Your domain]           |
| Email              | [Your current email]    |
| Select PHP         | PHP 7.4                 |
| Additional Feature | SSL; DKIM; open_basedir |

After the setting, click the `Create Website`

### 3. DNS Config

In the part, you should finish DNS configuration by consulting the `ADD/MODIFY DNS ZONE` on CyberPanel. The records are as following:

| Type  | Name                        | Host                           |
| ----- | --------------------------- | ------------------------------ |
| A     | [domain]                    | @                              |
| A     | mail.[domain]               | mail                           |
| CNAME | www.[domain]                | www                            |
| MX    | [domain] (priority = 10)    | @                              |
| TXT   | [domain]                    | @                              |
| TXT   | _dmarc.[domain]             | _dmarc                         |
| TXT   | _domainkey.[domain]         | _domainkey                     |
| TXT   | default._domainkey.[domain] | default._domainkey (remove " ) |

Beside, you should change your reverse DNS for your vps. The value should be your domain.

### 4. Check DNS

1. Go to `whatsmydns.net`, input your domain, choose A records or MX records, and click `Search`
2. Go to `mxtoolbox.com`, input your ip address, and click `Reverse Lookup`

### 5. Issue SSL

1. Go back to CyberPanel, and choose `SSL` > `MailServer SSL`. Select your website/domain, and click `Issue SSL`.

2. Click `Hostname SSL`. Select your website/domain, and click `Issue SSL`. Now you can access your website of CyberPanel through `https://[domain]:8090`

## Create Email

1. Click `Create Email`, Select your website/domain, and set your `User Name` and `Password` for your email address.
2. Now you can access your email by clicking `Access Webmai`. 
3. Log in your email account.
4. Then, go back to CyberPanel. Click `List Emails`, and select your website/domain. Note that you may meet a SSL configuration problem. If so, click `Fix Now` to fix it.

## Test Email

1. Go to `mail-tester.com` and copy the text `test-cqfusmito@srv1.mail-tester.com`.

2. Go back to your Webmail, and send a email to this copied email address.
3. Then go back to `mail-tester.com`, and click `Then check your score`.

That's all the steps you should do to create your own email server. 

This tutorial consults IdeaSpot's channel. You can check his tutorial video through this [link][https://www.youtube.com/watch?v=uzrixSmvZJA].





