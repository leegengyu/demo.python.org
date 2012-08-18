**MISSING**
**MISSING**

Maritime Industry Increases Efficiency with Python
==================================================

**MISSING**
**MISSING**
**Category:**  Software Development, Business, Engineering

**Keywords:**  Product Development, Rapid Application Development, Quality, Marine, Manufacturing

**Title:**  Maritime Industry Increases Efficiency with Python

**Author:**   Henrik Wimmerstedt

**Date:**   2003/01/17 15:59:02

**Website:**  `http://www.tribon.com/ <http://www.tribon.com/>`_

**Contact:**   `info@tribon.com <mailto:info%40tribon.com>`_

**Summary:**  Tribon Solutions uses Python to increase efficiency in ship design and construction.

**Logo:**  .. image:: /files/success/tribon/tribon-logo.gif    :alt: /files/success/tribon/tribon-logo.gif

Introduction
------------

`Tribon Solutions <http://www.tribon.com/>`_ develops, markets and supports CAD/CAM/CIM software
solutions, with the mission of increasing overall efficiency in the
maritime industry.

For more than 30 years the company has provided shipyards, design
agents and maritime equipment suppliers with new ways to improve cost
efficiency, quality and performance. Our solutions are proven to
generate time savings and to increase speed to market.

With its head office in Sweden and offices in the Republic of Korea,
China, Japan, Germany, the UK, Russia, Singapore and the USA, Tribon
Solutions serves the global maritime industry and customers in more
than 43 countries.

The Need for a Ship Building API
--------------------------------

The building of a ship is initiated by the need to transport goods,
people, or firepower. The particular need dictates the dimensions,
layout of the cargo area, engine power, and other basic attributes for
the ship. The design for the ship then meshes these requirements with
strength and safety regulations. Because most transport needs are
unique, many ship designs are built only once or only in a small
series.

The Tribon software suite covers the ship building process from the
first concept to the finished ship. The design and construction of a
ship involves a high degree of concurrent engineering. To solve this
problem Tribon uses a Product Information Model (PIM), which is the
central repository and single source of information for designers,
planners, administrators of material, manufacturing personnel, and
others working on design and construction.

.. image:: /files/success/tribon/tribon-web.jpg
   :alt: View of a small part of a ship's PIM created using the Tribon system

*View of a small part of a ship's PIM created using the Tribon system.
Picture courtesy of Samho Heavy Industries Co., Ltd.* `Zoom in </files/success/tribon/tribon-print.png>`_

Even though most ship designs are unique, shipyards try to lower cost
by using as much standardized and parameter-driven design as possible.
The problem for a software vendor is that design principles are
different at each yard due to factors such as ship type, production
facilities, prior experience, and national regulations and standards.

Tribon's solution to this problem was to make it easy for shipyards to
develop their own functionality based on Tribon core technology,
including the Tribon PIM. To achieve this, Tribon Solutions had to
create an API that was platform independent, easy to use, had all the
strengths of a modern programming language, and was extendable and
embeddable.

Choosing Python
---------------

Tribon began work on its API in 1995. Two different paths were
considered at this stage: Either to publish directly the libraries used
by Tribon, or to create a wrapper on top of existing code.

The first approach would make all our functionality available to the
user, but users would have to use the same development environment as
Tribon Solutions, change compiler versions when Tribon Solutions did
so, and so forth. This would have been an expensive and complex
solution, only usable by the largest shipyards in the world, those that
had their own large IT and development departments.

The second approach was preferable, as long as a tool could be found
or developed that covered most of the given criteria. Tribon already
had a geometry macro language that was developed in-house, but to
extend it to the desired level of functionality would have been costly
to implement and maintain. The remaining option was to find a 3rd party
solution that fulfilled the API's needs.

During investigation of options, Python was discovered quite early when
a member of the development team read about Python in a computer
magazine. After some initial experimentation there were really no other
contenders. Python had it all. It was a beautiful programming language
that was extensible, embeddable, platform independent, and had no
license cost.

When it came to incorporate Python into the Tribon software, we found
the integration to be quite easy and problem-free, and it was achieved
with very little effort. The result of this merge between Tribon and
Python was named Tribon Vitesse, and the first version of Python used
was 1.2.

Experiences
-----------

During the last seven years Tribon Solutions has been able to move with
the updates of Python without any major inconvenience to our customers
or ourselves. Today we have customers that have developed hundreds of
modules over the years. Python's platform independence, and the fact
that it is an interpreted language, have been a major benefit to
customers that have migrated from the VMS and UNIX to Windows. They
have been able to port their code with no changes or at most only minor
changes.

Today Tribon Solutions has customers that have, by utilizing the power
of Tribon Vitesse, been able to reduce design time of certain complex
ship structures from four weeks to two days, while improving overall
quality. This enormous reduction in design time has been possible by
automating more of the design, calculations, information search, and
result checking.

Other customers have created entire applications, based on Tribon
technology, that fit perfectly into their way of working and thinking.

Python is also used to customize the Tribon system through the
implementation of hooks and event driven triggers that allow the user
to control the graphical user interface, information display, design
standards, and much more.

In the fall of 2002, as a further service to customers, Tribon
Solutions formed a Developer's Network that supports third party
vendors building maritime solutions based on Tribon Vitesse.

Summary
-------

Today Tribon Vitesse consists of over 500 functions and more than 50
different classes, and it is still growing.  Development is to a
large extent driven by customer requests.

Python has proven to be a perfect tool for creating an API to
existing applications because it is:

    - Extendable

    - Embeddable

    - Platform independent

    - Easy and logical to learn, even for non programmers

    - A beautiful programming language

Visit Tribon Solutions on-line at `www.tribon.com <http://www.tribon.com/>`_ for more information
or contact `info@tribon.com <mailto:info%40tribon.com>`_.

About the Author
----------------

*Henrik Wimmerstedt is product manager for the Tribon Developer's Toolkit and
chairman of the Tribon Developers Network. He joined the company in 1997,
after studies in naval architecture.*