**MISSING**
**MISSING**

Python is Rackspace's CORE Technology
=====================================

**MISSING**
**MISSING**
**Category:**  Business, Software Development

**Keywords:**  Enterprise Resource Planning (ERP), Hosting, Reuse

**Title:**  Python is Rackspace's CORE Technology

**Author:**   Nick Borko

**Date:**   2003/01/17 15:59:01

**Web site:**  `http://www.rackspace.com/ <http://www.rackspace.com/>`_

**Logo:**  .. image:: /files/success/rackspace/rackspace-logo-trans.gif    :alt: /files/success/rackspace/rackspace-logo-trans.gif

**Summary:**  Rackspace, the industry leader in Managed Hosting, uses Python to implement its enterprise data systems and to achieve true object reuse.

Introduction
------------

To be the industry leader in Managed Hosting, you have to be fast and
flexible. By using Python to implement our enterprise data systems,
`Rackspace <http://www.rackspace.com/>`_ can quickly and effectively change its internal systems to
keep up with shifts in the industry and in our own business processes.
We do this through a central customer information system called &quot;CORE,&quot;
which is used both for Customer Relationship Management (CRM) and
Enterprise Resource Planning (ERP). Python and CORE are key factors
that enable Rackspace to provide our Fanatical Support(tm) and faster
customer service.

Background
----------

Rackspace's central customer database started as a simple ERP system to
provision and track managed servers. It began humbly, as a small
collection of PHP pages that did the job nicely for the few hundred
servers that was the beginning of Rackspace's customer base.

As Rackspace grew, that small PHP system became the center of business
at Rackspace. Every time an opportunity to automate a process presented
itself, it was rolled into that system.

After a couple of years, the result was a big, un-maintainable mess of
thousands of PHP pages and modules that had been written and maintained
primarily by one person. The limits of PHP (then version 3) had been
stretched thin, the system was too much for one person to maintain,
and it was difficult to bring in new people to help with it.

.. image:: /files/success/rackspace/datacenter-web.jpg
   :alt: View of Rackspace Managed Hosting Data Center

*Rackspace Managed Hosting provides customized servers in state-of-the-art
data centers* `Zoom in </files/success/rackspace/datacenter.jpg>`_

Our first attempt to update the system came when PHP version 4 was
released. This release promised better object oriented capabilities,
and the time was right for Rackspace to dedicate more people to the
project.

The system was totally redesigned from the ground up, including new
database schemas and application design strategies. At this time we
re-dubbed the project &quot;CORE,&quot; an acronym for Core Objects Reused
Everywhere, in order to reflect the overall design goal for CORE:
modularity and reusability across all systems in the company. With that
goal in mind, our team went to work using the object oriented features
of PHP.

While we were able to re-fit the application and add increased
functionality, the project ultimately failed due in large part to the
problems encountered while using the object framework provided by PHP.

Memory leaks, inconsistent interfaces, inconsistent internal data model,
randomly freed objects, multiple object copies despite explicit use of
references, internal PHP errors, and untraceable code failures all but
made the task impossible to accomplish in PHP.

Even after we achieved a relatively stable code base, we were nowhere
near our goal of Core Objects Reused Everywhere because we had to
depart from pure object-oriented methods just to work around the
problems inherent in PHP. It became clear that PHP was unsuitable for
our large scale, mission critical projects. A new solution had to be
found.

Python in CORE
--------------

We had always considered Python to be an excellent candidate for
implementing our enterprise system, but it was initially passed over in
favor of building upon the existing (vast) code base we already had in
PHP. At that time, we felt that PHP could be used successfully in CORE
by introducing a better structured system design.

Unfortunately, that wasn't enough to overcome our other problems with
PHP, so we re-evaluated our situation. The first alpha version of Python
2.2 had recently been released, and we decided to begin work on a new
CORE framework using the new features that were available in that
version.

The Power of Introspection
--------------------------

One of the first tasks in writing the new framework was to build
its database interface.

Python's introspection model had been significantly enhanced with the
release of Python 2.2. We decided to use it to build a generic database
interface class based on a DBI 2.0 compliant database connector. In this
approach, rather than writing queries or table-specific wrappers by
hand, a meta-class abstracts all database queries into a single clean
API.

We create descendents of this meta-class to make an API for each table.
Each table's class contains a few class constants that describe the
columns in the database. This way we can add new tables to the overall API
quickly and simply without having to worry about implementation
details for any specific table.

The API also uses meta-data to automatically validate and convert values
passed to the database. This is done by a &quot;normalizer&quot; function that
converts the Python data types being passed through the API into valid SQL
values.  The function also verifies types and formats that are not
necessarily checked by the database or by Python, such as phone numbers
and ZIP codes.

Reusing Objects Everywhere
--------------------------

Once the database API was complete, we created a second layer of classes
on top of it. This higher level API implements the business logic for
specific applications, such as contact management or trouble ticket
handling.  It also prevents users from performing operations that are
inconsistent with Rackspace's business practices, or assigning data that
would result in other types of high-level corruption of the data in the
database.

With the creation of this second layer, we achieved our original goal
of Core Objects Reused Everywhere. Programmers throughout the company
began to use this API to implement interfaces to application
functionality. This required little interaction with our API
development team, and it could be done without fear of misusing the API.

While we designed the API primarily for CORE, the central enterprise
application, it is reused in a number of other systems at Rackspace. For
example, one group built a SOAP server on top of the API, in order to
access it from their PHP applications. Other applications use the API
directly, and it has been extremely gratifying to see our work reused
and integrated so easily with other systems.

Integrating Python with Apache
------------------------------

With the API in place, our next task in developing CORE was to find a
useful templating module to integrate our Python code with HTML pages
running on the Apache web server.

After looking at a number of available Python-based templating modules,
we opted to create a simple parser of our own. Our approach was to convert
server-side template pages into Python servlets whose output is sent by
the HTTP server to the user's browser.

Although this was a fairly simple exercise, we did run into some
problems stemming from our design of the CORE database meta-class. We
found that altering classes and modules at runtime, as is done by the
meta-class, violates guidelines imposed by Python's optional restricted
execution environment. Since we felt that restricted execution was a
necessary component in supporting a persistent web module, we opted to
deploy CORE using CGIs rather than mod_python or similar persistent
solutions.

Since fast hardware and multiple servers are readily available, and
since and our template parser pre-compiles and caches the Python servlet
code that it produces, the CGI solution is sufficient for our needs.  It
also allows us to resolve issues such as database connection pooling and
restricting the execution environment outside of Python.

Unit Testing
------------

Thanks to the unit testing module that comes with Python, our projects
are reaching production with far fewer bugs than we had ever thought
possible when we were using PHP. During maintenance with PHP, there was
always a question of whether a change in one place would break something
else in another part of the application.

We now write unit tests for each and every API as the API is being
designed. This means that we can verify the changes in one module as
well as its effects on all the others simply by running the unit tests
for the entire API.

Since introducing Python and unit testing, the nature of the bugs that
we see in deployed applications has shifted to include primarily those
in the user interface, such as layout problems or faulty event handling.

These days, very few bugs come from the API itself, and even those are
generally the result of poor revision management or DBA coordination
during application deployment. Python can't solve _all_ problems during
development, but it certainly has reduced the number of critical system
defects for us.

Documentation
-------------

Lack of documentation has been a major problem with our previous
development efforts. We tried several tools and policies to document our
PHP efforts, but in the end these failed. Code changed too quickly, and
the code-level documentation tools available for PHP at the time were
too finicky to justify the amount of effort required to get the
documentation to parse correctly. Additionally, despite careful planning
and coding strategies, the mixture of PHP and HTML made deciphering and
understanding the code more difficult.

Fortunately, Python was designed with documentation in mind, with the
use of &quot;doc strings&quot; for modules, classes and methods. Since
documentation is actually a part of the language itself, and pydoc is a
standard module in the Python distribution, it was easy to extract API
documentation to HTML and other formats.

Over time, we have found that the syntactic structure of Python makes
for extremely readable code, and that in itself helps in the overall
task of documenting and maintaining code.

Conclusion
----------

Python has dramatically improved development processes for the CORE
project, and it has led to the faster development times and more rapid
releases that allow us to keep up with Rackspace's ever-changing
business processes.

Python enabled us to create a sophisticated dynamic data model that is
flexible and easy to use for abstracting database operations. With it,
we realized our goal of Core Objects Reused Everywhere.

Python's integrated unit testing and documentation tools greatly
enhance our ability to deploy and maintain a more stable, error-free
product.

The result is a successful enterprise application that is instrumental
in the delivery of Rackspace Managed Hosting's promise of Fanatical
Support, Unmatched Speed, and Unlimited Flexibility in the managed
hosting industry.

About the Author
----------------

*Nick Borko is the Director of Internal Application Development and the
project manager for Rackspace's enterprise database application, CORE.
Rackspace Managed Hosting is the leader in delivering managed hosting
services to small and medium enterprises. All customer platforms
include state-of-the-art data centers, customized servers, burstable
connectivity, 99.999% uptime SLA, a dedicated account manager, instant
emergency response and access to live expert technicians 24x7 for
support of all hardware and core software. Founded in 1998 and
headquartered in San Antonio, Texas, Rackspace manages servers for
customers in more than 80 countries.*