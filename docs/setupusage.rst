Setup and usage
===============

There are two methods for setting up and running the test suite: the
"quick" method and the "virtualenv". For either to work, you must turn
on adb access on the device

Enabling ADB
------------

**For Firefox OS version 1.3:** Launch *Settings*, and navigate to
*Device Information* → *More Information* → *Developer*, then check
*Remote Debugging*.

**For version 1.4:** Launch *Settings*, and navigate to *Device
Information* → *More Information*, then check *Developer Options*.
Next, hold down the *Home* button, and close the *Settings* app (press
the x).  Finally, launch *Settings* again, and navigate to
*Developer*, then select *ADB only* in *Remote Debugging*.

Once this is done, go to *Settings* → *Display* and set the *Screen
Timeout* to “never”.  You need this because adb will not work when the
device is locked.

Quick setup and usage
---------------------

You can setup your environment and run the tests by running::

    ./run.sh --version=<some version>

The *--version* argument is optional.  If passed,
*--version* must be one of our supported release versions, either 1.3
or 1.4.  If you don't pass a version, 1.3 will be assumed.

This command sets up a virtual environment for you, with all the
proper packages installed, activates the environment, runs the tests,
and lastly deactivates the environment.

You may call *run.sh* as many times as you like, and it will run the
tests using its previously set up virtual environment.

Setup and usage with virtualenv
-------------------------------

If the quick setup doesn't work, then follow these instructions.  You
can set up and run this tool inside a virtual environment.  From the
root directory of your source checkout, run::

    virtualenv .
    ./bin/pip install -e .

Then activate the virtualenv::

    source bin/activate

Once the virtualenv is activated, the certification test suite can be
run by executing::

    runcertsuite

To get a list of command-line arguments, use::

    runcertsuite --help

WIP: Running Guided WebAPI Tests
--------------------------------

This test tool will eventually contain a full suite of guided WebAPI tests
that allow a tester to interact with the phone to perform functional
testing of WebAPI's.

This semi-auto harness is in development (and is thus not runnable
using the process above), but you can run a prototype of these tests
now. To do so:

    cd webapi_tests
    ./setup_and_run.sh <directory>

where <directory> is one of the directory names under webapi_tests that contains
tests, one of: sms, proximity, tcp_socket, telephony, orientation, or
vibration.

This will install a test app on your device, and then open a web page on
your host browser (*not* on the device), which will lead you through the tests.

Submitting Results
------------------

Once the tests have completed successfully, they will write a file
containing the results to disk; by default this file is called
*rfirefox-os-certification.zip* and will be put in your current working
directory. Please e-mail this file to fxos-cert@mozilla.com.

Known Issues
------------
* Tests fail if re-run on a device they've already been run on
[https://bugzilla.mozilla.org/show_bug.cgi?id=995455].  Workaround:
re-install gaia or re-flash the device before re-running the tests.

