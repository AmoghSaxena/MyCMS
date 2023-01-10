
# Administrators documentation


## Welcome

This page is created for DigiPlex administrators that are responsible for setting up the software, maintaining it and making modificatio

## Installation


Install a recent version of [Docker](https://docs.docker.com/get-docker/), and [Docker Compose](https://docs.docker.com/compose/install/).

For Ubuntu 18/20 systems this is:

```bash

curl -fsSL https://get.docker.com -o get-docker.sh

sudo sh get-docker.sh

sudo curl -L "https://github.com/docker/compose/releases/download/1.29.2/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose

sudo chmod +x /usr/local/bin/docker-compose


```
Then run as root

```bash

git clone https://dvgit.digivalet.com/scm/pyt/videocms.git

cd videocms && git checkout dev

```

The default option is to serve DigiPlex on all ips available of the server (including localhost).

Run

```bash

docker-compose up

```

This will download all DigiPlex related Docker images and start all containers. Once it finishes, DigiPlex will be installed and available on http://localhost:8084 or http://ip:8086

A user admin has been created with random password, you should be able to see it at the end of migrations container, eg
 

```
 

migrations_1 | Created admin user with password: gwg1clfkwf
 

```

or if you have set the ADMIN_PASSWORD variable on docker-compose file you have used (example `docker-compose.yaml`), that variable will be set as the admin user's password

## Update

Get latest DigiPlex image and stop/start container

```bash

cd /path/to/digiplex/installation
docker-compose down
git pull
docker-compose up

```

## Maintenance

Database is stored on ../postgres_data/ and media_files on media_files/


## Configuration

Several options are available on `cms/settings.py`, most of the things that are allowed or should be disallowed are described there.

### Change portal logo

Set a new svg file for the white theme (`static/images/logo_dark.svg`) or the dark theme (`static/images/logo_light.svg`)

### Set global portal title
set `PORTAL_NAME`, eg
 

```

PORTAL_NAME = 'my awesome portal'

```

### Control who can add media

By default `CAN_ADD_MEDIA = "all"` means that all registered users can add media. Other valid options are:

-  **email_verified**, a user not only has to register an account but also verify the email (by clicking the link sent upon registration). Apparently email configuration need to work, otherise users won't receive emails.

-  **advancedUser**, only users that are marked as advanced users can add media. Admins or DigiPlex managers can make users advanced users by editing their profile and selecting advancedUser.

### What is the portal workflow

The `PORTAL_WORKFLOW` variable specifies what happens to newly uploaded media, whether they appear on listings (as the index page, or search)

-  **public** is the default option and means that a media can appear on listings. If media type is video, it will appear once at least a task that produces an encoded version of the file has finished succesfully. For other type of files, as image/audio they appear instantly

-  **private** means that newly uploaded content is private - only users can see it or DigiPlex editors, managers and admins. Those can also set the status to public or unlisted

-  **unlisted** means that items are unlisted. However if a user visits the url of an unlisted media, it will be shown (as opposed to private)

### Show or hide the Sign in button

 to show button:

```

LOGIN_ALLOWED = True

```

to hide button:

```

LOGIN_ALLOWED = False

```
### Show or hide the Register button  

to show button:

```
REGISTER_ALLOWED = True
```

to hide button:

```

 
REGISTER_ALLOWED = False


```

  

  

### Show or hide the upload media button

  

  

To show:

  

  

```

  

UPLOAD_MEDIA_ALLOWED = True

  

```

  

  

To hide:

  

  

```

  

UPLOAD_MEDIA_ALLOWED = False

  

```

  

  

### 5.11 Set a custom message on the media upload page

  

  

this message will appear below the media drag and drop form

  

  

```

  

PRE_UPLOAD_MEDIA_MESSAGE = 'custom message'

  

```

  

  

## Set email settings

  

  

Set correct settings per provider

  

  

```

  

DEFAULT_FROM_EMAIL = 'info@mediacms.io'

  

EMAIL_HOST_PASSWORD = 'xyz'

  

EMAIL_HOST_USER = 'info@mediacms.io'

  

EMAIL_USE_TLS = True

  

SERVER_EMAIL = DEFAULT_FROM_EMAIL

  

EMAIL_HOST = 'mediacms.io'

  

EMAIL_PORT = 587

  

ADMIN_EMAIL_LIST = ['info@mediacms.io']

  

```

  

  

## Disallow user registrations from specific domains

  

  

set domains that are not valid for registration via this variable:

  

  

```

  

RESTRICTED_DOMAINS_FOR_USER_REGISTRATION = [

  

'xxx.com', 'emaildomainwhatever.com']

  

```

  

  

## Require a review by DigiPlex editors/managers/admin

  

set value

  

```

  

MEDIA_IS_REVIEWED = False

  

```

  

any uploaded media now needs to be reviewed before it can appear to the listings.

  

DigiPlex editors/managers/admins can visit the media page and edit it, where they can see the option to mark media as reviewed. By default this is set to True, so all media don't require to be reviewed

  
  

### Specify maximum size of a media that can be uploaded

  

  

change `UPLOAD_MAX_SIZE`.

  

  

default is 4GB

  

  

```

  

UPLOAD_MAX_SIZE = 800 * 1024 * 1000 * 5

  

```

  

  
  

### How many files to upload in parallel

  

  

set a different threshold for `UPLOAD_MAX_FILES_NUMBER`

  

default:

  

  

```

  

UPLOAD_MAX_FILES_NUMBER = 100

  

```

  

  

## Force users confirm their email upon registrations

  

  

default option for email confirmation is optional. Set this to mandatory in order to force users confirm their email before they can login

  

  

```

  

ACCOUNT_EMAIL_VERIFICATION = 'optional'

  

```

  

  

## Rate limit account login attempts

  

  

after this number is reached

  

  

```

  

ACCOUNT_LOGIN_ATTEMPTS_LIMIT = 20

  

```

  

  

sets a timeout (in seconds)

  

  

```

  

ACCOUNT_LOGIN_ATTEMPTS_TIMEOUT = 5

  

```

  

  

## Disallow user registration

  
  

set the following variable to False

  

```

USERS_CAN_SELF_REGISTER = True

```

  

  

## Configure notifications

  

  

Global notifications that are implemented are controlled by the following options:

  

  

```

  

USERS_NOTIFICATIONS = {

  

'MEDIA_ADDED': True,

  

}

  

```

  

  

If you want to disable notification for new media, set to False

  

  

Admins also receive notifications on different events, set any of the following to False to disable

  

  

```

  

ADMINS_NOTIFICATIONS = {

  

'NEW_USER': True,

  

'MEDIA_ADDED': True,

  

'MEDIA_REPORTED': True,

  

}

  

```

  

  

- NEW_USER: a new user is added

  

- MEDIA_ADDED: a media is added

  

- MEDIA_REPORTED: the report for a media was hit

  

  

## Configure only member access to media

- Make the portal workflow public, but at the same time set `GLOBAL_LOGIN_REQUIRED = True` so that only logged in users can see content.

  

- You can either set `REGISTER_ALLOWED = False` if you want to add members yourself or checkout options on "django-allauth settings" that affects registration in `cms/settings.py`. Eg set the portal invite only, or set email confirmation as mandatory, so that you control who registers.

  

  

## Add/delete categories and Departments

  

Through the admin section - http://your_installation/admin/

  

  

## Video transcoding

  

Add / remove resolutions and profiles through http://your_installation/admin/encodeprofile

  

  

## Restart the mediacms web server

  

On docker:

  

```

  

sudo docker-compose restart

  

```

  
  

  

  

## Debugging email issues

  

On the [Configuration](https://github.com/mediacms-io/mediacms/blob/main/docs/admins_docs.md#5-configuration) section of this guide we've see how to edit the email settings.

  

In case we are yet unable to receive email from DigiPlex, the following may help us debug the issue - in most cases it is an issue of setting the correct username, password or TLS option

  

Enter the Django shell, example if you're using the Single Server installation or jump into container named `web`:

  

```bash

  

source /home/mediacms.io/bin/activate

  

python manage.py shell

  

```

  

and inside the shell

  

```bash

  

from django.core.mail import EmailMessage

from django.conf import settings

  

settings.EMAIL_BACKEND = 'django.core.mail.backends.smtp.EmailBackend'

  

email = EmailMessage(

'title',

'msg',

settings.DEFAULT_FROM_EMAIL,

['recipient@email.com'],

)

  

email.send(fail_silently=False)

  

```

  
  

You have the chance to either receive the email (in this case it will be sent to recipient@email.com) otherwise you will see the error.

  

For example, while specifying wrong password for my Gmail account I get

  

  

```

  

SMTPAuthenticationError: (535, b'5.7.8 Username and Password not accepted. Learn more at\n5.7.8 https://support.google.com/mail/?p=BadCredentials d4sm12687785wrc.34 - gsmtp')

  

```

  

## Frequently Asked Questions

  

Video is playing but preview thumbnails are not showing for large video files

  
  

Chances are that the sprites file was not created correctly.

  

The output of files.tasks.produce_sprite_from_video() function in this case is something like this

  

```

  

convert-im6.q16: width or height exceeds limit `/tmp/img001.jpg' @ error/cache.c/OpenPixelCache/3912.

  

```

  
  

Solution: edit file `/etc/ImageMagick-6/policy.xml` and set bigger values for the lines that contain width and height. For example

  

```

  

<policy domain="resource" name="height" value="16000KP"/>

  

<policy domain="resource" name="width" value="16000KP"/>

  

```

  
  

Newly added video files now will be able to produce the sprites file needed for thumbnail previews. To re-run that task on existing videos, enter the Django shell

  
  
  

```

  

root@8433f923ccf5:/home/mediacms.io/mediacms# source /home/mediacms.io/bin/activate

  

root@8433f923ccf5:/home/mediacms.io/mediacms# python manage.py shell

  

Python 3.8.14 (default, Sep 13 2022, 02:23:58)

  

```

  

and run

  

```

from files.models import Media

from files.tasks import produce_sprite_from_video

  

for media in Media.objects.filter(media_type='video', sprites=''):

produce_sprite_from_video(media.friendly_token)

  

```

  

this will re-create the sprites for videos that the task failed.