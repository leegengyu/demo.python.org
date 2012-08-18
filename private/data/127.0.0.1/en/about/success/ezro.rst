**MISSING**
**MISSING**

Python and Zope in the EZRO Content Management System
=====================================================

**MISSING**
**MISSING**
**Category:**  Software Development, Business,

**Keywords:**  Scalability, Web Development, Web2.0, Aviation, Knowledge Management, Accessibility, Content Management

**Title:**  Python and Zope in the EZRO Content Management System

**Authors:**   Andy J. Williams Affleck and M. Adam Kendall   Development InfoStructure (devIS)

**Date:**   2004-06-02

**Website:**  `http://ezro.devis.com/ <http://ezro.devis.com/>`_

**Website:**  `http://www.devis.com/ <http://www.devis.com/>`_

**Summary:**  Python and Zope speed development of devIS EZ Reusable Objects (EZRO), a flexible content management system used in the eGovernment sector

**Logo:**  .. image:: /files/success/ezro/devis-logo.gif    :alt: /files/success/ezro/devis-logo.gif

Introduction
------------

`Development InfoStructure (devIS) <http://www.devis.com/>`_ is a small consulting firm in Arlington,
Virginia that is well known for its work in the eGovernment sector. This includes
development of small, medium, and large-scale systems.

devIS `EZ Reusable Objects (EZRO) <http://ezro.devis.com/>`_ is a content management system which can be
used for many different kinds of websites, including traditional information
presentation sites such as `http://www.devis.com/ <http://www.devis.com/>`_, portals like
`http://www.milspouse.org/ <http://www.milspouse.org/>`_, training sites like `http://cable.devis.com/ <http://cable.devis.com/>`_, and
coach style sites.  A coaching site appears as a frame on the edge
of the screen and drives another site in order to walk the user through that
site, as in `http://www.careeronestopcoach.org/ <http://www.careeronestopcoach.org/>`_.

EZRO was the outgrowth of a number of contracts with the Department of Labor
over the years from 2001 through 2004. It was developed under the name of
Workforce Connections. devIS contributed its copyright to the Department of
Labor to allow them to release it as an open source tool in January 2004. EZRO
is a more advanced version of the Workforce Connections software that has been
released by devIS under the GPL.

.. image:: /files/success/ezro/ezro-screenshot-web.jpg
   :alt: EZRO Screenshot

*EZRO's repository management interface is used to author and manage content
for the websites that are based on it* `Zoom in </files/success/ezro/ezro-screenshot.jpg>`_

Why Python
----------

EZRO was originally developed as the engine to host the Department of Labor's
DisabilityInfo portal, originally called Disability.gov, later renamed to
DisabilityDirect.gov and now `DisabilityInfo.gov <http://disabilityinfo.gov/>`_. The site is a portal site
that is maintained by people in each of the major agencies including the
Departments of Labor, Education, Transportation, Defense, Commerce, as well as
the Social Security Administration and Health and Human Services. The
Department of Labor, the implementing agency, had final editorial authority.

What was needed was a content management system that allowed for distributed
editing and centralized editorial control that had to be fully accessible to
the disabled. To further complicate things, an Executive Memorandum from
President Bush mandated the site go live within sixty days. While some work
had already been started and a previous generation of the site existed, there
was still an incredibly tight deadline to meet. As the site was to be one of a
handful of sites mandated by the White House, it had to be done right the
first time.

devIS decided from the start of the project that our code had to meet two
general requirements. First, the software should eventually, some time after
meeting the initial deadline, be released as open source. Second, it had to be
portable enough to run on several platforms.

Python and `Zope <http://www.zope.org/>`_, a web application server written in Python, were chosen
for the work. devIS had been using Zope since 1999 and already had a large
staff of developers that were skilled in the ways of Zope, including the owner
and developer of `ZopeLabs <http://www.zopelabs.com/>`_.

At this time devIS was still developing its web applications using Zope's
management interface, DTML (dynamic template markup language) tags, and short
Python scripts to create dynamic sites. But Zope's management interface was
not a good environment for group work: one developer could accidentally
overwrite another developer's work with no warning and there was no adequate
version control.

With five developers working half-to-full time on this project, it was clear a
better solution was needed. The natural conclusion was to start developing in
Python using the Products framework available in Zope. A Zope product is a
package of code, graphics and templates that provides a piece of reusable
web functionality. We were able to combine the integrated pieces of Zope that we
loved and used on a daily basis, like user management and simple object
publishing to the web, with the flexibility of Python and its large internal
library. This also allowed us to keep source code outside of the Zope object
database and on the file system, where it could be used with our existing CVS
infrastructure for source code control and reporting.

.. image:: /files/success/ezro/ezro-stack-web.jpg
   :alt: EZRO Architecture

*EZRO was developed in Python, as a Zope Product. It interacts with other Zope
Products and uses aspell as an external process for spell checking. The
content management interface and published web content is provided to its
users through Apache or other web server.* `Zoom in </files/success/ezro/ezro-stack.jpg>`_

Implementation
--------------

Development of the EZRO content management solution started with the
assumption that the application would grow over time, as most software
projects do. The initial choice was between producing the software from
scratch, or using an already existing framework like the Zope CMF or Plone,
both of which were first released around the same time as development
was started on EZRO.

After carefully reviewing the alternatives, it was decided that developing a
new solution would result in a product more closely tailored to the client's
needs and requirements, without the significant overhead incurred by the
unneeded parts of CMF or Plone.

Because Python allows for very rapid development, this choice was not at odds
with the very tight initial deadline on the DisabilityInfo project. In two
weeks, a working prototype was ready to show to the client. The first
production quality release of the software only took an additional three
weeks, building directly upon the prototype.

By using Python, maintenance overhead was greatly reduced. Over the next year,
devIS developers were able to add new EZRO features quickly and easily, in
response to requests from the client. As devIS acquired new clients, EZRO was
leveraged to reduce development cost of new projects.  In this way, the tool
grew in features and scale to what it is today.

Python's clean layout and structure also made the code that was released later
as open source more readable. This was a boon when bringing new developers on
board, as they were able to jump in and understand the code right away.

Because of the cross-platform nature of Python, EZRO runs equally well on
Microsoft Windows and any Unix-like operating system, including Linux and
MacOS X. devIS has released a self-contained EZRO environment with installer
for Windows, and distributes just the EZRO Zope Product in tar archive form
for other environments. The software does rely on `Zope <http://www.zope.org/>`_, `Aspell <http://aspell.sourceforge.net/>`_ and
`PyXML <http://pyxml.sourceforge.net/>`_, but because of Python's portability, all of these third party
applications also run on most other operating systems.

EZRO runs happily on a single machine but is deployed in the devIS production
facility on three redundant servers for the public-facing sites, and a fourth
secure server for the administrative back-end.

Conclusion
----------

Python and Zope together gave devIS incredible flexibility and allowed
implementing new features on a very rapid cycle, which, in turn, has greatly
pleased devIS clients. The OSHA Training Institute is using EZRO to develop its
training materials and they've informed devIS that they are saving thousands of
dollars per day in development costs. As a bonus, the people who use it to
develop their courses actually enjoy coming to work and using this tool. In no
other set of tools have devIS staff found such ease of implementation.

About the Authors
-----------------

*Andy J. Williams Affleck is the project manager for EZRO and M. Adam Kendall
is the lead developer on the project. Andy has an Ed.M. from the Technology
in Education program at the Harvard Graduate School of Education and has
many years background in creating solutions for online learning and
teaching. Adam is the creator of zopelabs.com, holds a BFA in Digital
Design, and has over 9 years web programming experience.*