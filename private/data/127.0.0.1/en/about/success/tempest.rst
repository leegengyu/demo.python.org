**MISSING**
**MISSING**

Integration of Legacy Monitoring Systems into a Central Management Console
==========================================================================

**MISSING**
**MISSING**
**Category:**  Business

**Keywords:**  Monitoring, Management, Integration, Python on Windows

**Title:**  Integration of Legacy Monitoring Systems into a Central Management Console

**Author:**   Tom Olexa

**Contact:**   `Tomas_Olexa@tempest.sk <mailto:Tomas_Olexa%40tempest.sk>`_

**Date:**   2009/05/15 11:23:00

**Website:**  `http://www.tempest.eu/ <http://www.tempest.eu/>`_

**Summary:**  Tempest uses Python for integrating proprietary monitoring solutions into a central management console.

**Logo:**  .. image:: /files/success/tempest/tempest-logo.png    :alt: /files/success/tempest/tempest-logo.png

Introduction
------------

`TEMPEST <http://www.tempest.eu/>`_, a.s. is one of leading system integrators
in Slovakia and surrounding countries.

TEMPEST has long-term experience in the area of IT service management (ITSM).
ITSM is aimed at fulfilling strategic business objectives in order to allow
flexible reaction to market demand, to connect the IT capabilities with the
business needs, and to enable planning, management and measurement of the
quality of IT services.

Many large organizations have different technological systems on which their
enterprises run or depend. If there are more than a few devices, they need to
be monitored. Usually, each group of technology and/or vendor-related devices
comes with its own monitoring solution.

Purpose of the Project
----------------------

In this project, a major telco company had eight proprietary monitoring
systems, each for a group of devices. These included radio data links, signal
coders and decoders, radio transmitters and other support systems.

The goal of this project was to collect events from these legacy monitoring
systems into an umbrella management console, which could display their data
and also some inter-dependencies among systems. The primary purpose was to
relieve operators from watching many different systems and, to a certain
extent, provide a correlation between these systems.

Analysis and Solution
---------------------

The solution's central console was HP OpenView Operations (OVO). OVO works as
an agent/manager solution, where agents intercept events from the environment
and the manager processes, stores, and provides the events to operator
consoles.

The OVO manager (or OVO server) was deployed on an HP-UX system. OVO agents
were deployed to each of the legacy platforms, most of which were Windows
systems, one of which was an older Digital UNIX, and one of which was an even
older MS-DOS based solution.

Each of the legacy systems consisted of monitoring software ranging from one
to three layers, with one of them being a database or flat file of events.
Each of these systems used a very different event logic, event format, and
event storage technology.

Python Comes to the Scene
-------------------------

The challenge we faced was to extract the events from each legacy system,
transform them to a common format and send them to the OVO manager. For this,
we felt we needed a powerful scripting language for the OVO agents on the
legacy platforms, one that would facilitate easy deployment and debugging of
the scripts there.

Another requirement was that event processing needed to be easily configurable
and extensible. Neither the customer nor the implementor could manually
configure handling of each specific event type. A configuration tool for
filtering and altering messages was needed, and had to be simple enough for
the customer to understand and use.

It was clear that a unified approach to integration was needed. Python was
chosen for it's flexibility, clarity, and native object-oriented (OO)
programming style.  Perl was also considered but we felt it would lead to
code readability and understandability issues at later times.  While
easy to write, Perl code often appears very cryptic when read.

A common Python module was developed, with a few common classes that are used
on all the OVO agent platforms. Most of the platform-specific customization
was accomplished in the class initialization. In some cases, some methods
needed to be overridden as well. On most platforms only two Python files were
needed.

With IDLE and CVS, development was easy and convenient.

Functionality of Integration Modules
------------------------------------

The integration module is first initialized according to the underlying data
source. This is an ODBC data source in most cases, although one platform
uses flat files. The ODBC data sources include many database formats. One special
case with flat files uses a Perl parser as client and the common Python module
with a network extension as server.

Next, the module periodically reads new events from the data source. Each event
needs to be filtered to determine whether it should be sent at all and, if
so, translated into human-readable form. Finally, the event is sent through a
common command line interface, OVO agent's ``opcmsg`` command. OVO agents have
the ability to further modify an event's properties (e.g. provide automatic
alarm closure).

Event filtering and translation is controlled through configuration files,
which are read in automatically both at start and whenever they are
modified. Their purpose is to transform event input fields to output fields
or apply rules to transform the event (e.g. drop the event, enrich the event,
and so forth). These configuration files have table-like structure and simple
syntax, so they are easily readable and comprehensible. Each platform has
a different number and format of these files. The files are maintained by the
customer.

Conclusion
----------

A powerful yet clear multi-platform scripting language was needed to achieve
this project's goal.  Python fulfilled this requirement.

With good code reuse -- some 40KB of code in the common module, 5-10 KB of
initialization code -- a lot of programming time was saved. Taking into
account that each platform is very different, this was a very pleasant result.
The majority of the work that had to be done was analysis and testing, not
programming.

The modules described here have been running for almost 2 years now without
serious issues. The code is still easy to understand and easy to tailor for a
new platform or to add a new feature.

Developing integration code with Python is fast and easy. Python's native OO
approach -- something that was not available in our older integration
languages -- made it easy to create reusable code with minimal effort. This
project has shown the great power of Python and open source tools in general.

About the Author
----------------

*Tom Olexa is an ICT consultant at TEMPEST, Slovakia.*