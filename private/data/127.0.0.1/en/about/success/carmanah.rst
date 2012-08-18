**MISSING**
**MISSING**

Carmanah Lights the Way with Python
===================================

**MISSING**
**MISSING**
**Category:**  Software Development, Business

**Keywords:**  Embedded Systems, Functional Testing, Product Development, Unit Testing, Energy Efficiency, Quality, Traffic Control, Simulation, Lighting, Marine

**Title:**  Carmanah Lights the Way with Python

**Authors:**   George Belotsky and Thomas Major

**Date:**   2004-06-29

**Website:**  `http://www.carmanah.com/ <http://www.carmanah.com/>`_

**Summary:**  Carmanah Technologies uses Python to help build its rugged self-maintaining solar-powered LED lights.

**Logo:**  .. image:: /files/success/carmanah/carmanah-logo.png    :alt: /files/success/carmanah/carmanah-logo.png

Introduction
------------

This is a story about how Python's elegant design can make the
language useful in an unexpected way.

Carmanah Technologies Inc. (`http://www.carmanah.com/ <http://www.carmanah.com/>`_) was conceived
in the middle of the Pacific Ocean.  The founder, David Green, was
sailing his boat from Fiji, bound for Victoria, British Columbia.  He
was running low on battery power for his navigation lights, and had an
insight.

The eventual result of that mid-ocean idea was the world's first
self-contained, fully autonomous marine navigation light.  During the
day, each device uses solar power to recharge its integrated
batteries.  The light then operates from the stored charge at night.
In place of conventional bulbs, Carmanah's systems use long lasting,
high-efficiency LEDs. The overall result is an exceptionally rugged
device, sealed against the elements and requiring no maintenance.

On occasion, lost Carmanah lights have drifted for thousands of miles
upon the ocean currents, only to be recovered later -- in full working
order.  This sort of reliability has made them famous amongst waterway
authorities, sailors and the coast guards of various countries.

The technology born of the harsh marine environment has proven useful in many
other areas, and today Carmanah is the world leader in solar-powered LED
lighting. The company manufactures a whole line of such lights for a variety
of different uses, including transit, roadway, railway, industrial markers and
airfield illumination as well as the original marine application. The lights
are sold all over the world, and must often with stand extreme conditions (the
open ocean, desert climates, the far north, urban vandals, etc.). Carmanah's
lights have even been the subject of a documentary on national television.

.. image:: /files/success/carmanah/xwalk-closeup-web.jpg
   :alt: Closeup of one crosswalk traffic beacon.

*Closeup of a Carmanah crosswalk traffic beacon, a recent product in
which Python has played a significant role.  The enclosure at the top
of the pole is oriented towards the sun, to better expose the solar
panels that it carries on the front. The antenna for the wireless link
to a similar unit on the other side of the street is visible at the
left side of the enclosure.* `Zoom in </files/success/carmanah/xwalk-closeup-zoom.jpg>`_

Electric lighting has become so commonplace, it seems like a simple
idea.  An autonomous, self-contained light, however, turns out to be a
complicated thing indeed.  The amount of usable solar radiation varies
with the weather, the seasons, one's position on the earth, and the
orientation of the solar panel.  The battery state of charge must be
carefully managed to ensure long life and correct operation.
Available power has to be monitored, and possibly rationed through the
night.

Depending on the application, the light may also have to be
programmable to emit internationally recognized flash codes, react to
user input, etc.  In even more complex situations, wireless networking
is required to allow the lights to communicate with each other, or
with a central base station.

A great deal of mechanical, electrical, electronic and optical design
is required to create these lights.  As is typical of modern complex
devices, an embedded software program running on a microcontroller
operates each unit, making it come to life.  Like a miniature version
of the Monolith from *2001: A Space Odyssey*, each light maintains
itself, ready to perform its function whenever the need arises.

The Future of Practical Computing
---------------------------------

Current practical computer applications are dominated by the PC.  Yet,
just like the mainframe before it, the PC will lose its central place
in the use and deployment of computer technology.  Embedded systems --
computers that are part of other devices -- will be the most prevalent
in the future.

The mainframe is far from being obsolete today, and the PC will
likewise remain important.  Most computers, however, will be
incorporated into something else, rather than standing alone.  This
process has already begun.  Automobiles employ multiple embedded
systems, some of which communicate with each other.  Embedded systems
also operate many household appliances.  Such systems are likewise
very important in industry, where they form a crucial element of many
instruments and tools.

The catalyst for the future expansion of embedded systems is the rapid
advance of network technology.  As the hardware becomes less
expensive, smaller, faster and more efficient in the use of electrical
power, networks of embedded devices will proliferate and grow.  Such
devices -- in collaboration with one another -- will control homes,
offices and industrial facilities.  Preparations for this new world of
computing are underway now, as evidenced by the Cambridge-MIT
Institute's *Pervasive Computing* initiative (see `http://oxygen.lcs.mit.edu/ <http://oxygen.lcs.mit.edu/>`_).
The initiative has also been covered in a BBC story (see
`http://news.bbc.co.uk/1/hi/technology/3583479.stm <http://news.bbc.co.uk/1/hi/technology/3583479.stm>`_).

The emergence of Pervasive Computing will make it necessary for each
system to be very low maintenance.  When every user requires hundreds
of devices, it is simply not feasible to service them all on a regular
basis.  Of course, fully self-contained systems that manage their own
power would be ideal, because changing batteries or attaching wires is
a serious challenge if it needs to be done on a large scale.  Thus,
the miniature Monolith becomes a swarm.

The Importance of Python
------------------------

Large scale deployment of embedded systems demands inexpensive
components.  Considerations such as small size, high reliability and
low power consumption are also very important.  Specialized processor
chips, called microcontrollers, have been developed to meet these
goals.  Combining CPU, memory and peripherals (such as UARTs) on a
single chip, modern microcontrollers are marvelous devices.  These
features, however, come at a significant price.  A typical
microcontroller has only a few hundred bytes of RAM, several K of ROM
(to store the program) and orders of magnitude less processing
capability than a conventional desktop microprocessor.  Hardly an
environment for running Python!

There are projects to adapt Python for embedded applications, but they
require significant resources on the microcontroller, and are still in
the very early stages.  Surprisingly, however, it turns out that
standard Python is of tremendous value throughout an embedded system's
lifecycle.  This is because the highly resource-constrained nature of
embedded devices make them dependent on standard PCs for many tasks --
both during development and during deployment.

For example, embedded software is compiled on conventional desktop
systems, and the resulting object code is then loaded onto the target
microcontroller.  Another example is troubleshooting a device in the
field, which usually requires additional hardware to run a diagnostic
utility.  Ordinary laptops are a very attractive platform for this
application, due to their ready availability and relatively high level
of standardization.

Thus, a major part of any embedded software development effort is
writing the required support code, to run on a standard PC.  There are
quite a few languages available for this task, but the advantages of
Python are many.  Python is quite easily learned by people from
various programming backgrounds, such as Java, C or Visual Basic.
After becoming familiar with Python, development proceeds very quickly
-- perhaps faster than with any other language.  At the same time,
Python lends itself to the creation of highly readable, compact and
well structured code.

Python's particular mix of features also helps embedded developers be
more effective when programming a PC.  While these developers are well
familiar with C (by far the most popular high level language for
embedded systems) a C program written for a standard desktop or server
is quite different in style from one for a microcontroller.

The compactness of Python programs is especially important, because
embedded developers have, by necessity, learned to express their
designs in a very small amount of code.  Python's automated memory
management also helps, because many embedded developers have little
experience with dynamic memory allocation -- a technique that is not
practical in most embedded environments.  In addition, the
Object-Oriented facilities of Python are simple, powerful yet not
coercive.  This allows embedded developers (who are often less
familiar with OOP) to gradually adopt the Object-Oriented paradigm in
their work.

As embedded systems grow in complexity, the advantage of using Python to
augment traditional techniques becomes more and more important. At Carmanah,
Python adoption (which began with the crosswalk traffic beacon, a
sophisticated device that includes wireless networking) has spread to several
key areas of the embedded system's lifecycle.

A Python program controls the software build process, allowing firmware for
different products to be put together from a large number of shared
components. The build system is simple yet a lot more flexible than makefiles,
as well as easier to customize, configure and extend. Unlike the build tools
supplied by compiler vendors, the Python-based build system can work with
different compilers.

Python is also used for stress tests and unit testing -- an aspect of
development particularly vital in embedded systems, due to the
inherent difficulty of upgrading devices once they are in the field.
Additional uses of Python, such as for control panels and code
generation, are being considered as well.

One very exciting application of Python at Carmanah is in the role of
a device simulator.  A simulator can act as a node in an embedded
network, while displaying the internal system state via animated
images on the screen.  Simulators are very valuable during the early
stages of an embedded project, when little actual hardware is
available.  By taking the place of missing devices, simulators can
allow software development to continue even before the hardware design
is completed.

.. image:: /files/success/carmanah/xwalk-proto-web.jpg
   :alt: Prototype of Carmanah's crosswalk traffic beacon attached to a device simulator written in Python.

*Here is an illustration of the usefulness of Python in embedded
development.  A prototype of Carmanah's crosswalk traffic beacon
interacts with a Python-based simulator running on an ordinary PC.
The simulator effectively completes the system, because two traffic
beacons (one for each side of the street) are required in a crosswalk
installation.  In addition to significantly accelerating development,
a Python-based simulator can easily animate drawings, as shown.  This
allows meaningful demonstrations of the system much earlier than would
otherwise have been possible.* `Zoom in </files/success/carmanah/xwalk-proto-zoom.jpg>`_

At Carmanah, Python has been used not only by experienced engineers,
but by student interns as well.  Even interns with little prior
programming experience can accomplish quite a lot with Python, while
requiring less supervision than other languages demand.

Conclusion
----------

The exciting work of creating self-contained, autonomous devices
continues at Carmanah.  As the swarm of micro-Monoliths becomes reality,
the importance (and complexity) of the embedded software grows.  By
making such software much easier to develop, test, control and deploy,
Python is really lighting the way to the future of computing.

About the Authors
-----------------

*George Belotsky is a software architect who has done extensive work on
high performance Internet servers as well as hard real time and
embedded systems. His technology interests include C++, Python and
Linux.  George Belotsky has written a number of articles (see*
`http://www.oreillynet.com/pub/au/1204 <http://www.oreillynet.com/pub/au/1204>`_ *) including a series on Python
and Network I/O.  He is also the author of the Flightdeck-UI open
source project (* `http://openlight.com/fdui/ <http://openlight.com/fdui/>`_ *).  You can reach him by
email at questions at openlight.com.*

*Thomas Major is the Product Development Manager at Carmanah, an electrical
engineer by schooling with broad product design experience acquired at
Visteon and Philips Electronics.  His interest started in analog circuit
design, later embracing digital, software, and embedded design.*