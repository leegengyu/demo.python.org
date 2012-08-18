**MISSING**
**MISSING**

The Devil Framework: A Python-based Distributed System For Technology Integration
=================================================================================

**MISSING**
**MISSING**
**Category:**  Business

**Keywords:**  cpython, programming, process, integration

**Title:**  The Devil Framework: A Python-based Distributed System For Technology Integration

**Author:**   Alessandro Iob

**Date:**   2007/03/26 20:21:00

**Web Site:**  `http://www.dlevel.com/ <http://www.dlevel.com/>`_

**Summary:**  D-Level finds Python delivers an order-of-magnitude productivity increase in their development of a platform for distributed technology integration.

**Logo:**  .. image:: /files/success/devil/dlevel-logo.png    :alt: /files/success/devil/dlevel-logo.png

Introduction
------------

The `Devil Framework <http://www.dlevel.com>`_ is a multi-platform (Linux, OS X, Windows),
multi-user, multi-tier, distributed  platform for developing process and
technology integration solutions: developers can easily collect,
integrate, correlate, control and visualize all information produced and
consumed by heterogeneous networked hardware and software technologies.

The project started in 1999 as a network security data integration
system, but when we &quot;discovered&quot; that security is just another process,
it evolved to a more general infrastructure for process management.

We are now using it for implementing business/plant integration
solutions for business groups (manufacturing, distribution, etc.) with
production/business units distributed all over the country.

We are on the way of releasing it as an open-source product with
non-commercial and commercial licenses.

Architecture
------------

The Devil Framework system is composed of two different applications:
the Application Server components and the IceBridge graphical
console. Both are multi-platform applications completely written in
Python: the server runs on Linux and Windows platforms (and can be
easily ported to other Unix systems), the client runs on Linux, Windows
and Mac OS X.

Application Server Components
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

The Applications Server components are the core of the application
development and supervisory control platform for the Devil Framework
product line. They provide a unified environment for data collection,
data historization, communication, process automation and applications
deployment and integration.

.. image:: /files/success/devil/devil-component.png
   :alt: Application Server component architecture

*Application Server component architecture* `Zoom in 
</files/success/devil/devil-component.png>`_

A component is designed as a plugins-based system. Plugins can be added,
removed and updated at run-time, manually or through scheduled
policies. Different policies are supported so a component can change
functionalities and configurations at scheduled times. Every
functionality of a component is implemented via plugins.

Components are designed to work as a tree-like networked structure, with
one master node (MCP) where all configuration and plugins installation
and updates are performed. All other nodes (Collectors and Agents)
automatically get proper configuration and software updates.  New nodes
can be added at any time to scale data processing, reach new geographic
zones or to connect to new devices.

.. image:: /files/success/devil/devil-nettree.png
   :alt: Tree-like distributed system topology

*Tree-like distributed system topology* `Zoom in 
</files/success/devil/devil-nettree.png>`_

Components are designed to work on insecure, unreliable and
not-always-connected communication channels. All communication is
encrypted (using the `pycrypto <http://www.amk.ca/python/code/crypto.html>`_ module) and authenticated through an
internal PKI infrastructure (all nodes have their `PKI <http://en.wikipedia.org/wiki/Public_key_infrastructure>`_ certificates). A
store and forward  mechanism is used either for the configuration and
code propagation systems either for events transmission. Connections can
be initiated from any component: parents can call children, and children
can call their parent (connections can activated at scheduled times,
when specified events occur or when special conditions are detected).

The Application Framework creates a distributed environment where all
nodes, from a programming and operative point of view, are seen as an
unique system exposing a single API. Operations can be performed on any
child node from any parent node, transparently.

IceBridge Graphical Console
~~~~~~~~~~~~~~~~~~~~~~~~~~~

The `IceBridge <#icebridge>`_ console is a multi-platform application written in Python
(using the `QT <http://www.trolltech.com/products/qt>`_/`PyQT <http://www.riverbankcomputing.co.uk/pyqt/index.php>`_ toolkit/wrapper for the user interface) that
provides all tools needed for development, configuration, management and
interactive use of the Application Server system.

Like the Application Server's components, the console is a plugins-based
system. Plugins are dynamically downloaded from the server when needed
or when new versions are available. No user or administrator
intervention is needed. Plugins can add, change, augment or hide any
console functionality, providing  a complete per-user customizable
experience.

A complete configuration and visual development environment is
integrated into the console (including a version control system for
Views and an interactive remote Python shell). Visualization and control
forms (called Views) can be added, modified and tested in real-time. New
view components (Widgets) can dynamically be made available by plugins.

.. image:: /files/success/devil/devil-config.png
   :alt: Real-time system configuration and interface design with "live" widgets

*Real-time system configuration and interface design with &quot;live&quot;
widgets* `Zoom in </files/success/devil/devil-config.png>`_

Process specific widgets, views, windows and applications can be easily
developed and deployed. The system is ready for internationalization;
multiple languages are supported and every user can use its preferred
language. Moreover, a translation tool (inspired by the
`QT Linguist Tool <http://www.trolltech.com/products/qt/features/internationalization>`_) and a `WikiWiki <http://en.wikipedia.org/wiki/Wiki>`_-like documentation editing and
viewing tool are integrated into the system.

.. image:: /files/success/devil/devil-control.png
   :alt: Real-time system configuration and interface design with "live" widgets

*Control view with a custom 3D visualization widget running on Linux and KDE*
`Zoom in </files/success/devil/devil-control.png>`_

Why Python?
-----------

Python was not our first choice as the main programming language it was
a coincidence. When we started our project we was very proficient in
Perl and completely unaware of Python: so we chose Perl.

We discovered Python when we decided that we had to substitute the
`PerlTK <http://www.perltk.org/>`_ user interface with a Web-based one. We found `Zope <http://www.zope.org/>`_, and after
some attempts to integrate `Perl <http://www.perl.org/>`_ with `Zope <http://www.zope.org/>`_, we switched to Python. To
make a log story short, at the end we dropped `Zope <http://www.zope.org/>`_ but kept using
Python (and rewrote the whole `Devil Framework <http://www.dlevel.com>`_ with it).

Without this fortunate switch we think the `Devil Framework <http://www.dlevel.com>`_ would not
be possible to be developed, at least for a team of only two developers.

Project Statistics
------------------

The `SLOCCount <http://www.dwheeler.com/sloccount/>`_ output says it all: 

.. code-block::

    Totals grouped by language (dominant language first):
    python:      233020 (97.72%)
    ansic:         2480 (1.04%)
    cpp:           1833 (0.77%)
    makefile:       571 (0.24%)
    sh:             560 (0.23%)

    Total Physical Source Lines of Code (SLOC)                = 238,464

    Development Effort Estimate, Person-Years (Person-Months) = 62.71 (752.50)
     (Basic COCOMO model, Person-Months = 2.4 * (KSLOC**1.05))

    Schedule Estimate, Years (Months)                         = 2.58 (30.98)
     (Basic COCOMO model, Months = 2.5 * (person-months**0.38))

    Estimated Average Number of Developers (Effort/Schedule)  = 24.29

    Total Estimated Cost to Develop                           = $ 8,471,018
     (average salary = $56,286/year, overhead = 2.40).

    SLOCCount, Copyright (C) 2001-2004 David A. Wheeler
    Please credit this data as &quot;generated using David A. Wheeler's 'SLOCCount'.&quot;

On the Persons-Years side, it took us four years for two developers to
develop the 2.0 version from scratch (version 1.x was in production use
but never released).

Results
-------

As said before, we think that this project would not be possible without
the adoption of Python as the main development language, either because
of its powerful features either because it was instrumental in the
adoption of libraries like `PyQT <http://www.riverbankcomputing.co.uk/pyqt/index.php>`_ (after having tried to use `PerlTK <http://www.perltk.org/>`_, `Web <http://www.zope.org/>`_,
`wxPython <http://www.wxpython.org>`_), `pycrypto <http://www.amk.ca/python/code/crypto.html>`_ and others that let us build a reliable and portable
system in a relative small time lapse.

Productivity
~~~~~~~~~~~~

Python is our &quot;secret weapon&quot;. It gives us order-of-magnitude increases
in productivity thanks to:

- Simple syntax and clear coding style: it effortlessly forced us to use a consistent and expressive coding style. Now it's easy to look at a piece of code and understand at a glance how it works (nearly impossible with the first Perl version).

- Rapid development cycle: Python removed the tedious and long code/build/run/crash development cycle.

- It allowed us to development one of the hottest features of our system: when we upgrade or install some new code into the system, it dynamically updates itself, either the client and the server. Imagine this: with a simple double-click you install a plugin on the central server, update it (propagating the changes to all the nodes of the system that are using it), run it, download its client stuff into the console and make it active (dynamically updating the GUI). Everything without restarting nor the server nor the client.

- Extensive and complete standard library and great external modules.

- And when there's no standard library or external module, it's really easy to build wrappers around a third-party library (especially with the ctypes module)

- Easy and fast code refactoring: we have some old code that gets updated all the time.

Cross-platform Development
~~~~~~~~~~~~~~~~~~~~~~~~~~

Porting our application to the different supported platforms was really
simple thanks to the great portability of both Python and `PyQT <http://www.riverbankcomputing.co.uk/pyqt/index.php>`_ and most
of the external modules we used in the project. The only real problems
we had were caused from platform specific modules (mostly on Window) and
from the development of the installation systems (Windows again).

GUI Development
~~~~~~~~~~~~~~~

The choice of the `PyQT <http://www.riverbankcomputing.co.uk/pyqt/index.php>`_/`QT <http://www.trolltech.com/products/qt>`_ toolkit was fundamental for the development
of the client side application. We extensively used other toolkits (`Tk <http://www.tcl.tk/>`_
and `wxPython <http://www.wxpython.org>`_) before approaching `PyQT <http://www.riverbankcomputing.co.uk/pyqt/index.php>`_.  No toolkit can compare with its
easy of use, power, stability and portability.

As an example, the Mac OS X port of the `IceBridge <#icebridge>`_ console was possible
in less than a week, with most of the time spent in learning how to
correctly build the single packages from source and configure the
packaging system.

.. image:: /files/success/devil/devil-console.png
   :alt: The IceBridge console running under Mac OS X

*The IceBridge console running under Mac OS X* `Zoom in 
</files/success/devil/devil-console.png>`_

Speed, Scalability and Stability
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

One of our concerns was the speed of our system. Python proved to be
&quot;fast enough&quot; for our uses as the most processor-intensive stuff is
already written in C (GUI toolkit, GUID generators, numeric
manipulations, etc.). We only had to write, in Python, our custom RPC
protocol, because `XML-RPC <http://www.xmlrpc.com/>`_ (and it's Python implementation) proved to be
too slow and processor-intensive.

Scalability was an issue that we solved at design time, but Python let
us create programming constructs like the transparent distributed RPC
system and extensible API system.

In regard to stability, we think that Python's great exception handling
mechanism gave us an enormous advantage. Our coding errors almost never
stop the application and are just about always recoverable.

Real-life Applications
~~~~~~~~~~~~~~~~~~~~~~

Some sample scenarios where we used the Devil Framework are: 

- Management and control of all the technology systems for large-scale retailers from the local stores and the head offices (air-conditioning systems, power consumption control and reduction, data analysis, etc).

- Interface and integration of production systems and accounting systems for manufacturing groups with different production plants and business units located all over Europe (real-time price simulation, live production data analysis and visualization, automated anomaly detection and response, data correlation, etc.).

- Management and control of  remote environmental monitoring units (GPS connections, automatic update and reconfiguration of the units, data normalization and analysis, etc.)

Quirks
------

We had only minor quirks with the Python language itself, only one of
which had a real impact on our projects:

- Thread management. We know threads are evil, but sometimes they are invaluable. Not having a way to kill them was something difficult to accept.

- Floating point representation inconsistency between Windows and the rest of the world. We had to perform some nasty tricks to circumvent (partially) this inconsistency.

Conclusion
----------

After so much developing time and so many lines of code we can say
without hesitation: *&quot;Hail Python, we believe in you!&quot;*

It was, and it is still, a pleasure to develop in a such a friendly and
powerful language.

About the Author
----------------

Alessandro Iob is the CEO and co-founder of `D-Level <http://www.dlevel.com>`_ s.r.l., makers of
the Devil Framework. He was a C fervent believer before encountering the
beauties of Python. You can find some more info about him and the Devil
Framework development at `his blog <http://www.dlevel.com/blogs/alex>`_.