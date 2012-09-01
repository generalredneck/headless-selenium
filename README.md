Headless Selenium
=================

## What do I need?
Yes there are a few dependencies for this to work. The following list (possibly incomplete) is everything that I can think of off the top of my head:

* Java
* Xvfb
* Selenium Server
* Firefox
* Linux

## Headless Selenium Service
You should be able to get all of these things from your local Linux distribution. Notice, I tend to sway for Debian based Linux distributions.

## How do I install?
### Step 1
Download the latest script from my github repository and place the script in `/etc/init.d/`.

### Step 2
Make the directory `/usr/lib/headless-selenium`.

### Step 3
Download Selenium Server and place it in `/usr/lib/headless-selenium`.

### Step 4
Edit the variable `SELENIUM_JAR` in the service file with the name of the selenium server you downloaded. (At the time I wrote the service the latest was 2.24.1)

### Step 5
Create the directores up to `/usr/lib/headless-selenium/profiles/firefox`

### Step 6
Create a selenium profile using firefox. There are several tutorials out there (particularly handy one). I've taken the liberty of creating a default one that you can do what you want to with.

### Step 7
Put that Profile in `/usr/lib/headless-selenium/profiles/firefox/selenium`.

### Step 8
Start the service! `sudo /etc/init.d/headless-selenium start`

## Usage
```
sudo /etc/init.d/headless-selenium start
sudo /etc/init.d/headless-selenium stop
sudo /etc/init.d/headless-selenium restart
sudo /etc/init.d/headless-selenium status
```

## Debugging
You may need to debug whether headless selenium is running. The process that is best used is the following:

### Check service status:
`sudo /etc/init.d/headless-selenium status`

Headless Selenium should be “running”

### Restart service:
`sudo /etc/init.d/headless-selenium restart`

### Get a screenshot of Xvfb
`DISPLAY=:42 import -window root screenshot.png`

### Check for output printed to the logs:
`sudo tail -f /var/log/selenium/selenium-output.log`

Note: There are several different logs in /var/log/selenium which may be useful.
Check to see if headless selenium is running via a process manager:
```
ps -ef | grep selenium
ps -ef | grep Xvfb
```