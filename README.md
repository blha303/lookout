Lookout
=======

Lightweight, web-based server monitoring.

The Python backend uses Flask and Tornado to serve JSON data thanks to psutil,
while the frontend uses Smoothie Charts for the live graphs.

What's this fork?
-----------------

I added a screenfetch output to it, using the two scripts in the bin directory. See it in action at http://stats.blha303.biz

What does it look like?
-----------------------

![screenshot](http://i.imgur.com/X3RD0LV.png)

Windows Server 2012 users
-------------------------

Please run `diskperf -y` to enable disk activity monitoring. Without doing so,
psutil and lookout will fail to run properly. As a side effect, doing so allows
you to also view disk activity in Task Manager.

Running directly from source
----------------------------

To run Lookout from source, install Python 2.7, pip and a C compiler. Windows
users should use MSVC++ 2008 (not even a newer version) for the least headaches.

Then install dependencies with `pip install -r requirements.txt`.

Finally, run `lookout.py` to start monitoring. You can optionally supply the
port to listen on as the first argument (e.g. `lookout.py 8080`), but the
default is port 80.

Skype users, please note that ports 80 and 443 are taken by default; you will
need to turn off "Use 80 and 443 for incoming connections" and restart Skype to
use those ports.

If you're using Debian, Ubuntu or relatives, setup might look like this:

	apt-get install git build-essential python python-dev python-pip
	git clone git://github.com/delan/lookout.git
	cd lookout
	pip install -r requirements.txt
	python lookout.py

How to build a standalone executable
------------------------------------

Werkzeug does some crazy import magic that breaks PyInstaller's module
detection, so please edit werkzeug's `__init__.py` and remove everything after
the line where `__version__` is defined.

Download PyInstaller and in this directory, run
`path/to/pyinstaller.py -F lookout.spec`.

The resulting executable will be found as `dist/lookout.exe`. Run it to start
monitoring, again with an optional port argument.
