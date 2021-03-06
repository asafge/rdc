rdc
===
A remote desktop (xfreerdp) connections manager.


FILES
-----
* settings.py: tunables
* model.py: takes care of loading and saving the user's configuration file to the GTK GUI and back
* tests/: contains unit tests
* connection.py: functions that actually call xfreerdp
* rdp_ui.py: the gui and the main routines
* ui_prorotype.glade: prototype for the gui, open with glade-3 <filename>. Only a prototype, GUI wasn't generated by it

CONF FILES
==========
1. ~/.rdp_connections - list of user's RDP connection entries 
------------------------------------------------------
Format: <display name>:<address>:<user>:<domain>
e.g. My Server:1.2.3.4:moshe:mydomain

Notes:
1. newline character after each entry
2. fields could be left empty but three colons (:::) must appear
3. Illegal lines should be skipped
4. Check the log for detailed info on conf file parsing
5. Being both read & written by rdc_ui

2. ~/.rdp_general - general user settings
-----------------------------------------
Format: <key>=<value>
e.g. readonly=yes

Allowed keywords (see model.py file for most up-to-date list): 
- readonly (only if set to 'yes' it has an effect, all other values do nothing). Note that '-r' flag also sets readonly to yes.

Notes:
1. Illegal lines are skipped
2. Check the log for detailed info on conf file parsing
3. Not being written/modified by rdc_ui


GUI
---
GUI widgets are created in RdpUI class inside rdp_ui.py module.
Most of the GUI creation is done from __init__() method, which calls some other methods such as create_window(), create_buttons(). It tries to be as readable as possible..

REQUIREMENTS
------------
* Python 2.x (2.6 and up)
* PyGTK 2 (rpm name: pygtk2)
* gconf (rpm name: gnome-python2-gconf)
* xfreerdp 

Was developed and tested on CentOS 6.0:
* The OS's original Python and Python modules
* A manually installed xfreerdp 0.8.2


TROUBLESHOOTING
---------------
1. Set logging to logging.DEBUG (in settings.py) and run rdc_ui.py from the console. Lots of informative messages would be printed


UNIT TESTS
----------
The project contains a few unit tests, as it's mostly GUI which is hard to test.
To run the unittest simply run 'nosetests .' when inside the project's directory.
(requires the 'nose' directory)


DEPLOYMENT
----------
Easiest deployment is simply unpacking the project's directory into /opt/, e.g. /opt/rdc/.
Then running /opt/rdc/rdc_ui.py should do.


AUTHOR
------
Oren Held
Written on Dec 2011
