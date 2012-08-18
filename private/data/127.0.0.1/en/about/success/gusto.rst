**MISSING**
**MISSING**

Gusto! Chooses Python for Travel Social Network Transition
==========================================================

**MISSING**
**MISSING**
**Category:**  Business

**Keywords:**  python, travel, web services, database, social, network

**Title:**  Gusto! Chooses Python for Travel Social Network Transition

**Author:**   Michael Engelhart

**Contact:**   `mengelhart@gusto.com <mailto:mengelhart%40gusto.com>`_

**Date:**   2007/05/24 13:00:00

**Web site:**  `http://www.gusto.com/ <http://www.gusto.com/>`_

**Summary:**  Gusto! uses Python to transition its EZTrip.com online travel site into a travel oriented social networking site

**Logo:**  .. image:: /files/success/gusto/gusto_logoLG.gif    :alt: /files/success/gusto/gusto_logoLG.gif

Introduction
------------

`Gusto.com <http://www.gusto.com>`_ began as an online travel site
under the domain name EZTrip.com which catered to the traveler looking
to make online flight, hotel and car reservations.  As our customer base
grew we started seeing a need to allow our customers to report on their
journeys in the form of
travel reviews, blogs, sharing photos and other post trip needs.   While
we've continued to develop and improve our online booking engines and
related systems that communicate with large Global Distribution Systems
(`GDS <http://en.wikipedia.org/wiki/Computer_reservations_system>`_), as
well as directly to suppliers' Central Reservation Systems (CRS), we've
now developed a social network to support the growing travel consumer
generated content niche.

Booking Systems
---------------

Most `GDS <http://en.wikipedia.org/wiki/Computer_reservations_system>`_'s were built in the late 1960's and early 1970's and are
mainframe based `OLAP <http://en.wikipedia.org/wiki/OLAP>`_
systems that handle millions of transactions per
day. GDS's work incredibly well and are testament to the skill of the
early developers that built them, but they have severe limitations when
it comes to the data that can be entered into them, and the formats that
the data is allowed to take. Although some CRS's used by individual
suppliers are more modern, they inherit many of the limitations of the
GDS's as a result of their tight data-level integration with them.

This is a problem when using these systems in the context of a web-based
applications like `Gusto.com <http://www.gusto.com>`_. Also, GDS's are not relational systems and
lack a query language like
`SQL <http://www.w3schools.com/sql/sql_intro.asp>`_,
so queries are limited by the API
provided by its developers.

During the past 4 years our online processing systems have been
developed in Java because many of the GDS's provide a low level Java or
C API, and most of our developers have experience building
`J2EE <http://java.sun.com/javaee/index.jsp>`_
applications. While Java is a great language for building a large web
presence with persistent data, many aspects of our development would
quickly become unmanageable and prohibitively expensive using Java
alone. `Python <http://www.python.org>`_ and
`Jython <http://www.jython.org>`_ are used instead for many of the day
to day integration tasks and the large amount of data &quot;cleaning&quot; that
are required to provide customers with a user-friendly interface.

Green Screens
-------------

The travel industry is much like the financial industry in that &quot;screen
scraping&quot; is often required to integrate older systems that provide no
interface other than the textual screen interface used by its original
human users.

Screen scraping makes heavy use of text processing tools, regular
expressions, and string manipulation, all of which are built into Python
and are very easy to work with. Python also provides the ability to
communicate easily with other operating system processes, which made it
possible to leverage external tools like
`sed <http://www.gnu.org/software/sed>`_ and
`awk <http://www.gnu.org/software/gawk/manual/gawk.html>`_
for the processing
tasks This flexibility in choosing the right tool for the job was
critical to the rapid development of the custom screen scrapers needed
to interface to the very many unique travel supplier's systems.

`Gusto.com <http://www.gusto.com>`_ uses `Python <http://www.python.org>`_'s
`OO <http://en.wikipedia.org/wiki/Object-oriented_programming>`_ aspects
heavily and has built an
extensive class library that allows new developers to come up to speed
quickly when working on new `GDS <http://en.wikipedia.org/wiki/Computer_reservations_system>`_ data access tasks.

Text, Text, Text
----------------

Text processing is where `Python <http://www.python.org>`_ really shines for us. Almost all the
data handled at `Gusto.com <http://www.gusto.com>`_ is text-based. From screen scraping `GDS <http://en.wikipedia.org/wiki/Computer_reservations_system>`_ data
to data mining vendors' websites, Python tools munge text day in and day
out, and have yet to run into any problems with the language or it's
performance. For these tasks, Python is fast.

One of the tools currently being worked on is a localization system that
allows generation of localized versions of hotel property descriptions
without requiring human translators for every one of the 100,000 hotels
in the Gusto.com network. This tool will increase market size 10 fold,
and is a project that is coming along much faster than
anticipated. Python's text processing capabilities helped make it
possible to build a solution with much higher productivity per man hour
than would have been possible using Java as the development language.

Web Services To The Rescue
--------------------------

In the past year or so, the larger suppliers have been slowly rolling
out Web services for some of their products and services. These also
work seamlessly with our `Python <http://www.python.org>`_ code. The
`XML <http://www.xml.org>`_
processing tools in Python
are, like everything else included with Python, well thought out, spec
compliant, and powerful.

`Gusto.com <http://www.gusto.com>`_ often builds automated test suites in Python, in order to
validate a new supplier Web service before rolling it into its web
presence. Python's rapid development times and capacity for automating
this kind of testing makes it possible to quickly find and work around
bugs in the supplier's code, resulting in a more a robust web
application.

Social Network
--------------

Building a social network for travelers was not a trivial paradigm shift
for us.   We researched the current crop of social communities to try
and find a blend of features that would best suit our customer base.
During R&D we used `Python <http://www.python.org>`_'s rapid development capabilities extensively
to get an idea of which features were feasible within our development
timeline.  Python once again shined for us during this transition.
Large data sets had to be shuttled between systems during the creation
of our new database model and Python proved it's mettle by allowing
rapid development, testing and implementation of our back end systems.

Why Python?
-----------

The author originally came across `Python <http://www.python.org>`_ in 1999 while working on a
large Java-based website. Like many developers new to Python, the use of
indentation to indicate program structure was a stumbling block during
this initial contact and Python was not adopted for use with that
project. On second look, after actual experience with the language, the
language's indentation-defined structure became a virtue, an important
part of the overall power and simplicity of the language.

In addition to Python's clean design, the following factors make Python
a good choice for enterprise integration tasks, like those undertaken at
`Gusto.com <http://www.gusto.com>`_:

- OS Independence - The ability to develop code on one operating system, email it to a travel suppliers IT group, and have it work seamlessly on another operating system has been a godsend in deploying and maintaining the many components of Gusto.com.

- Database Integration - Python's database tools are top notch, allowing for quick and painless development of data mining tools in a matter of hours, rather than the days or weeks it would take in a language like Java.

- Batteries Included - Except for a few database libraries and domain-specific libraries developed in-house, almost everything needed by Gusto.com developers is included in the Python distribution. Nevertheless, Python has managed to avoid the bloat seen in many other languages.

- Community - The Python community is fantastic. The amount of online technical information available for Python is vast. A good internet search engine will almost always find the answers a developer needs, any time of the day or night. In those cases where Gusto.com developers have had questions not answered by a web search, for example about the LDAP library or a database library, the developers of those projects have always been willing to provide an answer quickly. This has been invaluable as a time saver, and in keeping development costs down.

- `Jython <http://www.jython.org>`_ - Jython is an implementation of Python that is written in Java and runs on the Java Virtual Machine. It provides a powerful tool for scripting Java, and a more productive way to develop components for use in a Java system. For Gusto.com, Jython has bridged the gap between the front-end Java-based web systems and the back-end Python tools that do much of the heavy lifting.

Newbies
-------

One unexpected bonus discovered in the 4 years `Gusto.com <http://www.gusto.com>`_ has been using
`Python <http://www.python.org>`_ is its support for new developers and interns, and its ability to
make existing code more approachable and maintainable. Python has
exhibited an uncanny ability to teach and encourage good coding skills,
enabling developers to write clear and concise code. Python is very well
designed, and this quality tends to transfer into the software that is
written with it.

Summary
-------

`Python <http://www.python.org>`_ has helped `Gusto.com <http://www.gusto.com>`_ in countless ways. It has reduced costs by
speeding development time, improved integration with myriad suppliers,
provided a solid backbone to the behind-the-scenes development that
continues to strengthen Gusto.com, and made it possible to meet the many
goals faced as the business has grown. Without Python, Gusto.com would
not be as successful in the online travel space as it has been in such a
short period of time.

About the Author
----------------

Michael Engelhart is the CTO and lead software engineer for
Gusto.com. He previously worked at Apple computer as senior software
engineer for worldwide corporate travel, and has been a travel
technology consultant to several major travel industry suppliers over
the past 10 years.