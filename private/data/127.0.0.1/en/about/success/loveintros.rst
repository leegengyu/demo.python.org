**MISSING**
**MISSING**

LoveIntros Uses Python to Help Northwest Singles Click
======================================================

**MISSING**
**MISSING**
**Category:**  Business, Software Development

**Keywords:**  ECommerce, Web2.0

**Title:**  LoveIntros Uses Python to Help Northwest Singles Click

**Author:**   Greg Unrein

**Date:**   2004-05-29

**Website:**  `http://www.loveintros.com/ <http://www.loveintros.com/>`_

**Summary:**  Northwest singles community loves Python for rapid development of clean, readable code.

**Logo:**  .. image:: /files/success/loveintros/loveintros-logo.gif    :alt: /files/success/loveintros/loveintros-logo.gif

Introduction
------------

`LoveIntros <http://www.loveintros.com/>`_ is an online singles community for people living in the Northwest
United States. The LoveIntros Web application allows members to create
personal profiles, send and receive anonymous e-mails, create private Web
journals, perform advanced profile searches, and execute many other functions.
By providing a safe and effective way for individuals to find each other,
LoveIntros makes it easier to meet new people who have similar interests and
values and who live in or near one's own community.

.. image:: /files/success/loveintros/screen0-web.png
   :alt: LoveIntros Screenshot

*LoveIntros is an online singles community that provides a safe effective
way for Northwest singles to find and meet each other* `Zoom in </files/success/loveintros/screen0.png>`_

The Architecture
----------------

As a software project, LoveIntros contains several different modules: The
end-user's Web application, the administrative interface, the anonymous email
daemon, and a cross-platform GUI component for editing some of the site's
content. Together, these modules provide all of the functionality needed by
users and administrators. The system is deployed on FreeBSD, but is portable
to other operating systems. In fact, most of the project's initial development
was done using Windows 2000.

The LoveIntros Web application allows users to create profiles, search for
others who interest them, and communicate with these individuals in order to
explore the potential for a relationship. This application is based on a
three-tier architecture. Data is stored in a `PostgreSQL <http://www.postgresql.org/>`_ database, and
`psycopg <http://initd.org/software/initd/psycopg>`_ provides database connectivity. The middle tier is coded in Python
and is driven by `mod_python <http://www.modpython.org/>`_ running under `Apache 2 <http://www.apache.org/>`_. The user interface
is rendered as HTML using the `SimpleTAL <http://www.owlfish.com/software/simpleTAL/>`_ template library.

The administrative interface to the site is written using the `Quixote <http://www.quixote.ca/>`_ Web
application framework, and employs `mod_scgi <http://www.mems-exchange.org/software/scgi/>`_ behind Apache 2. This interface
provides the site administrators access to all of the functions they need to
interact with user's profiles, process log files to provide reports about site
activity and issues, and update site content. Quixote and mod_scgi have
performed extremely well in this application, and plans call for them to
replace the current SimpleTAL and mod_python implementation of the user site.

Another important module of the LoveIntros project is its anonymous e-mail
daemon. This daemon strips the senders' e-mail addressed from correspondence
sent to other users, then forwards the e-mails on to their intended recipient.
As a result, members can communicate without the risk of accidentally
divulging their actual e-mail addresses. Because of the power of Python and
its associated libraries, this daemon consists of only a few hundred lines of
code, which include several response e-mail templates that are sent to notify
senders in the event that an e-mail could not be forwarded successfully.

Finally, LoveIntros includes a GUI application used to create a
domain-specific XML editor that allows nontechnical users to edit LoveIntros'
FAQ files. This was written using `PythonCard <http://pythoncard.sourceforge.net/>`_, a rapid GUI development tool
based on the `wxPython <http://www.wxpython.org/>`_ GUI framework. Inspired by Apple's HyperCard,
PythonCard was impressive in its ability to quickly and easily create a
responsive cross-platform GUI.

Implemented in Python
---------------------

The LoveIntros implementors chose Python for its expressive, easy-to-maintain
nature and its rich set of built-in libraries and excellent third-party
modules. Java and `Jython <http://www.jython.org/>`_, the Java-based implementation of the Python
programming language, were both considered as well, but were not chosen
because of the added complexity introduced by either approach, without
appreciable added value. Ultimately, Python's flexibility, coding speed,
solution quality, and libraries made it the language of choice for this
endeavor.

The LoveIntros project consumed approximately four months of full-time
development work, with one developer working on the Python code, and one
designer working on the UI. These four months of work were spread over more
than a year of actual part-time effort. Python helped the programmers sustain
this development rate in several ways:

First, Python is a very expressive language. The syntax is clean and easy to
read, and basic data structures are built in. It is amazing how much less
typing goes into Python code, since braces and type declarations are not used.

Second, the standard library and third-party modules available for Python are
breathtaking in their coverage. Almost every time a problem was encountered, a
Python library that helped speed the solution process was found. These
libraries, both standard and third-party, were high-quality and tended to have
helpful communities of users.

Finally, the ease with which code can be read and comprehended quickly, even
months after being written, has helped to keep LoveIntros' feature set growing
and maturing more quickly than any other project with which its developers
have been involved.

Python has been a major factor in the success of the LoveIntros software
project. It has proven to be a great choice, and LoveIntros' developers have
only happy experiences to relate regarding this excellent language.

About the Author
----------------

*Greg Unrein cofounded LoveIntros with his wife, Junel.  Greg holds a degree
in computer and information science from the University of Oregon. He has been
in the technology industry for almost a decade, with years of experience in
Java and C++, and he has found Python to be the best tool for creating a
superior dating site for Northwest singles.*