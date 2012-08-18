**MISSING**
**MISSING**

Putting Web Services to Work with Python
========================================

**MISSING**
**MISSING**
**Category:**  Software Development

**Keywords:**  Web Development, Web2.0

**Title:**  Putting Web Services to Work with Python

**Authors:**   Dr Tim Couper and Marc-Andre Lemburg   Siena Technology Ltd.

**Date:**   2003/01/17 15:59:01

**Website:**  `http://www.siena-tech.com/ <http://www.siena-tech.com/>`_

**Summary:**  The Siena Web Services Architecture brings Python productivity to enterprise Web services development.

**Logo:**  .. image:: /files/success/siena/siena-tech-logo-sm.gif    :alt: /files/success/siena/siena-tech-logo-sm.gif

Introduction
------------

Consultants naturally try to provide their customers with the best
solutions for a problem. Sometimes this means exploring new areas
together with the customer or directing the project into a solution
space that better fits the problem than the usual &quot;buzzword-compliant&quot;
approaches. We've seen these fail too often, misleading the project
into solving problems relating to the selected technology, rather than
meeting the original project plan.

Python Goes Fortune 500
-----------------------

In a recent project for one of our customers, we faced a problem that
is quite common in Fortune 500 companies: Multiple clients running on
unmanageable client machines are tied closely to complicated database
relationships, making management and further development very
difficult.

Thanks to the marketing efforts of several large server vendors, our
solution space was quickly identified. What the company needed was &quot;Web
services&quot;, or put simply, a way for a client application to talk to the
server side in a reasonably standardized manner. Our customer was
already using two of the dominant technologies in this area:
Microsoft's .NET and BEA's WebLogic J2EE server.

When we came into the project, a team was already trying to solve some
of the company's problems using the J2EE platform. However, we found
that they were spending more time trying to work around design problems
in the technology than actually writing code for the services. Since
the company had already been introduced to Python in a smaller XML
project, we were able to convince the project lead to try a new
technique based on Python.

The idea was to leverage the efficiency of Python programming together
with its good database connectivity to compete against the J2EE team.
What we needed was a stable and robust server implementation and
a flexible way to write and publish Web services. Fortunately, the
server had already been written in the form of the easily extensible
eGenix.com Application Server, so our task was simply one of adapting
this server to make writing services as easy as possible.

Keep IT Simple But No Simpler (KISS)
------------------------------------

Following the Python paradigm of &quot;obvious is better than obscure,
explicit is better than implicit,&quot; we chose the most straight forward
possible way of dealing with Web services: Each service was mapped to a
Python class, which provided the public methods to call from the client
application. There were two reason that we felt that service
implementations should look no different than any standard class
implementation in Python for two reasons: (1) a programmer should not
need to learn a new way of coding just to be able to write services,
and (2) existing integrated development environments (IDEs) should be
used to make coding services even easier.

Since Python is an object-oriented programming (OOP) language in all
respects, the implementation we chose placed basic shared functionality
into a *Service* base class that hides networked server interaction
from the programmer. As a result, the service developer only needs to
think about the business logic in the service methods and can rely on
the server to automatically provide database connection pooling, protocol
handling, transaction control, and all the complicated interactions
that are needed to make a server side implementation robust.

Client-Side Bliss
-----------------

Another design goal for the system was to simplify client-side
programming as much as possible, in order to make it easy to adopt the
new technique. Just as service writers shouldn't need to think about
low-level database connectivity, we felt that client application
programmers shouldn't be bothered with the details of setting up
connections and talking to the server side. We wanted to design a very
simple application programmer's interface (API) which would hide all
the complications inherent to networked client/server interaction.

Client side agents for Java and Windows' COM interface made this
possible by enabling access to the Web services from all major client
application environments such as Visual Basic (VB), Visual Basic for
Applications (VBA as used in Word, Excel, and Access), Delphi, C++,
Java, C# and others. These not only hide the protocol level from the
application programmer, but also provide the key to enabling security
and fail-over solutions.

Web services standards are still in the planning stage, and it is not
at all clear which of the proposals will be accepted by standards
organizations. By creating a true middle tier, we were able to hide the
particular methods and protocols we chose inside of the Siena client
and server, and were free to use existing security standards and
authentication modes to build a secure communication channel.

.. image:: /files/success/siena/image1-web.jpg
   :alt: The Siena Web Services Architecture

*The Siena Web Services Architecture* `Zoom in 
</files/success/siena/image1.png>`_

Above and Beyond Web Services
-----------------------------

With these basic building blocks, we were moving towards realizing the
Siena Web Services Architecture, which included a Python-based server
side, a COM client side agent (also written in Python), and a Java
client side agent.

One distinct advantage of writing both the server side and COM client
side of our Web services architecture in Python was that we could
automatically replicate services from the server to the client side.
This was possible whenever a service did not depend on database
connectivity or other elements specific to the server-side environment.
Python's data packaging facilities and portable byte code format made
this operation quite easy to implement. The result was a significant
boost in application performance, reduced network bandwidth
requirements, reduced network latency, and increased server
performance, all without sacrificing the efficiency of centralized
server-side management that makes Web services so attractive to IT
management.

.. image:: /files/success/siena/image2-web.jpg
   :alt: Managed client-side service replication with Siena Web Service Containers

*Managed client-side service replication with Siena Web Service Containers* 
`Zoom in </files/success/siena/image2.png>`_

The Python Mantra
-----------------

Still missing in our plan were the skills needed to code Python servers
and clients. Most of the programmers in our team knew only a mix of
Java, Visual Basic, and C++. While the J2EE group was working on solving
J2EE problems, we invested a day in teaching Python to the rest of the
team.  Python wasted no time making its way into the hearts and minds of
these programmers. It was a thrill to hear fellow programmers chiming in
with our own Python mantra: &quot;This is what I've always been looking for.&quot;

Results
-------

Happy programmers are good programmers, and good programmers work
efficiently. That's what project management learned at this point
in our effort. The group's Web services programmers quickly caught onto
the new Python-based system and development progressed at amazing
speed. Services could now be implemented in a few *minutes* rather than
the days needed using the typical J2EE approach. Now most services were
completed and deployed in less than a day, and the ease and speed with
which they can be modified and tested has made an incremental approach
to service development possible. And IT management was excited to see
the overall high performance of our solution.

The Siena Web Services Architecture has become a crucial
mission-critical component for this customer, as it moves from a two
tier to three tier architecture and adds fail-over and security to their
Web services.

The Siena Web Services Architecture will soon become part of our
product line. If you are interested in the solution, please visit our
web-site at `http://www.siena-tech.com/ <http://www.siena-tech.com/>`_ or contact us directly.

PS: After several months of effort, the J2EE team never did get their
Web services working.

About the Authors
-----------------

*Dr. Tim Couper (tim@siena-tech.com) is the chairman of Siena
Technology. He holds a mathematics D.Phil. and has 20 years experience
running software companies. He now spends most of his time consulting
as architect and technical lead for large development projects, and has
been extensively involved in planning and coordinating the 2002 and
2003 Python UK conferences.*

*Marc-Andre Lemburg (mal@siena-tech.com) is the Chief Technical Officer
(CTO) of Siena Technology. He holds a degree in mathematics from the
University of Duesseldorf. Marc-Andre has been working with Python
since 1993, is a Python Core Developer, board member of the Python
Software Foundation (PSF), author of the well-known eGenix.com mx
extensions (mxODBC and mxDateTime), and was one of the executive
organizers of EuroPython 2002.*