**MISSING**
**MISSING**

ERP5: Mission-critical ERP/CRM with Python and Zope
===================================================

**MISSING**
**MISSING**
**Category:**  Business, Software Development, Government

**Keywords:**  Web2.0, XML, Ecommerce, Administration, Business Information, Relational Online Analytical Processing (ROLAP)

**Title:**  ERP5: Mission-critical ERP/CRM with Python and Zope

**Author:**   Dr. Jean-Paul Smets

**Date:**   2004-06-02

**Website:**  `http://www.nexedi.com/ <http://www.nexedi.com/>`_

**Summary:**  Nexedi uses Python and Zope for super-efficient development of applications in Enterprise Resource Planning (ERP) and Customer Relationship Management (CRM).

**Logo:**  .. image:: /files/success/nexedi/nexedi-logo.gif    :alt: /files/success/nexedi/nexedi-logo.gif

Introduction
------------

`Nexedi <http://www.nexedi.com/>`_ is a leader in high-end enterprise services, providing solutions for
Enterprise Resource Planning (ERP), Customer Relationship Management (CRM),
and eCommerce. Nexedi has built its business on Open Source, and has designed
and released an ERP/CRM framework called `ERP5 <http://www.erp5.org/>`_ under the GPL Free Software
license.

ERP5 is in production in the apparel industry and government agencies with
multi-gigabyte databases that track millions of warehouse stock movements.
ERP5 is written entirely in Python and leverages the `Zope <http://www.zope.org/>`_ Enterprise Objects
framework to provide high performance and availability on clusters of
inexpensive PCs.

Background
----------

The ERP5 project started in 2002 when Coramy, an apparel industry leader in
Europe, decided to migrate its in-house ERP solution to a new open source
model. The choice of open source for Coramy ERP was a strategic move to reduce
software maintenance costs and to allow Coramy to retain complete control over
its custom developments, something that would have been impossible with
standard proprietary ERP solutions.

Nexedi was created as an independent company in charge of
developing, implementing, and disseminating the ERP5 technology. Nexedi was
given a budget of 80,000 EUR to develop a generic ERP framework published
under GPL license and customize it for Coramy's specific needs.

Python: Clean Objects from Scripting to Metaprogramming
-------------------------------------------------------

Working with this small budget, ERP5's developers needed to look to innovative
approaches and code reuse to cut development costs.  At the most abstract
level, ERP5 is based on five generic classes used by all modules: Resource,
Node, Movement, Item, and Path. This model, known as the ERP5 Universal
Business Model, makes it possible to reuse code by abstracting away from the
specific domain and encapsulating the generic relationships and actions common
to many business processes. As a result, modules as different as Payroll and
Invoice can share almost of all their code.

.. image:: /files/success/nexedi/technology-hires-web.png
   :alt: ERP5 Universal Business Model Example

*In this example of the ERP5 Universal Business Model, Movement allows the
transfer of a quantity of resource from one node to another, Path allows
planning of resource sourcing, and Item provides Resource traceability.*
`Zoom in </files/success/nexedi/technology-hires.png>`_

The ERP5 abstract model architecture requires a well-designed object language
that supports high level abstraction. Selecting an appropriate implementation
language became strategic to the project's success. The project also required
complete multi-platform OS abstraction, a rich library for Web applications, a
rapid GUI development toolkit, support for internationalization, wide
community support, and proven maturity. The short list of candidates quickly
became: Java or Python. Or, more precisely, Java+Jakarta or Python+Zope.

Two key factors led to the choice of Python. First, was the need to make
extensive use of metaprogramming. Second, for simplicity's sake, ERP5 needed
to be implemented in a single language from core architecture to scripting.

Metaprogramming is a technique that allows the programmer to redefine the
semantics of the implementation language at runtime. It can be used to endow
extremely abstract implementations with domain-specific behaviors that are
modeled in properties or tables, rather than hand-coded. In ERP5, this
powerful technique allows 95% of the class methods to be generated
automatically from lists of properties that define each unique custom ERP
implementation. This has reduced maintenance costs by an order of magnitude:
The typical ERP5 system contains 100,000 lines of code, rather than the
1,000,000 lines of code required in similar projects based on traditional
programming techniques.

Python supports efficient metaprogramming through powerful introspection
features that allow programs to inspect and modify code at runtime. Java's
introspection are by contrast quite poor and inflexible. Metaprogramming in
Java requires writing preprocessors, which would have added prohibitively to
the cost and complexity of implementing the ERP5 system.

Another advantage that Python had over Java was that it could be used at all
levels of the system, from core implementation to scripting. Most ERP systems,
while written in one language, use another scripting language to allow
flexible configuration at run time by ERP administrators. Python is equally
well suited both for scripting and core development, reducing complexity and
increasing the flexibility of the system. Using Python allowed code initially
written as scripts to be incorporated afterward into core components, and vice
versa, wherever this made sense. With Java, it would have been necessary to
provide a separate scripting environment based on a different language, such
as `Jython <http://www.jython.org/>`_ or ECMAScript, and reusing scripting code in core components would
have been much more difficult.

Enterprise Objects with Zope
----------------------------

In addition to leveraging these high-level language capabilities, the ERP5
project also needed to base on an existing turn-key application server with
support for transparent object persistence, transactions, and workflow. This
would allow the project to focus its limited resources on application design,
rather than on application server design.

`Zope <http://www.zope.org/>`_, a Python-based application server, fulfilled this need. In 2002, Zope
was already a mature application server environment while Jakarta was still
rather immature. Zope provided clustering, object storage, object publication,
transactions, security, workflows, and a web-based management interface, all
in a turn-key package. Zope and Python, unlike Java, also provided the
licensing needed for complete freedom in distributing code on LiveCD, in RPM
packages, and so forth.

In some applications needed in ERP, such as in Point-of-Sales (POS), an
autonomous client/server GUI application provides better results than a pure
Web-based solution. For these cases, the ERP5 project team selected `PyQt <http://www.riverbankcomputing.co.uk/pyqt/index.php>`_,
which supports the rapid development of multi-platform client/server
applications with native look and feel. Autonomous applications written in
PyQt could interoperate with Zope through the `XML-RPC <http://www.xmlrpc.com/>`_ and `SOAP <http://www.w3.org/TR/soap/>`_
implementations available for Python.

ZSQLCatalog: Querying and ROLAP of Zope Object Database
-------------------------------------------------------

In January 2003, the initial ERP5 modules went into production at the Coramy
factory and design center.

The ERP5 architecture relies completely on Zope for data storage, transactions
and workflow management. The user interface is based on an extended version of
Martijn Faassen's `Formulator <http://www.zope.org/Members/infrae/Formulator>`_ component. ERP5 itself is implemented as a set
of Zope components. Overall, thanks to massive code reuse and fast coding,
ERP5's initial development was completed in less than one year. The choice of
Python and Zope proved to be a good one.

Part of this success was due to Nexedi's `ZSQLCatalog <http://www.erp5.org/workspaces/project/zsqlcatalog/>`_ component which
leverages Zope's object database to implement an innovative approach for
querying objects and data mining.

ZSQLCatalog solves several major problems often encountered in Enterprise
applications: locks, slow reports, and inconsistent transactions. Most
Enterprise applications use tables in a relational database to store data. In
ERP5 data is stored instead in Zope's object database. Zope eliminates the
need for storage adapters or attribute mappings by providing transparent
persistence of Python objects. Zope also speeds up object access: Reading the
Zope object database is 10 to 100 times faster than retrieving a row from the
fastest relational databases available on the market today. Finally, unlike
relational databases, transactions in a Zope object database can last minutes
without causing deadlocks.

One limitation encountered in Zope was that it does not provide an efficient
tool for querying the millions of objects that are needed in an ERP solution.
To solve this, Nexedi's ZSQLCatalog maps between attributes or methods of
objects and relational columns, tables, and databases. This mapping is not
intended to store actual object attributes into relational tables, but rather
only those attributes relevant to facilitating fast queries. In this way, the
relational database is used as an index into the Zope object database.

.. image:: /files/success/nexedi/odb-web.png
   :alt: ZSQLCatalog

*To provide support for fast queries of the object database, ZSQLCatalog
copies select attributes (dots) and relations (lines) from the object database
into tables of a relational database.* `Zoom in </files/success/nexedi/odb.png>`_

ZSQLCatalog can be viewed as a kind of Relational Online Analytical Processing
(ROLAP) component for object databases, and it provides a nice interface for
extracting reports from the object database into OpenOffice or Microsoft Excel
spreadsheets.

ZSQLCatalog was very successful in this project: a Zope database with more
than 2,000,000 objects can be queried with statistical methods in a few
milliseconds.

ERP5SyncML: Synchronized Distributed Objects
--------------------------------------------

Coramy's requirements for ERP5 included the need to deploy applications in its
factories in Tunisia. This posed some additional challenges, since internet
connectivity between Africa and Europe is not always perfect and can be very
expensive. Given Coramy's modest budget for network connectivity, the project
had to provide a solution for synchronizing two ERP5 servers over slow and
unreliable transcontinental internet connectivity.

To do this, Nexedi implemented the `SyncML <http://www.openmobilealliance.org/tech/affiliates/syncml/syncmlindex.html>`_ protocol in Zope, using email or
http as the transport layer. Early prototypes were developed in a few weeks,
using Python's rich library for network protocols and XML parsing.

Turning those prototypes into an industrial-strength solution turned out to be
a bit more complex, due to the many possible failure cases the code had to
handle. Nexedi used Python's unit testing framework to write extensive tests
of the SyncML implementation. These tests could test every part of the SyncML
component, especially those that would be difficult to test in the field, and
report any problems back to the developer. Once this was done, the ERP5SyncML
component became reliable. In the process of testing, some minor bugs occurring
in complex situations were found in the Python libraries. Because Python is
open source, the ERP5 developers could find and fix the bugs quickly and
contribute the fixes back to the Python community.

ERP5SyncML is now being used not only by ERP5 but was also adopted by
the Nuxeo CPS, a Content Management System, as a way to
synchronize documents between French government agencies.

Python-GLPK: Linear Programming in Python
-----------------------------------------

Some aspects of an ERP system's database query functionality require
mathematics that go beyond the capabilities of the relational query model. For
example, ERP5 uses linear programming to determine resource capacities.
Although Python includes excellent numerical frameworks, C or FORTRAN
implementation of complex scientific algorithms is usually much more
efficient.

Nexedi found the `GNU Linear Programming Kit <http://www.gnu.org/software/glpk/glpk.html>`_ (GLPK) to be a good starting
point for ERP5's linear programming needs. GPLK is written in C, and
interfacing it to Python was achieved in only a couple of hours using
the `SWIG <http://www.swig.org/>`_ glue libraries. Nexedi now distributes a Python GLPK module,
python-glpk, which provides the power of linear programming in Python.

Conclusion
----------

The ERP5 abstract model has been found to reduce development costs by an order
of magnitude when compared to traditional ERP architectures, and it has
performed well in large mission-critical Enterprise applications. ERP5's
largest system runs on a cluster of eight CPUs. It serves fifty simultaneous
users, each of them with eight parallel sessions, and it handles more than
2,000,000 Python objects. Its ZSQLCatalog relational index holds more than
10,000,000 rows.

Python and Zope were key to this success. Python provided a powerful object
language and a rich set of libraries which allowed quick development of clean
and compact code. Zope provided a mature application server and object
database.

Nexedi is sometimes asked: Why not Java and J2EE? While it would be possible
to create a similar system with Java and J2EE, development costs would be much
higher. Jakarta and ObjectWeb have both matured but are still poorly
integrated when compared with Zope, and require a much more complex
development style. Java's poor introspection features are also still a serious
limitation for efficient metaprogramming, for using Java itself as a scripting
language, or for flexible object persistence. Using Java is simply not
consistent with today's trend of cost cutting in Enterprise development. If
the choice were made again today, Nexedi would still opt for Python and Zope.

In June 2004, ERP5 was nominated for &quot;best enterprise project&quot; by Decision
Informatique professional magazine. Nexedi is now working to simplify the
ERP5 setup and configuration process, in order to ease its adoption by a wider
audience of open source developers.

About the Author
----------------

*Dr. Jean-Paul Smets is CEO of Nexedi. Nexedi develops ERP5, a high end ERP /
CRM / eCommerce solution based on Zope application server and published under
Open Source / Free Software licenses. Nexedi provides complete enterprise
consulting, software development and professional training services for ERP5.
Nexedi clients include the apparel industry, consumer electronics industry,
telecommunication companies, and government agencies.*