**MISSING**
**MISSING**

Frequentis TAPtools? - Python in Air Traffic Control
====================================================

**MISSING**
**MISSING**
**Category:**  Software Development, Business, Government, Scientific

**Keywords:**  Aviation, Java and Python, Public Safety, Traffic Control, Weather, Homeland Security, User Interface

**Title:**  Frequentis TAPtools? - Python in Air Traffic Control

**Author:**   Michael Bartl

**Date:**   2004-06-02

**Website:**  `http://www.frequentis.com/ <http://www.frequentis.com/>`_

**Summary:**  Python and Jython provide the basis for flexible and portable user interface layout and execution engines used in the Tower and Airport segment of Air Traffic Control.

**Logo:**  .. image:: /files/success/frequentis/frequentis-logo.gif    :alt: /files/success/frequentis/frequentis-logo.gif

Introduction
------------

`Frequentis <http://www.frequentis.com/>`_ is one of the world's leading providers for safety-critical
solutions in the field of Air Traffic Management and Public Safety &
Transport. With over 500 employees world-wide, it provides innovative,
user-centered solutions to its customers.

Frequentis has been using Python in its `TAPtools? <http://www.taptools.com/>`_ product family, which
focuses on the *Tower and Airport Tools* segment of Air Traffic Control.
These tools are used by air traffic controllers to track weather conditions,
control runway lighting, and to monitor and control navigational aid instruments.

.. image:: /files/success/frequentis/main-web.png
   :alt: Runway Control Screen

*TAPtools? products display runway and weather conditions for air traffic
controllers managing the approach of incoming aircraft* `Zoom in </files/success/frequentis/main.png>`_

A Brief History
---------------

One of the problems in developing air traffic control solutions is that each
customer's unique airport, regulatory picture, and methodologies impose
specific and different requirements for user interface look and behavior. A
significant part of the deployment of an air traffic control system is the
customization of its interface.

Instead of developing each user interface from the ground up on a per-customer
basis, Frequentis has developed a user interface layout tool called PanView,
similar to products like QDesigner or Visual Studio. This tool is used to
design and build the user interface which is then executed by a piece of
software called the PanMachine. The PanMachine runs on in-house developed
hardware called the PowerPanel, a 66MHz PowerPC with 32 MB RAM and a 12&quot;
touch screen entry device.

.. image:: /files/success/frequentis/screen-web.png
   :alt: Custom Interface Screenshot

*TAPtools? user interfaces are developed for the unique requirements of
each air traffic control customer* `Zoom in </files/success/frequentis/screen.png>`_

With these tools, Frequentis developers can rapidly prototype a layout in
front of the customer, greatly reducing the number of customer design workshops
necessary in the deployment of a solution.

The Customer is King
--------------------

PanView and the PanMachine were originally developed using `Lua <http://www.lua.org/>`_ as the
scripting language used to connect the user interface to the underlying
functionality of the air traffic control system.

This choice was found to be problematic for the layout implementors for
a variety of reasons:

- Limited information is provided on errors, making it hard for developers to locate bugs.

- Variables are global, not local, by default.  Python is exactly the other way around, making programs less prone to error.

- Lua has no list data structure.  Although its dictionaries can be used as lists, this caused unnecessary complexity in practice.

- Lua code is easy to follow for short scripts, but its syntax and minimal standard library makes it unmanageable for larger programs.

In a very important project, the Finnish Civil Aviation Administration (FCAA)
wanted to run their user interface layouts not just on the PowerPanel, but
also in the context of a web browser.  This requirement was important enough
that it led to re-implementation of the PanMachine in Java, so it could be
run as an applet in the browser.  Because Lua could not be run under Java, this
was a good time to replace it.

Python and `Jython <http://www.jython.org/>`_, the Java implementation of Python, were chosen because
they would allow both the PowerPC and Java implementations of the PanMachine
to execute the same user interface layouts.  Python, implemented in C, was
used on the PowerPC, and Jython, implemented in Java, was used in the browser
applet.

Implementation in Python
------------------------

Re-implementation using Python went smoothly. The Python language interpreter
and support libraries are written in C and can be compiled with most C
compilers. In this project, the ability for Python to be embedded into other
code worked very well. The `documentation <http://docs.python.org/extending/>`_ is excellent and the examples are
easy to follow.

However, the PowerPanel hardware has no hard disk and thus could not itself
compile the Python interpreter's C sources. To work around this problem, the
developers cross-compiled Python from another machine, producing object code
for the PowerPC using a compiler running on another type of hardware. Once
this was done, Python byte code produced on any machine could be run on the
PowerPanel without modification; only the initial compilation of the language
itself required cross-compilation.

Rewriting the Lua Layouts
-------------------------

Once the Python-based implementation of the GUI layout tools was complete,
it became necessary to rewrite the existing Lua layouts using Python.
Our layout coders embraced Python with open arms because it solved
all the problems they had been having with Lua, and it made new code
easier to write because of Python's straightforward syntax and extensive
standard libraries.

In this transition, we found that Python's syntax was very easy to learn
for new users, and our coders were able to completely rewrite the Lua
layouts to take advantage of the new features offered by Python, rather
than just porting them at the language level.

The finished layout code contains about 5000 lines, which is half the size of
the original code, is much easier to maintain, and works flawlessly with Jython
in the Java port of the PanMachine.

Conclusion
----------

Python enabled us to fulfill customer requirements in a time critical project,
while improving the overall quality of our tools. Since changing to Python,
layout implementation has become much easier for a variety of reasons:

- Python's runtime error handling makes it easier to locate and fix problems in code.  The stack traces produced by Python, even when running in staged production on the custom PowerPanel hardware, have helped to speed up the testing and debugging process.

- Python's vast standard libraries allow rapid development of functionality without resorting to re-invention of the wheel.

- Python's very clean syntax and indentation-based program structure makes code much easier to read and maintain.

Since using Python in our development, the time to write new user interface
layouts for the TAPtools? product family has been reduced by a factor three.

About the Author
----------------

*Michael Bartl initially joined Frequentis in 2000 as a software engineer to
test telecommunication hardware and later moved on to develop weather
information systems. After several years he is now Product Manager for the
TAPtools? product family. His main addictions are Java, Python and Chess.*