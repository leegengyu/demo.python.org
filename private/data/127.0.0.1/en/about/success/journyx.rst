**MISSING**
**MISSING**

Python Powers Journyx Timesheet
===============================

**MISSING**
**MISSING**
**Category:**  Software Development, Business

**Keywords:**  Product Development, Rapid Application Development, Cross-platform, Database, Project Management, ROI Case Study, Web2.0, Product Development, XML

**Title:**  Python Powers Journyx Timesheet

**Authors:**   Curt Finch and John Maddalozzo

**Date:**   2003/01/17 15:59:01

**Website:**  `http://www.journyx.com/ <http://www.journyx.com/>`_

**Summary:**  Journyx Timesheet is a commercial time, expense, and project tracking application. The application logic is implemented entirely in Python.  It is available for most major operating systems and hardware configurations.

**Logo:**  .. image:: /files/success/journyx/journyx-logo.gif    :alt: /files/success/journyx/journyx-logo.gif

Introduction
------------

`Journyx <http://www.journyx.com/>`_ Timesheet (tm) is a commercial application that provides time,
expense, and project tracking.  In 1996, Curt Finch, Journyx CEO and
founder, was working in the staffing industry when he saw an
opportunity to use the web to accurately collect and store employee
timesheet information.

.. image:: /files/success/journyx/te1-half.jpg
   :alt: Journyx Screen Shot

*Journyx Time Entry Screen* `Zoom in </files/success/journyx/te1.jpg>`_ 

The first version of Timesheet focused on collecting accurate cost
information, with an eye towards applying that data in the formulation
of new project cost projections. Since then, Timesheet has expanded
considerably to facilitate tracking of time, mileage, and expenses, not
just for project management but also for billing and payroll purposes.
Optional modules are available for paper-less expense reporting,
advanced user role management, automated billing and payroll, and to
facilitate system access for disconnected traveling users.

Today, Timesheet is platform-independent, flexible enough to be
reconfigured by customers to fit unique organizational needs, and
scales to tens of thousands of users for the large enterprise.

Python From the Start
---------------------

Journyx Timesheet has been using Python from the beginning. Curt Finch
chose Python initially on the recommendation of a friend, Steve Madere,
who had founded Dejanews.com (now a part of Google). Describing the
rationale for his choice, Curt said &quot;I looked at Java and C and came to
the conclusion that 1 line of Python is 10 lines of Java or 100 lines
of C. Developers write code at basically a constant rate so I chose
Python which was (and is) the highest level language I've ever seen
that is also flexible enough to be generally useful.&quot;

Architecture
------------

From the beginning, Timesheet was designed and implemented as a web
application. It uses a three-tiered web application architecture with
separate layers for web presentation, business logic, and data storage.
As time has progressed, the application's functionality has advanced
considerably, and Curt's decision to use Python for an implementation
language has proven to be good choice.

Python is currently used for all application logic in the Timesheet
application. This includes all code between the initial Apache
dispatch, where mod_python is employed to expedite interpreter
instantiation, though the application logic, and down to the point of
call out to the database transport layer.

Timesheet uses not only the Python standard library but also several
independently developed open source Python subsystems, such as PyXML
and ActZero's SOAP support. PyXML is used to implement certain business
rules and to develop jxAPI, which is a SOAP-based API into the
application logic. Work is in progress to extend this API to define Web
Services Description Language templates for the jxAPI functions. The
application currently builds and ships with Python 2.1.1.

Timesheet also incorporates several non-Python technologies. The Unix
and Linux distributions are packaged with the Apache HTTP server and
PostgreSQL database. The Timesheet distribution for Windows ships with
an optional Microsoft Desktop Engine (MSDE) database and integrates
with Microsoft IIS. Timesheet can be configured to use a variety of
third-party databases.

Results
-------

The Timesheet project has succeeded spectacularly, generating millions
in revenue and allowing Journyx to grow every year, even under the
current economic conditions.

Journyx, like many of our customers, uses Timesheet internally as a
mission critical part of the company infrastructure. It is used
extensively for project tracking, billing, and payroll.

To date, approximately 11 person-years have gone into the Journyx
Timesheet product, resulting in over one hundred fifty thousand lines
of Python code.

In developing Journyx, the two greatest benefits of Python were the
speed with which features could be written and deployed, and its true
write-once-run-anywhere cross-platform capabilities.

Journyx developers have found that the simplicity and clarity of Python
combine with its object-oriented properties to make it a very powerful
and productive language.  Python's rich standard library, which includes
modules for things like string manipulation and HTML generation,
further supports programmers in meeting aggressive development
schedules.

Because of these properties of the language, Python has enabled Journyx
to add features more quickly than our competitors. We've been able to
implement SOAP/XML and WSDL support and extended other aspects of
the application's functionality well ahead of competitive products. One of
the key enablers of this efficiency in maintenance and improvement is
the inherent clarity and readability of the Python language. Other
important factors are the vibrant and responsive Python development
community, and the high degree of backwards compatibility and stability
we have seen as the language design evolves over time.

Python's cross-platform standard library and platform-independent byte
code file format allow the deployment of Python modules to any
platform, regardless of which platform the module was prepared on. This
helped not only in avoiding per-platform development overhead but also
facilitates customer support for the Timesheet software product. For
example, a patch module built on a Redhat 6.2 system can be sent to a
customer for installation on Windows XP or any other operation system
without the need for cross-compilation or translation of any kind.

Conclusion
----------

Python made it possible for Journyx to produce a flexible, feature-rich
product for multiple platforms in less time than would have been
possible using another language. Python has been an important
competitive advantage for us, and even as our Python code base grows in
complexity and maturity, the natural advantages of Python enable us to
provide a high quality mission critical application at a competitively
low cost.

About the Authors
-----------------

*Curt Finch, Journyx founder and CEO, started the company in 1996 after
a successful career in the consulting industry participating in and
managing engagements with Fortune 100 companies such as Tivoli, IBM,
and Prudential Securities.*

*John Maddalozzo, Journyx V.P. of Engineering, joined Journyx in 1999
after a twelve year career in Unix kernel development at IBM's AIX
Engineering group.*