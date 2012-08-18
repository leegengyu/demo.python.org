**MISSING**
**MISSING**

MayaVi Uses Python for Scientific Data Visualization
====================================================

**MISSING**
**MISSING**
**Category:**  Software Development, Science

**Keywords:**  Rapid Application Development, Knowledge Management, Scientific Programming

**Title:**  MayaVi Uses Python for Scientific Data Visualization

**Author:**   Prabhu Ramachandran

**Date:**   2003/01/16 21:42:26

**Website:**  `http://mayavi.sf.net/ <http://mayavi.sf.net/>`_

**Summary:**  MayaVi is an open source, scientific data visualization tool written entirely in Python. Coded in spare time by a single developer, MayaVi is now used by thousands of researchers and scientists around the world.

**Logo:**  .. image:: /files/success/mayavi/logo.gif    :alt: /files/success/mayavi/logo.gif

Background
----------

`MayaVi <http://mayavi.sf.net/>`_ is an open source scientific data visualization tool written
entirely in Python.

I started work on MayaVi in 2000.  At that time, a few colleagues of
mine needed to visualize their computational fluid dynamics (CFD) data
but the only suitable tools available were commercial, closed source
programs that were prohibitively expensive.

We looked at some open source tools as alternatives.  OpenDX had just
been released to the public and at that time was hard for me to get up
and running.  OpenDX was also a fairly complex system with a steep
learning curve.

Another visualization/graphics library, `VTK <http://www.vtk.org/>`_, was also available as
open source.  VTK is an extremely powerful visualization library written
in C++.  It is very portable and runs on various flavors of Unix,
Windows, and recently on Mac OS X.

VTK was chosen as the most appropriate solution, but it was not enough
to solve the problem at hand.  An application was needed on top of the
VTK library before non-programmers equipped only with specialized
domain knowledge could sit at a computer and visualize their data.

Python Chosen
-------------

Although most of my previous experience was in C and C++, I felt that
another language might be a better choice for quickly developing a
graphical user interface.  VTK is written in C++, but it has also been
wrapped for Python, Tcl and Java.  I took a look at each of those.

I ruled out Tcl because I felt Python's syntax was much cleaner and
because I had heard that large Tcl programs could be hard to maintain.
Java had the disadvantage of requiring compilation with each change in
the code, and the ability to run code in any recent browser was of no
use for this project. Java's verbose syntax as compared to Python was
also a point against it. Python was just as portable as Java and a much
easier to learn and use language. I'd also read the Python tutorial,
seen various Python programs and liked the language very much for its
simplicity, object oriented nature, dynamic data typing, and large
standard library.

Starting with a few simple Python scripts using VTK, I was able to get
my colleagues up and running fairly quickly with a few custom CFD
visualization scripts.  At this time I was still learning Python and
Tkinter (the GUI toolkit used in MayaVi) and created a GUI based tool
called VTK-CFD in June 2000.  This went through several rounds of
improvements until I eventually completely re-wrote it and released
MayaVi in May 2001.

Results
-------

MayaVi was written in 100% pure Python and by virtue of VTK, Python,
and Tkinter's portability, it works on Linux, Unix, and Windows.
Python turned out to be simple, easy to learn, and yet extremely
powerful.  Its interactive interpreter was a huge plus when learning
and experimenting.  It also has excellent freely available
documentation.

I found the development cycle extremely fast because Python is both
object oriented and interpreted.  The program can be well-designed
from an OO standpoint, and thus more maintainable, but there is no
compilation to wait for each time you make alterations to your code.

Python's readability and dynamic typing made it even easier to write,
maintain, and extend the code. I never had to worry about types, which
let me focus on the problem at hand rather than wrestle with the
language and its syntax. This made me much more productive than I was
with C and C++. For example, I was able to write a complete VTK
documentation browser with GUI and search engine in just 400 lines of
code.

.. image:: /files/success/mayavi/mpss0-half.jpg
   :alt: Mayavi Screen Shot

*Flow past a cylindrical post, showing configuration dialog, VTK
pipeline, and VTK documentation browser. Data courtesy of NASA.*
`Zoom in </files/success/mayavi/mpss0.png>`_

Excellent support for introspection, coupled with a comprehensive
standard library, made it easy to write data-driven code like the
vtkPipeline browser.  This automatically generates a GUI at runtime
that displays the VTK graphics pipeline.  It also generates a GUI
configuration dialog for any VTK object by parsing the object's
methods with Python's regular expression module, categorizing it, and
building the GUI accordingly.  This code is also used in MayaVi's
persistence mechanism, which can save most VTK objects to disk by
inspecting them at runtime.  The use of introspection to write
data-driven modules such as these avoided substantial amounts of
manual coding, and makes MayaVi self-extending as additional VTK
objects are defined.

Since Python is a scripting language, it was the natural choice for an
extension language for MayaVi.  As a result, MayaVi isn't just written
in Python but can also be scripted by end users working in Python, in order
to extend it with additional useful functionality.

I'm not a software developer or a computer scientist. Neither am I a
graphics expert.  While I did have a good bit of programming
experience with C/C++, I knew very little Python when I started on
this project.  Yet, I was able to learn Python using only its tutorial
and the standard Python documentation, and then could quickly develop
a substantial application.  I was pleased that Python could be learned
so easily and then so readily applied to non-trivial tasks.

It is important to note that this project was only a spare time
activity for me, which means that I had very little sustained time to
work on it.  I was the sole developer and I had to write the code,
maintain the web pages, write the documentation, and answer user
questions all by myself.

Even so, I was able to write about 16,000 lines of Python code in the
equivalent of about 4 months of full time effort and have produced a
successful end product.  This effort was spread over about 5 versions
of VTK-CFD and 3 versions of MayaVi.  MayaVi has been downloaded over
12,000 times from SourceForge, with over 3,500 downloads of the latest
release in a three months time period. There are now thousands of
users all over the world applying MayaVi in many research fields. It
has recently been packaged for Debian Linux and was included in its
latest release, Woody.

Conclusion
----------

If it weren't for Python, MayaVi would not exist.  Programming in
Python is such a pleasure and so easy that even a spare time project
can be very successful in doing what it set out to do.  There were no
major porting issues and MayaVi runs perfectly well under Linux, Unix,
and Windows with very little modifications made by me.  Overall it has
been a wonderful experience with Python.  I've learned so much, become
very productive with it, and hopefully have also made others
productive with the tools I have been able to write.

About the Author
----------------

*Prabhu Ramachandran is an Aerospace Engineer and PhD student at the
Indian Institute of Technology - Madras, Chennai, India.  An OSS and
GNU/Linux advocate, Prabhu has also contributed to VTK, the open
source 3D computer graphics, image processing, and visualization
system on which MayaVi is based.*