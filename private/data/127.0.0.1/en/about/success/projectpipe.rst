**MISSING**
**MISSING**

Botonomy Uses Python to Create ProjectPipe.com for Web-based Project Management
===============================================================================

**MISSING**
**MISSING**
**Category:**  Business

**Keywords:**  Project Management, Web2.0, Web Development, Groupware, Network Development, Product Development, Rapid Application Development

**Title:**  Botonomy Uses Python to Create ProjectPipe.com for Web-based Project Management

**Author:**   Mike Coyle

**Contact:**   `mcoyle@botonomy.com <mailto:mcoyle%40botonomy.com>`_

**Date:**   2006/08/23 15:00:00

**Web site:**  `http://projectpipe.com/ <http://projectpipe.com/>`_

**Summary:**  Python and the Twisted asynchronous networking framework form the basis for an advanced project management tool written with an Ajax web interface.

**Logo:**  .. image:: projectpipe-logo.png    :alt: projectpipe-logo.png

Introduction
------------

`ProjectPipe <http://www.projectpipe.com>`_ is a hosted project management solution developed by Botonomy
LLC. It provides everything that you need to manage the full lifecycle of a
midsized project.

Although it is a hosted browser-based application, ProjectPipe seamlessly
integrates with MS Project, Excel, and Word, allowing users to leverage the
benefits of ProjectPipe without abandoning the desktop tools that they (and
their peers) use and understand.

We believe that dependency management is the root cause of many project
headaches, so we make it very easy to establish, manage, and visualize
dependencies among and across requirements, tasks, issues, etc.

With ProjectPipe, all project team members have access to project data, as
well as a Subversion source code repository. All of the features are
integrated, and we leverage a number of modern techniques to help you manage
your data, such as RSS, Tagging, and an intuitive &quot;Ajax&quot; interface. You can
manage your data as an outline, or build custom queries with complete control
over filter criteria, column layout, and sort order. We figure that you know
more about your project than we do, so we give you a set of very flexible
tools to mold our software around your project, instead of vice-versa.

Background
----------

Christian Simms, Botonomy co-founder, and I had worked together for several
years, and we used Python for utility-type tasks in larger J2EE projects. We
had talked informally a couple of times about building some kind of software
product or service.

I had just wrapped up a project where the client had no source code control or
issue tracking tools available to the 100% offsite project team. We talked
about the fact that there wasn't a hosted solution that explicitly addressed
all of the project management needs of small teams at an attractive price
point. We also saw the Software-as-a-Service (SaaS) model being validated by
the likes of Salesforce.com and likely to grow in the coming years.

So we set out to build the &quot;Everything that you need to run a midsized project
in one box&quot; service, combining project data (requirements, issues, etc.),
process guidance, and source code management in a single integrated solution.
We also had the idea that we could bring simplified, purpose-built Nouvelle
Artificial Intelligence (think videogames, not academia) to the agile project
management world by providing a number of autonomous agents, or &quot;bots&quot;, to
assist small agile project teams in their planning, process adherence, and
execution.

We wrote bots to conduct interviews, bots to maintain risk lists, bots to
build project plans, etc. We believe that by leveraging bots to handle
well-understood and/or repetitive tasks, team members would have greater
autonomy in addressing the high-value needs of their project. Hence the name
of our company, Botonomy LLC.

Python made our initial proof-of-concept experiments fast and painless to
implement (even if the late nights and weekends weren't so painless). Many
people have used the term &quot;executable pseudo-code&quot; to describe Python, and I
wholeheartedly agree. If we had to do our prototypes in a heavier language and
more cumbersome development environment, we wouldn't have gotten the momentum
that we needed to get the idea off the ground.

After we had the bot architecture working, we went back-to-basics and fleshed
out the UI and content-related aspects of the system. We had our first beta
release in September 2005. We went live in production on 12/23/2005 (that's
`Festivus <http://en.wikipedia.org/wiki/Festivus>`_ for any `Seinfeld <http://en.wikipedia.org/wiki/Seinfeld>`_ fans out there). In May 2006, we released a major
upgrade to the application, with significant usability and look-and-feel
improvements. Some of the bot-based functionality made it into the production
releases, and other pieces are still being developed or refined for future
releases.

The View from 10,000 Feet
-------------------------

ProjectPipe actually has a somewhat novel architecture. It uses a traditional
relational database for persistence, but it also uses an XMPP/Jabber server to
manage the communications among the several bots that run the backoffice,
performing tasks such as creating new accounts, building project plans, etc.
These bots basically chat back and forth over IM as if they were people. This
XMPP infrastructure also drives our desktop integration strategy, allowing
rich interaction between the browser-based application and MS Project, Excel,
and Word.

Part of the &quot;secret sauce&quot; of ProjectPipe lies in the way we're bridging the
HTTP and XMPP worlds behind the scenes. We're pleased that we were able to
address a tricky real-world problem (web-to-desktop integration) atop open
standards (HTTP and XMPP) and documented interfaces (MS Office COM bindings).
Below is a high-level diagram of the ProjectPipe distributed architecture:

.. image:: projectPipeArchitecture_small.png
   :alt: ProjectPipe High-Level Architecture

*High-level view of the ProjectPipe distributed Architecture* `Zoom in 
<projectPipeArchitecture.png>`_

In addition to addressing the web-to-desktop integration challenge, this
bot-based architecture had three interesting side-effects:

- It allowed us to interact in real-time with these subsystems. We could fire up iChat and interact with the bots via IM, using a simple and limited english-like grammar

- It allowed us to make the core system relatively small, since we didn't need to bundle in the work that was being done by the bots. Sure, there was still code to write, but the bot code is conceptually and physically decoupled from the stuff that drives the web user interface.

- It provides a roadmap for gradually folding in the AI functionality that got us excited and working on this in the first place. Most importantly, we can add arbitrarily complex functionality without making any significant changes to the core system

A Peek Under the Hood
---------------------

To implement this distributed, multi-protocol architecture, ProjectPipe is
built atop the `Twisted <http://twistedmatrix.com>`_ Networking Framework. Twisted's asynchronous model
allows us to have all of the Jabber bots running in the same process as the
HTTP server, but we could just as easily migrate the bots to other processes,
hardware, or data centers, for that matter.

I cannot imagine building a system of this type without using Python and 
Twisted. 

Christian and I both had previous experience with Python, but primarily as a
scripting language to process text or automate miscellaneous tasks. I went to
PyCon 2004, and was shocked by the number of interesting projects that were
developed and maintained by lone developers or very small teams. I was
particularly impressed by the demos and presentations given by the Twisted
team.

We briefly considered using J2EE, but felt that rapid development of our
initial prototypes would be much faster in Python and Twisted. In the end, we
estimate that it would have taken us at least twice as long for a solution
with less than half the functionality if we had gone with J2EE.

Python was an ingredient from the beginning. The asynchronous networking in
Twisted made this type of multi-protocol application possible. The clarity,
conciseness, and expressiveness of Python made it practical for a two-person
team to take it on. The lack of an explicit compilation step, coupled with the
ability to dynamically reload modules allow us to turn very fast cycles during
development.

The current codebase is about 30K lines of code, written over the last year or
so. I do a lot of the prototypes, mockups, etc., but Christian has implemented
most of the current codebase himself. The productivity that Python provides
over the &quot;mainstream&quot; languages is profound.

We've also found the application stack to be very robust. As our flagship
application, ProjectPipe is mission critical. If it proved unreliable to our
customers, we'd be out of business.

The Cast of Characters
----------------------

Alongside Python, there are a host of other tools and technologies in use: 

- `Twisted <http://twistedmatrix.com>`_, as the basis for all application networking

- `Nevow <http://divmod.org/trac/wiki/DivmodNevow>`_ for much of the Web-based UI

- `MochiKit <http://www.mochikit.com>`_ for Javascript-based browser functionality

- `PyDot <http://dkbza.org/pydot.html>`_ for dependency graph rendering, and to draw workflow diagrams for our integrated workflow editor.  PyDot relies on `graphviz <http://www.graphviz.org>`_ and `pyparsing <http://pyparsing.wikispaces.com>`_

- `Python for Windows extensions <http://sourceforge.net/projects/pywin32/>`_ for client-side integration with MS Office (Project, Excel, Word)

- `Jabber <http://www.jabber.org>`_ for backoffice component interaction and desktop-to-web integration

- `Wildfire <http://www.jivesoftware.org/wildfire/>`_ as our backend XMPP Server

- `wxPython <http://www.wxpython.org>`_ for the Local Client used in MS Office import/export

- We provide an integrated `Subversion <http://subversion.tigris.org>`_ source code repository

- `PostgreSQL <http://www.postgresql.org>`_ and `SQLite <http://www.sqlite.org>`_ for data management

- Last, but certainly not least, `VIM <http://vim.sf.net>`_ :)

Parting thoughts about Python
-----------------------------

We are very happy with the development velocity and runtime performance that
we're getting with Python. Building our application atop Twisted imposed a bit
of a learning curve, but well worth it since it enables ProjectPipe to be a
true multi-protocol application, speaking HTTP and XMPP/Jabber.

If Python had a Just-in-Time (JIT) compiler, then we would not have had
occasional misgivings while worrying about hitting performance snags. Java's
JIT provides much better performance than Python when executing complex
algorithms.

The one problem that I see with Python is that there isn't a single dominant
web application development framework / paradigm at the moment. However, we're
pretty optimistic that `TurboGears <http://www.turbogears.org>`_ is going to become the long-term de facto
standard for building web applications in Python, and Botonomy is currently
building out consulting and training offerings around the TurboGears stack.
But Twisted is still the way to go for general network programming or
multi-protocol web-centric applications.

Links
-----

- `ProjectPipe.com Product Website <http://www.projectpipe.com>`_

- `Botonomy Website <http://botonomy.com>`_

- `Approach.Botonomy.Com <http://approach.botonomy.com>`_: Project Management and Software Development Best Practices

- `Mike Coyle's Weblog <http://mcoyle.botonomy.com>`_

- `Christian Simms' Weblog <http://csimms.botonomy.com>`_

About the Authors
-----------------

Mike Coyle and Christian Simms are the founders of `Botonomy LLC <http://botonomy.com>`_, a small
technology firm outside Philadelphia, PA.