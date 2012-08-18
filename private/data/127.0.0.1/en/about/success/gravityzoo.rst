**MISSING**
**MISSING**

GravityZoo: Bringing Your Desktop Applications To The Internet As A Service
===========================================================================

**MISSING**
**MISSING**
**Category:**  Business

**Keywords:**  cpython, ubiquitous, distributed

**Title:**  GravityZoo: Bringing Your Desktop Applications To The Internet As A Service

**Authors:**   Mahdi Abdulrazak and Marcel von Birgelen

**Contact:**   `mahdi.a@gravityzoo.com <mailto:mahdi.a%40gravityzoo.com>`_

**Date:**   2007/05/01 23:08:00

**Web Site:**  `GravityZoo <http://www.gravityzoo.com>`_

**Summary:**  Python is the language of choice for the development of the GravityZoo ubiquitous computing framework.

**Logo:**  .. image:: /files/success/gravityzoo/gravityzoo.png    :alt: /files/success/gravityzoo/gravityzoo.png

Introduction
------------

The `GravityZoo <http://www.gravityzoo.com>`_ Company,
founded in late 2005 is a pioneering innovator of
`Software as a Service <http://en.wikipedia.org/wiki/Software_as_a_Service>`_
(SaaS) enabling technology,
`Ubiquitous Computing <http://en.wikipedia.org/wiki/Ubiquitous_computing>`_
and
`Ambient Intelligence <http://en.wikipedia.org/wiki/Ambient_intelligence>`_
Systems.
The core technology of the Company is its framework.
This `GravityZoo Framework <http://gravityzoo.com/products/overview.py>`_ is
designed to develop and host any kind of application while
simultaneously making these applications available at anytime,
anyplace. The latter on any type of client device, be it a PC, a mobile
client like a smart phone or an embedded device like the microwave in
your kitchen, whereby the application has become device aware.

An essential part of the GravityZoo Framework is its sophisticated
object sharing infrastructure. It is within this infrastructure that
object-updates &quot;generated&quot; by the applications are shared with
the devices connected to The GravityZoo Framework. (each device running
a GZF Client). Regarding these Shared objects one can think of both
simple User Interface objects or complex objects related to for example
the operations of a nuclear reactor. In both instances these objects are
handled identically by the core of the GravityZoo
Framework. Identically, because The GravityZoo Framework is designed to
replicate the state changes of all those &quot;shared objects&quot;
between client and server.

GravityZoo Framework
--------------------

The GravityZoo Framework consists of several layers with each a
distinctive function.

.. image:: /files/success/gravityzoo/gzf.jpg
   :alt: GravityZoo Framework

*Application Server component architecture* `Zoom in 
</files/success/gravityzoo/gzf.jpg>`_

Client Side
~~~~~~~~~~~

The client runs a small software stack. This stack consists of a core
and one or more toolkits. The toolkits form the interface between the
Operating System of the client and the Client core.

Backend
~~~~~~~

The backend does the actual application processing and stores most of
the application data and the entire state of the applications. The
backend therefore is the place where the real action takes place.

The REP routing infrastructure enables the messaging between the
client(s) and the backend and the communication between clients. The REP
protocol used is the workhorse of the `GravityZoo Framework <http://gravityzoo.com/products/overview.py>`_. It is
designed to cope with the limitations of the current common Internet
connections.

The application Processing infrastructure is responsible for the
execution of the applications itself and consists of at least one server
with an Application Server role.

The Storage infrastructure stores the user data and the application
state. The Storage infrastructure is known as the Central Object Store
(COS) which is intended as a huge intelligent &quot;object database&quot;.

The Development As A Service (DAAS)
-----------------------------------

DaaS is a newly developed GravityZoo concept allowing software
developers to develop, maintain and test their applications at Anytime,
Anyplace and on Anydevice. The DaaS environment at this stage only
supports development in Python language. This can be done directly in
the GravityZoo Development Environment, allowing you to easily test and
develop small applications, online. In later stages, this environment
will be expanded to a fully featured IDE. Also, we will offer easy
conversion of existing projects developed in common IDEs like Visual
Studio .Net. The GravityZoo Client at this stage allows you
to access the DaaS environment and several demo application. Some of
these applications will be release to public under an Open Source
license.

Why Python?
-----------

The engineering team responsible for the initial prototyping was mainly
Artificial Intelligence oriented. It consisted of professionals,
graduated from the Maastricht University, most of them quite theoretical
and with little to no actual programming experience. The project itself
required a highly object oriented Programming Language able to deliver
the features we required for our prototyping but also was easy to learn
because of the lack of coding experience.
`Python <http://www.python.org>`_
was chosen because it matched the criteria set by the project while
still easy to learn.

Although we considered Python perfect for the prototype phase, we
anticipated that ultimately most of the prototypes would have to be
rewritten into C and C++. However during the prototyping and alpha phase
Python turned out to be more qualified for the job than initially
expected i.e. Python turned out to be a true problem solver. At present
most of the original Python code is still untouched or replaced by new
Python code.

The Python Successes
--------------------

- Speed of development      For us, development in Python has been proven to be much more efficient. Our developers generally finish `Python <http://www.python.org>`_ based projects much quicker than comparable projects in other languages like C, C++, C# or Java. Apart from the latter, Python turned out to be easy to learn for our developers, so easy that even new team members can fairly quickly start focusing on the project rather than learning Python.

- Cross platform capabilities      Python is ported to most platforms that are relevant for our Python code base. This allows large pieces of the `GravityZoo Framework <http://gravityzoo.com/products/overview.py>`_ to be ported to other platforms, with only small adaptations to the Python code base.

- Object oriented architecture      The highly object oriented architecture of Python integrates easily with the core of the GravityZoo Framework, which is entirely object based. Python was quite capable of supporting all data structures needed in the development of the GravityZoo Framework.

- The Open Source advantage      The fact that Python is open sourced works like an insurance policy for us. Although so far we have not yet run into serious problems, we know that we have the possibility to fix it.

- Interfacing with other languages      Python allows us to easily interface to most other languages. This makes it easy to hook other code into our Python code base. Interfacing with other languages is a core aspect of the GravityZoo Framework.

- Stability      One major concern in the beginning was the stability of Python. Until now, Python has been a very robust platform for much of our framework. Most bugs and problems were easily resolved.

- Performance      The performance of Python was also a huge concern for us. During the process we learned a lot of the capabilities of Python. Fortunately, our concerns were largely proven false, the performance of Python has proven to be much better than we expected. For the remaining issues, we have learned to cope with some of Pythons implementation limitations and &quot;design decisions&quot;. Also, the easy interface to other languages allows us to offload certain operations to other languages quite easily.

The Benefit For The Python Community
------------------------------------

The `GravityZoo Framework <http://gravityzoo.com/products/overview.py>`_ allows the `Python <http://www.python.org>`_ developer to easily bring
his/her existing and new Desktop applications to the Internet
as a service. The only action required is to integrate the GUI layer
without the need to compromise the object oriented method of
development.

We firmly believe that this technological development will allow the
Python language and its community to deliver an even greater
contribution to the creation of tomorrows Information Society.

For more information, please visit our `web site <http://www.gravityzoo.com>`_

About the Authors
-----------------

Mahdi Abdulrazak is Chief GravityZoo Evangelist and also responsible for GravityZoo's
Open Source strategy. Marcel von Birgelen is the CTO, lead architect and engineer
of GravityZoo.