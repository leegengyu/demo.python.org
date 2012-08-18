**MISSING**
**MISSING**

A Custom Image Viewing Game for an Autistic Child
=================================================

**MISSING**
**MISSING**
**Category:**  Software Development

**Keywords:**  Game Development, Assistive Technologies

**Title:**  A Custom Image Viewing Game for an Autistic Child

**Author:**   Ned Batchelder

**Date:**   2003/01/17 15:59:01

**Website:**  `http://www.nedbatchelder.com <http://www.nedbatchelder.com>`_

**Summary:**  Ned Batchelder describes a custom image viewing game he wrote for his autistic son Nat, in the process showing off some of Python's language features.

Introduction
------------

My son Nat is autistic.  He likes to look at pictures of familiar
places, things, and people.  We bought a digital camera so we could take
as many pictures of as many ordinary things as we wanted, without having
to worry about the cost and bother of film and development.  Nat's
tastes are difficult to predict, so we might take pictures of a subject
certain to please him, only to find that he has no interest in them
at all.  We wanted to be able to cast a wide net while taking
pictures, to be certain to capture the images that would interest him.

Once we had the camera, we took hundreds of pictures, and showed Nat how
to look through them on the computer using an off-the-shelf image viewer
called ThumbsPlus.  Watching Nat flip through pictures, though, I noticed
something: once he became familiar with the sequence of the pictures, he
was clicking on the pictures as if it mattered where he clicked.  The
image viewer didn't care: any click on the picture would show the next
picture.  But if Nat knew that the next picture was of a thing off to
the left of the current picture, he would click on the left of the
image.  If he knew the next picture was through a door at the right of
the picture, he would click on the door.  He's played a number of kid's
adventure games, such as Pajama Sam, and knew about this style of
navigation.  Even in a program that didn't use that navigation style, he
had begun using it as if it did.

So I thought, why not make an image viewer that worked his way?  Why not
write a program that lets me build picture environments from our life,
and lets Nat navigate through them in the style he wanted?

.. image:: /files/success/natsworld/natsworld-web.jpg
   :alt: Natworld Screen Shot

*One of over 1500 images in Natsworld.  The user interface is simply a
set of directional cursors (near center)* `Zoom in </files/success/natsworld/natsworld.jpg>`_

Choosing Python
---------------

I had used Python for small scripting projects before, and liked its
quick-off-the-blocks feel.  It would provide me with a malleable
environment in which to experiment with features, to see what Nat would
find interesting.  Although this was an at-home project to be used only
by my son, it shared issues with larger, supposedly more serious
projects: unclear requirements, unpredictable customers, and limited
developer resources.  The most important concern to me in choosing the
development tools was my productivity.  Since this was &quot;after-hours&quot;
work, my time and attention would be stretched thin, and I wanted to be
able to focus on the user experience, not build environments, memory
management, and the like.

I looked for existing software, and found lots of interesting examples
at pygame (www.pygame.org).  Pygame provided all the functions I'd need
for image manipulation and display management, and there were a few
existing projects there that provided useful examples.  Pyzzle almost
provided what I needed, but wasn't as well-organized internally as I
would have liked to be able to quickly experiment with new features.

Implementation
--------------

Using the existing examples to help guide my pygame use, I created a new
framework for my program.  My program, which I named simply &quot;Nat's
World&quot;, would provide a virtual world for exploration.  It would work
the way Nat expected it to, providing a simple exploration environment
similar to games like Myst; clicking on the left of the screen would
turn you left, clicking center would move you forward, and so forth.

At its simplest, the entire environment was simply a set of nodes, each
of which had an image to display, and a list of other connected nodes
to navigate to. One physical location in the world is represented by a
number of nodes, one for each direction to face. These nodes together
are called a &quot;spot&quot;. Over time, this model was extended to add features
to the environment, but this simple model got me off the ground. Python
gave me a clean object-oriented basis for building my Node class, and
pygame provided the primitives for displaying images, creating cursors,
and collecting input.

One of the biggest challenges was deciding among ways to organize the
description of the world. On the one hand, I could have created a
descriptive language for the structure of the world, and written an
interpreter to read the description and build the in-memory structures
on which the game would run. This would have been a fairly large
effort, and would have required me to formalize all of the structures
that could have appeared in a world. It also would have meant a longer
delay before I had something that Nat could actually use. On the other
hand, I could have simply used Python statements to construct the
structures directly. This would have been tedious and error-prone.

As a handy middle ground, I used Python statements to build the world,
but made heavy use of utility functions and classes to provide
short-cuts for common structures. For example, my images are all stored
in directories named by date, and I would have had to enter an image
filename for each node.  The ImgShortcut class made this simple.
Defining the ``__call__`` method allowed me to play with the syntax of
Python to get the effect I wanted:

.. code-block::

    class ImgShortcut:
        def __init__(self, fmt):
            self.fmt = fmt

        def __call__(self, arg):
            return self.fmt % (arg)

    nov4 =  ImgShortcut(r'C:\img\vol3\20011104\dscf%04d.jpg')
    nov10 = ImgShortcut(r'C:\img\vol3\20011110\dscf%04d.jpg')

    >>> print nov4(17)
    c:\img\vol3\20011104\dscf0017.jpg

As another example, many spots in the world shared the same four-node
structure: one for the north view, one for the west view, and so on.
Using Python's keyword argument syntax, I was able to write a function to
build this common spot type:

.. code-block::

    def nesw(name, **data):
        &quot;&quot;&quot;
        Make four nodes for n, e, w, s from a location.
        Keys:
            images: ni, ei, wi, si.
            destinations: n, e, w, s.
        &quot;&quot;&quot;
        # (code omitted)

The first argument is the base name for the new nodes (the node names
are made by appending &quot;:n&quot;, &quot;:w&quot;, etc).  The remaining arguments are
specified by keyword: ni is the image name for the north node, n is the
node to the north; wi is the image for the west node, w is the node to
the west, and so on.  Now I can make a spot with a simple short-hand
syntax:

.. code-block::

    nesw('front43',
        ni = nov4(17),
        ei = nov4(18),   e = 'allerton_hawthorne:e',
        si = nov10(381), s = 'hall:s',
        wi = nov4(16),   w = 'markliesl:w'
    )

Because of the keyword syntax, I can omit arguments that don't apply for
the particular spot.  Now I have an almost declarative syntax that is
handy for creating common structures, but without having to write an
interpreter for a new mini-language.  And if I have an unusual case that
needs full Python, it is available to me.

The world and the program to support it grew in parallel.  As I came up
with new ideas for structures for spots, I would write new utility
functions like nesw() to create them easily.  I could watch Nat play the
game, see what he wanted it to do, and add features quickly. Many of
Python's features (interpreted code, object orientation, garbage
collection, lists and dictionaries) supported this rapid turn-around.

The Node class was extended and subclassed to create new types of
nodes. For example, I added a MenuNode subclass to handle on-screen
menus of destinations. This allowed clicking on the car, then choosing
where you want to drive. Transitions between nodes were added to make
the effect more pleasing. Clicking on the stereo produced a menu of
songs to play (via pygame, of course).

Results
-------

At this point, the total size of the source is about 1400 lines of code,
plus 1300 lines describing the world, which is currently over 1500
nodes.

When I show Nat's World to friends, they always talk about how great it
would be if I could make something like it possible for other people.
I've thought about writing a WorldBuilder application. It would let a
non-technical person use a GUI to browse images, and connect them into
a world of nodes. It would be a nice project to build, and an even
nicer one to have since I could use it myself to extend Nat's World. I
don't know if I'll ever have the time and focus to build such a thing
in my spare time, but if I did, I know Python would be the tool for the
job.

About the Author
----------------

*Ned Batchelder is a software engineer from Brookline, MA. His wife and
three boys all love playing Nat's World. His web site is
http://www.nedbatchelder.com.*