# southwest-headers

IYKYK. 😄

Working on Ubuntu 20.04. YMMV.

Huge thanks and praise to https://github.com/byalextran/southwest-headers for blazing this trail. I really only forked his work in order to introduce redundancy and have a repo under my control so that my altered version of [wgriffing/SouthwestCheckin](https://github.com/WGriffing/SouthwestCheckin) can integrate with it.

## Prerequisites

- python3
- pip3

## Installation

### Install Google Chrome

```bash
$ wget https://dl.google.com/linux/direct/google-chrome-stable_current_amd64.deb
$ sudo dpkg -i google-chrome-stable_current_amd64.deb
```

### Install Southwest Headers

```bash
$ git clone https://github.com/wgriffing/southwest-headers
$ cd southwest-headers
$ git checkout develop
$ pip3 install virtualenv
$ python3 -m virtualenv venv
$ source venv/bin/activate
(venv)$ pip install -r requirements.txt
```

## Usage

No arguments saves the headers to `southwest_headers.json` in the current directory.

```bash
(venv)$ python southwest-headers.py
```

Include an argument if you want to specify where the headers are saved to.

```bash
(venv)$ python southwest-headers.py /PATH/TO/FILENAME.json
```

The JSON file can then be used in whatever app to auto check-in (assuming the script adds support for reading this file).

I've added support in my script here:

https://github.com/WGriffing/SouthwestCheckin and the expected usage is with no arguments in a parallel folder structure (top level dir should have a `SouthwestCheckin` and `southwest-headers` git clones)

## Add a Cron Job

For now, I'd recommend running this script as a daily cronjob to ensure headers are refreshed regularly. They change periodically, so if this isn't done there's a chance you'll have expired headers when you try to check in.

```bash
$ crontab -e
```

And then copy/paste the following at the end of the file (making sure to update it with the _absolute_ path):

```text
0 2 * * *       cd /ABSOLUTE/PATH/TO/southwest-headers/ && venv/bin/python southwest-headers.py
```

That would run at 2:00am every day with the file `southwest_headers.json` (the default filename) saved in the `southwest-headers` folder.
