# DigiPlex - MediaCMS 
[![Typing SVG](https://readme-typing-svg.herokuapp.com?font=Fira+Code&pause=1000&width=435&lines=DigiPlex+MediaCMS+Server+For+Digivalet)](https://git.io/typing-svg)

This is the DigiPlex a MediaCMS for **Digivalet** and files which can be hosted as **Standalone** or **Dockerized Container**

DigiPlex is a modern, fully featured open source video and media CMS. It is developed to meet the needs of modern web platforms for viewing. It can be used to build a small to medium video and media portal within minutes. 

It is built mostly using the modern stack Django + React and includes a REST API.


## Screenshots

<img src="https://i.ibb.co/tHTqDQD/Screenshot-from-2023-01-10-13-06-10.png" width="340">
<img src="https://i.ibb.co/RCGvccT/Screenshot-from-2023-01-10-13-33-12.png" width="340">



## Features
- **Complete control over your data**: host it yourself!
- **Modern technologies**: Django/Python/Celery, React.
- **Multiple media classification options**: categories, tags and custom
- **Easy media searching**: enriched with live search functionality
- **Responsive design**: including light and dark themes
- **Advanced users management**: allow self registration, invite only, closed.
- **Configuration options**: change logos, fonts, styling, add more pages
- **Enhanced video player**: customized video.js player with multiple resolution and playback speed options
- **Multiple transcoding profiles**: sane defaults for multiple dimensions (240p, 360p, 480p, 720p, 1080p) and multiple profiles (h264, h265, vp9)
- **Adaptive video streaming**: possible through HLS protocol
- **REST API**: Documented through Swagger


## Hardware dependencies

For a small to medium installation, with a few hours of video uploaded daily, and a few hundreds of active daily users viewing content, 4GB Ram / 2-4 CPUs as minimum is ok. For a larger installation with many hours of video uploaded daily, consider adding more CPUs and more Ram.    

In terms of disk space, think of what the needs will be. A general rule is to multiply by three the size of the expected uploaded videos (since the system keeps original versions, encoded versions plus HLS), so if you receive 1G of videos daily and maintain all of them, you should consider a 1T disk across a year (1G * 3 * 365).


## Releases

Visit [Releases Page](docs/release.md) for detailed Changelog


## Installation / Maintanance

To run DigiPlex, through Docker Compose and through installing it on a server via an automation script that installs and configures all needed services. Find the related pages:
 
* [SMTP Config](docs/soon.md) page - `Coming Soon!!`
* [Pre-Installation](docs/soon.md) page - `Coming Soon!!`
* [Docker Compose](docs/docker-install.md) page
* [Post-Installation](do)
* [Developer Documentation](docs/developers_docs.md) page
* [Admin Config](docs/admins_docs.md) page


## Technology
This software uses the following list of awesome technologies: Python, Django, Django Rest Framework, Celery, PostgreSQL, Redis, Nginx, uWSGI, React, Fine Uploader, video.js, FFMPEG, Bento4

