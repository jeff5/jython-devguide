.. _documenting:

Documenting Python
==================

The Python language has a substantial body of documentation, much of it
contributed by various authors. The markup used for the Python documentation is
`reStructuredText`_, developed by the `docutils`_ project, amended by custom
directives and using a toolset named `Sphinx`_ to post-process the HTML output.

This document describes the style guide for our documentation as well as the
custom reStructuredText markup introduced by Sphinx to support Python
documentation and how it should be used.

.. _reStructuredText: http://docutils.sf.net/rst.html
.. _docutils: http://docutils.sf.net/
.. _Sphinx: http://sphinx.pocoo.org/

.. note::

   If you're interested in contributing to Python's documentation, there's no
   need to write reStructuredText if you're not so inclined; plain text
   contributions are more than welcome as well.  Send an e-mail to
   docs@python.org or open an issue on the :ref:`tracker <reporting-bugs>`.


Introduction
============

Python's documentation has long been considered to be good for a free
programming language.  There are a number of reasons for this, the most
important being the early commitment of Python's creator, Guido van Rossum, to
providing documentation on the language and its libraries, and the continuing
involvement of the user community in providing assistance for creating and
maintaining documentation.

The involvement of the community takes many forms, from authoring to bug reports
to just plain complaining when the documentation could be more complete or
easier to use.

This document is aimed at authors and potential authors of documentation for
Python.  More specifically, it is for people contributing to the standard
documentation and developing additional documents using the same tools as the
standard documents.  This guide will be less useful for authors using the Python
documentation tools for topics other than Python, and less useful still for
authors not using the tools at all.

If your interest is in contributing to the Python documentation, but you don't
have the time or inclination to learn reStructuredText and the markup structures
documented here, there's a welcoming place for you among the Python contributors
as well.  Any time you feel that you can clarify existing documentation or
provide documentation that's missing, the existing documentation team will
gladly work with you to integrate your text, dealing with the markup for you.
Please don't let the material in this document stand between the documentation
and your desire to help out!


Style guide
===========

The Python documentation should follow the `Apple Publications Style Guide`_
wherever possible. This particular style guide was selected mostly because it
seems reasonable and is easy to get online.

Topics which are either not covered in Apple's style guide or treated
differently in Python documentation will be discussed in this
document.

Use of whitespace
-----------------

All reST files use an indentation of 3 spaces; no tabs are allowed.  The
maximum line length is 80 characters for normal text, but tables, deeply
indented code samples and long links may extend beyond that.  Code example
bodies should use normal Python 4-space indentation.

Make generous use of blank lines where applicable; they help grouping things
together.

A sentence-ending period may be followed by one or two spaces; while reST
ignores the second space, it is customarily put in by some users, for example
to aid Emacs' auto-fill mode.

Footnotes
---------

Footnotes are generally discouraged, though they may be used when they are the
best way to present specific information. When a footnote reference is added at
the end of the sentence, it should follow the sentence-ending punctuation. The
reST markup should appear something like this::

    This sentence has a footnote reference. [#]_ This is the next sentence.

Footnotes should be gathered at the end of a file, or if the file is very long,
at the end of a section. The docutils will automatically create backlinks to
the footnote reference.

Footnotes may appear in the middle of sentences where appropriate.

Capitalization
--------------

.. sidebar:: Sentence case

   Sentence case is a set of capitalization rules used in English
   sentences: the first word is always capitalized and other words are
   only capitalized if there is a specific rule requiring it.

Apple style guide recommends the use of title case in section titles.
However, rules for which words should be capitalized in title case
vary greatly between publications.

In Python documentation, use of sentence case in section titles is
preferable, but consistency within a unit is more important than
following this rule.  If you add a section to the chapter where most
sections are in title case you can either convert all titles to
sentence case or use the dominant style in the new section title.

Sentences that start with a word for which specific rules require
starting it with a lower case letter should be avoided in titles and
elsewhere.

.. note::

   Sections that describe a library module often have titles in the
   form of "modulename --- Short description of the module."  In this
   case, the description should be capitalized as a stand-alone
   sentence.

Many special names are used in the Python documentation, including the names of
operating systems, programming languages, standards bodies, and the like. Most
of these entities are not assigned any special markup, but the preferred
spellings are given here to aid authors in maintaining the consistency of
presentation in the Python documentation.

Other terms and words deserve special mention as well; these conventions should
be used to ensure consistency throughout the documentation:

CPU
   For "central processing unit." Many style guides say this should be
   spelled out on the first use (and if you must use it, do so!). For
   the Python documentation, this abbreviation should be avoided since
   there's no reasonable way to predict which occurrence will be the
   first seen by the reader. It is better to use the word "processor"
   instead.

POSIX
   The name assigned to a particular group of standards. This is always
   uppercase.

Python
   The name of our favorite programming language is always capitalized.

reST
   For "reStructuredText," an easy to read, plaintext markup syntax
   used to produce Python documentation.  When spelled out, it is
   always one word and both forms start with a lower case 'r'.

Unicode
   The name of a character coding system. This is always written
   capitalized.

Unix
   The name of the operating system developed at AT&T Bell Labs in the early
   1970s.

Affirmative Tone
----------------

The documentation focuses on affirmatively stating what the language does and
how to use it effectively.

Except for certain security risks or segfault risks, the docs should avoid
wording along the lines of "feature x is dangerous" or "experts only".  These
kinds of value judgments belong in external blogs and wikis, not in the core
documentation.

Bad example (creating worry in the mind of a reader):

    Warning: failing to explicitly close a file could result in lost data or
    excessive resource consumption.  Never rely on reference counting to
    automatically close a file.

Good example (establishing confident knowledge in the effective use of the language):

    A best practice for using files is use a try/finally pair to explicitly
    close a file after it is used.  Alternatively, using a with-statement can
    achieve the same effect.  This assures that files are flushed and file
    descriptor resources are released in a timely manner.

Economy of Expression
---------------------

More documentation is not necessarily better documentation.  Err on the side
of being succinct.

It is an unfortunate fact that making documentation longer can be an impediment
to understanding and can result in even more ways to misread or misinterpret the
text.  Long descriptions full of corner cases and caveats can create the
impression that a function is more complex or harder to use than it actually is.

The documentation for :func:`super` is an example of where a good deal of
information was condensed into a few short paragraphs.  Discussion of
:func:`super` could have filled a chapter in a book, but it is often easier to
grasp a terse description than a lengthy narrative.


Code Examples
-------------

Short code examples can be a useful adjunct to understanding.  Readers can often
grasp a simple example more quickly than they can digest a formal description in
prose.

People learn faster with concrete, motivating examples that match the context of
a typical use case.  For instance, the :func:`str.rpartition` method is better
demonstrated with an example splitting the domain from a URL than it would be
with an example of removing the last word from a line of Monty Python dialog.

The ellipsis for the :attr:`sys.ps2` secondary interpreter prompt should only be
used sparingly, where it is necessary to clearly differentiate between input
lines and output lines.  Besides contributing visual clutter, it makes it
difficult for readers to cut-and-paste examples so they can experiment with
variations.

Code Equivalents
----------------

Giving pure Python code equivalents (or approximate equivalents) can be a useful
adjunct to a prose description.  A documenter should carefully weigh whether the
code equivalent adds value.

A good example is the code equivalent for :func:`all`.  The short 4-line code
equivalent is easily digested; it re-emphasizes the early-out behavior; and it
clarifies the handling of the corner-case where the iterable is empty.  In
addition, it serves as a model for people wanting to implement a commonly
requested alternative where :func:`all` would return the specific object
evaluating to False whenever the function terminates early.

A more questionable example is the code for :func:`itertools.groupby`.  Its code
equivalent borders on being too complex to be a quick aid to understanding.
Despite its complexity, the code equivalent was kept because it serves as a
model to alternative implementations and because the operation of the "grouper"
is more easily shown in code than in English prose.

An example of when not to use a code equivalent is for the :func:`oct` function.
The exact steps in converting a number to octal doesn't add value for a user
trying to learn what the function does.

Audience
--------

The tone of the tutorial (and all the docs) needs to be respectful of the
reader's intelligence.  Don't presume that the readers are stupid.  Lay out the
relevant information, show motivating use cases, provide glossary links, and do
your best to connect-the-dots, but don't talk down to them or waste their time.

The tutorial is meant for newcomers, many of whom will be using the tutorial to
evaluate the language as a whole.  The experience needs to be positive and not
leave the reader with worries that something bad will happen if they make a
misstep.  The tutorial serves as guide for intelligent and curious readers,
saving details for the how-to guides and other sources.

Be careful accepting requests for documentation changes from the rare but vocal
category of reader who is looking for vindication for one of their programming
errors ("I made a mistake, therefore the docs must be wrong ...").  Typically,
the documentation wasn't consulted until after the error was made.  It is
unfortunate, but typically no documentation edit would have saved the user from
making false assumptions about the language ("I was surprised by ...").


.. _Apple Publications Style Guide: http://developer.apple.com/mac/library/documentation/UserExperience/Conceptual/APStyleGuide/APSG_2009.pdf


reStructuredText Primer
=======================

This section is a brief introduction to reStructuredText (reST) concepts and
syntax, intended to provide authors with enough information to author documents
productively.  Since reST was designed to be a simple, unobtrusive markup
language, this will not take too long.

.. seealso::

    The authoritative `reStructuredText User
    Documentation <http://docutils.sourceforge.net/rst.html>`_.


Paragraphs
----------

The paragraph is the most basic block in a reST document.  Paragraphs are simply
chunks of text separated by one or more blank lines.  As in Python, indentation
is significant in reST, so all lines of the same paragraph must be left-aligned
to the same level of indentation.


Inline markup
-------------

The standard reST inline markup is quite simple: use

* one asterisk: ``*text*`` for emphasis (italics),
* two asterisks: ``**text**`` for strong emphasis (boldface), and
* backquotes: ````text```` for code samples.

If asterisks or backquotes appear in running text and could be confused with
inline markup delimiters, they have to be escaped with a backslash.

Be aware of some restrictions of this markup:

* it may not be nested,
* content may not start or end with whitespace: ``* text*`` is wrong,
* it must be separated from surrounding text by non-word characters.  Use a
  backslash escaped space to work around that: ``thisis\ *one*\ word``.

These restrictions may be lifted in future versions of the docutils.

reST also allows for custom "interpreted text roles"', which signify that the
enclosed text should be interpreted in a specific way.  Sphinx uses this to
provide semantic markup and cross-referencing of identifiers, as described in
the appropriate section.  The general syntax is ``:rolename:`content```.


Lists and Quotes
----------------

List markup is natural: just place an asterisk at the start of a paragraph and
indent properly.  The same goes for numbered lists; they can also be
automatically numbered using a ``#`` sign::

   * This is a bulleted list.
   * It has two items, the second
     item uses two lines.

   1. This is a numbered list.
   2. It has two items too.

   #. This is a numbered list.
   #. It has two items too.


Nested lists are possible, but be aware that they must be separated from the
parent list items by blank lines::

   * this is
   * a list

     * with a nested list
     * and some subitems

   * and here the parent list continues

Definition lists are created as follows::

   term (up to a line of text)
      Definition of the term, which must be indented

      and can even consist of multiple paragraphs

   next term
      Description.


Paragraphs are quoted by just indenting them more than the surrounding
paragraphs.


Source Code
-----------

Literal code blocks are introduced by ending a paragraph with the special marker
``::``.  The literal block must be indented::

   This is a normal text paragraph. The next paragraph is a code sample::

      It is not processed in any way, except
      that the indentation is removed.

      It can span multiple lines.

   This is a normal text paragraph again.

The handling of the ``::`` marker is smart:

* If it occurs as a paragraph of its own, that paragraph is completely left
  out of the document.
* If it is preceded by whitespace, the marker is removed.
* If it is preceded by non-whitespace, the marker is replaced by a single
  colon.

That way, the second sentence in the above example's first paragraph would be
rendered as "The next paragraph is a code sample:".


Hyperlinks
----------

External links
^^^^^^^^^^^^^^

Use ```Link text <http://target>`_`` for inline web links.  If the link text
should be the web address, you don't need special markup at all, the parser
finds links and mail addresses in ordinary text.

Internal links
^^^^^^^^^^^^^^

Internal linking is done via a special reST role, see the section on specific
markup, :ref:`doc-ref-role`.


Sections
--------

Section headers are created by underlining (and optionally overlining) the
section title with a punctuation character, at least as long as the text::

   =================
   This is a heading
   =================

Normally, there are no heading levels assigned to certain characters as the
structure is determined from the succession of headings.  However, for the
Python documentation, we use this convention:

* ``#`` with overline, for parts
* ``*`` with overline, for chapters
* ``=``, for sections
* ``-``, for subsections
* ``^``, for subsubsections
* ``"``, for paragraphs


Explicit Markup
---------------

"Explicit markup" is used in reST for most constructs that need special
handling, such as footnotes, specially-highlighted paragraphs, comments, and
generic directives.

An explicit markup block begins with a line starting with ``..`` followed by
whitespace and is terminated by the next paragraph at the same level of
indentation.  (There needs to be a blank line between explicit markup and normal
paragraphs.  This may all sound a bit complicated, but it is intuitive enough
when you write it.)


Directives
----------

A directive is a generic block of explicit markup.  Besides roles, it is one of
the extension mechanisms of reST, and Sphinx makes heavy use of it.

Basically, a directive consists of a name, arguments, options and content. (Keep
this terminology in mind, it is used in the next chapter describing custom
directives.)  Looking at this example, ::

   .. function:: foo(x)
                 foo(y, z)
      :bar: no

      Return a line of text input from the user.

``function`` is the directive name.  It is given two arguments here, the
remainder of the first line and the second line, as well as one option ``bar``
(as you can see, options are given in the lines immediately following the
arguments and indicated by the colons).

The directive content follows after a blank line and is indented relative to the
directive start.


Footnotes
---------

For footnotes, use ``[#]_`` to mark the footnote location, and add the footnote
body at the bottom of the document after a "Footnotes" rubric heading, like so::

   Lorem ipsum [#]_ dolor sit amet ... [#]_

   .. rubric:: Footnotes

   .. [#] Text of the first footnote.
   .. [#] Text of the second footnote.

You can also explicitly number the footnotes for better context.


Comments
--------

Every explicit markup block which isn't a valid markup construct (like the
footnotes above) is regarded as a comment.


Source encoding
---------------

Since the easiest way to include special characters like em dashes or copyright
signs in reST is to directly write them as Unicode characters, one has to
specify an encoding:

All Python documentation source files must be in UTF-8 encoding, and the HTML
documents written from them will be in that encoding as well.


Gotchas
-------

There are some problems one commonly runs into while authoring reST documents:

* **Separation of inline markup:** As said above, inline markup spans must be
  separated from the surrounding text by non-word characters, you have to use
  an escaped space to get around that.


Additional Markup Constructs
============================

Sphinx adds a lot of new directives and interpreted text roles to standard reST
markup.  This section contains the reference material for these facilities.
Documentation for "standard" reST constructs is not included here, though
they are used in the Python documentation.

.. note::

   This is just an overview of Sphinx' extended markup capabilities; full
   coverage can be found in `its own documentation
   <http://sphinx.pocoo.org/contents.html>`_.


Meta-information markup
-----------------------

.. describe:: sectionauthor

   Identifies the author of the current section.  The argument should include
   the author's name such that it can be used for presentation (though it isn't)
   and email address.  The domain name portion of the address should be lower
   case.  Example::

      .. sectionauthor:: Guido van Rossum <guido@python.org>

   Currently, this markup isn't reflected in the output in any way, but it helps
   keep track of contributions.


Module-specific markup
----------------------

The markup described in this section is used to provide information about a
module being documented.  Each module should be documented in its own file.
Normally this markup appears after the title heading of that file; a typical
file might start like this::

   :mod:`parrot` -- Dead parrot access
   ===================================

   .. module:: parrot
      :platform: Unix, Windows
      :synopsis: Analyze and reanimate dead parrots.
   .. moduleauthor:: Eric Cleese <eric@python.invalid>
   .. moduleauthor:: John Idle <john@python.invalid>

As you can see, the module-specific markup consists of two directives, the
``module`` directive and the ``moduleauthor`` directive.

.. describe:: module

   This directive marks the beginning of the description of a module, package,
   or submodule. The name should be fully qualified (i.e. including the
   package name for submodules).

   The ``platform`` option, if present, is a comma-separated list of the
   platforms on which the module is available (if it is available on all
   platforms, the option should be omitted).  The keys are short identifiers;
   examples that are in use include "IRIX", "Mac", "Windows", and "Unix".  It is
   important to use a key which has already been used when applicable.

   The ``synopsis`` option should consist of one sentence describing the
   module's purpose -- it is currently only used in the Global Module Index.

   The ``deprecated`` option can be given (with no value) to mark a module as
   deprecated; it will be designated as such in various locations then.

.. describe:: moduleauthor

   The ``moduleauthor`` directive, which can appear multiple times, names the
   authors of the module code, just like ``sectionauthor`` names the author(s)
   of a piece of documentation.  It too does not result in any output currently.

.. note::

   It is important to make the section title of a module-describing file
   meaningful since that value will be inserted in the table-of-contents trees
   in overview files.


Information units
-----------------

There are a number of directives used to describe specific features provided by
modules.  Each directive requires one or more signatures to provide basic
information about what is being described, and the content should be the
description.  The basic version makes entries in the general index; if no index
entry is desired, you can give the directive option flag ``:noindex:``.  The
following example shows all of the features of this directive type::

    .. function:: spam(eggs)
                  ham(eggs)
       :noindex:

       Spam or ham the foo.

The signatures of object methods or data attributes should not include the
class name, but be nested in a class directive.  The generated files will
reflect this nesting, and the target identifiers (for HTML output) will use
both the class and method name, to enable consistent cross-references.  If you
describe methods belonging to an abstract protocol such as context managers,
use a class directive with a (pseudo-)type name too to make the
index entries more informative.

The directives are:

.. describe:: c:function

   Describes a C function. The signature should be given as in C, e.g.::

      .. c:function:: PyObject* PyType_GenericAlloc(PyTypeObject *type, Py_ssize_t nitems)

   This is also used to describe function-like preprocessor macros.  The names
   of the arguments should be given so they may be used in the description.

   Note that you don't have to backslash-escape asterisks in the signature,
   as it is not parsed by the reST inliner.

.. describe:: c:member

   Describes a C struct member. Example signature::

      .. c:member:: PyObject* PyTypeObject.tp_bases

   The text of the description should include the range of values allowed, how
   the value should be interpreted, and whether the value can be changed.
   References to structure members in text should use the ``member`` role.

.. describe:: c:macro

   Describes a "simple" C macro.  Simple macros are macros which are used
   for code expansion, but which do not take arguments so cannot be described as
   functions.  This is not to be used for simple constant definitions.  Examples
   of its use in the Python documentation include :c:macro:`PyObject_HEAD` and
   :c:macro:`Py_BEGIN_ALLOW_THREADS`.

.. describe:: c:type

   Describes a C type. The signature should just be the type name.

.. describe:: c:var

   Describes a global C variable.  The signature should include the type, such
   as::

      .. cvar:: PyObject* PyClass_Type

.. describe:: data

   Describes global data in a module, including both variables and values used
   as "defined constants."  Class and object attributes are not documented
   using this directive.

.. describe:: exception

   Describes an exception class.  The signature can, but need not include
   parentheses with constructor arguments.

.. describe:: function

   Describes a module-level function.  The signature should include the
   parameters, enclosing optional parameters in brackets.  Default values can be
   given if it enhances clarity.  For example::

      .. function:: repeat([repeat=3[, number=1000000]])

   Object methods are not documented using this directive. Bound object methods
   placed in the module namespace as part of the public interface of the module
   are documented using this, as they are equivalent to normal functions for
   most purposes.

   The description should include information about the parameters required and
   how they are used (especially whether mutable objects passed as parameters
   are modified), side effects, and possible exceptions.  A small example may be
   provided.

.. describe:: decorator

   Describes a decorator function.  The signature should *not* represent the
   signature of the actual function, but the usage as a decorator.  For example,
   given the functions

   .. code-block:: python

      def removename(func):
          func.__name__ = ''
          return func

      def setnewname(name):
          def decorator(func):
              func.__name__ = name
              return func
          return decorator

   the descriptions should look like this::

      .. decorator:: removename

         Remove name of the decorated function.

      .. decorator:: setnewname(name)

         Set name of the decorated function to *name*.

   There is no ``deco`` role to link to a decorator that is marked up with
   this directive; rather, use the ``:func:`` role.

.. describe:: class

   Describes a class.  The signature can include parentheses with parameters
   which will be shown as the constructor arguments.

.. describe:: attribute

   Describes an object data attribute.  The description should include
   information about the type of the data to be expected and whether it may be
   changed directly.  This directive should be nested in a class directive,
   like in this example::

      .. class:: Spam

            Description of the class.

            .. data:: ham

               Description of the attribute.

   If is also possible to document an attribute outside of a class directive,
   for example if the documentation for different attributes and methods is
   split in multiple sections.  The class name should then be included
   explicitly::

      .. data:: Spam.eggs

.. describe:: method

   Describes an object method.  The parameters should not include the ``self``
   parameter.  The description should include similar information to that
   described for ``function``.  This directive should be nested in a class
   directive, like in the example above.

.. describe:: decoratormethod

   Same as ``decorator``, but for decorators that are methods.

   Refer to a decorator method using the ``:meth:`` role.

.. describe:: opcode

   Describes a Python :term:`bytecode` instruction.

.. describe:: cmdoption

   Describes a Python command line option or switch.  Option argument names
   should be enclosed in angle brackets.  Example::

      .. cmdoption:: -m <module>

         Run a module as a script.

.. describe:: envvar

   Describes an environment variable that Python uses or defines.


There is also a generic version of these directives:

.. describe:: describe

   This directive produces the same formatting as the specific ones explained
   above but does not create index entries or cross-referencing targets.  It is
   used, for example, to describe the directives in this document. Example::

      .. describe:: opcode

         Describes a Python bytecode instruction.


Showing code examples
---------------------

Examples of Python source code or interactive sessions are represented using
standard reST literal blocks.  They are started by a ``::`` at the end of the
preceding paragraph and delimited by indentation.

Representing an interactive session requires including the prompts and output
along with the Python code.  No special markup is required for interactive
sessions.  After the last line of input or output presented, there should not be
an "unused" primary prompt; this is an example of what *not* to do::

   >>> 1 + 1
   2
   >>>

Syntax highlighting is handled in a smart way:

* There is a "highlighting language" for each source file.  Per default,
  this is ``'python'`` as the majority of files will have to highlight Python
  snippets.

* Within Python highlighting mode, interactive sessions are recognized
  automatically and highlighted appropriately.

* The highlighting language can be changed using the ``highlightlang``
  directive, used as follows::

     .. highlightlang:: c

  This language is used until the next ``highlightlang`` directive is
  encountered.

* The values normally used for the highlighting language are:

  * ``python`` (the default)
  * ``c``
  * ``rest``
  * ``none`` (no highlighting)

* If highlighting with the current language fails, the block is not highlighted
  in any way.

Longer displays of verbatim text may be included by storing the example text in
an external file containing only plain text.  The file may be included using the
``literalinclude`` directive. [1]_ For example, to include the Python source file
:file:`example.py`, use::

   .. literalinclude:: example.py

The file name is relative to the current file's path.  Documentation-specific
include files should be placed in the ``Doc/includes`` subdirectory.


Inline markup
-------------

As said before, Sphinx uses interpreted text roles to insert semantic markup in
documents.

Names of local variables, such as function/method arguments, are an exception,
they should be marked simply with ``*var*``.

For all other roles, you have to write ``:rolename:`content```.

There are some additional facilities that make cross-referencing roles more
versatile:

* You may supply an explicit title and reference target, like in reST direct
  hyperlinks: ``:role:`title <target>``` will refer to *target*, but the link
  text will be *title*.

* If you prefix the content with ``!``, no reference/hyperlink will be created.

* For the Python object roles, if you prefix the content with ``~``, the link
  text will only be the last component of the target.  For example,
  ``:meth:`~Queue.Queue.get``` will refer to ``Queue.Queue.get`` but only
  display ``get`` as the link text.

  In HTML output, the link's ``title`` attribute (that is e.g. shown as a
  tool-tip on mouse-hover) will always be the full target name.

The following roles refer to objects in modules and are possibly hyperlinked if
a matching identifier is found:

.. describe:: mod

   The name of a module; a dotted name may be used.  This should also be used for
   package names.

.. describe:: func

   The name of a Python function; dotted names may be used.  The role text
   should not include trailing parentheses to enhance readability.  The
   parentheses are stripped when searching for identifiers.

.. describe:: data

   The name of a module-level variable or constant.

.. describe:: const

   The name of a "defined" constant.  This may be a C-language ``#define``
   or a Python variable that is not intended to be changed.

.. describe:: class

   A class name; a dotted name may be used.

.. describe:: meth

   The name of a method of an object.  The role text should include the type
   name and the method name.  A dotted name may be used.

.. describe:: attr

   The name of a data attribute of an object.

.. describe:: exc

   The name of an exception. A dotted name may be used.

The name enclosed in this markup can include a module name and/or a class name.
For example, ``:func:`filter``` could refer to a function named ``filter`` in
the current module, or the built-in function of that name.  In contrast,
``:func:`foo.filter``` clearly refers to the ``filter`` function in the ``foo``
module.

Normally, names in these roles are searched first without any further
qualification, then with the current module name prepended, then with the
current module and class name (if any) prepended.  If you prefix the name with a
dot, this order is reversed.  For example, in the documentation of the
:mod:`codecs` module, ``:func:`open``` always refers to the built-in function,
while ``:func:`.open``` refers to :func:`codecs.open`.

A similar heuristic is used to determine whether the name is an attribute of
the currently documented class.

The following roles create cross-references to C-language constructs if they
are defined in the API documentation:

.. describe:: c:data

   The name of a C-language variable.

.. describe:: c:func

   The name of a C-language function. Should include trailing parentheses.

.. describe:: c:macro

   The name of a "simple" C macro, as defined above.

.. describe:: c:type

   The name of a C-language type.

.. describe:: c:member

   The name of a C type member, as defined above.


The following role does possibly create a cross-reference, but does not refer
to objects:

.. describe:: token

   The name of a grammar token (used in the reference manual to create links
   between production displays).


The following role creates a cross-reference to the term in the glossary:

.. describe:: term

   Reference to a term in the glossary.  The glossary is created using the
   ``glossary`` directive containing a definition list with terms and
   definitions.  It does not have to be in the same file as the ``term``
   markup, in fact, by default the Python docs have one global glossary
   in the ``glossary.rst`` file.

   If you use a term that's not explained in a glossary, you'll get a warning
   during build.

---------

The following roles don't do anything special except formatting the text
in a different style:

.. describe:: command

   The name of an OS-level command, such as ``rm``.

.. describe:: dfn

   Mark the defining instance of a term in the text.  (No index entries are
   generated.)

.. describe:: envvar

   An environment variable.  Index entries are generated.

.. describe:: file

   The name of a file or directory.  Within the contents, you can use curly
   braces to indicate a "variable" part, for example::

      ... is installed in :file:`/usr/lib/python2.{x}/site-packages` ...

   In the built documentation, the ``x`` will be displayed differently to
   indicate that it is to be replaced by the Python minor version.

.. describe:: guilabel

   Labels presented as part of an interactive user interface should be marked
   using ``guilabel``.  This includes labels from text-based interfaces such as
   those created using :mod:`curses` or other text-based libraries.  Any label
   used in the interface should be marked with this role, including button
   labels, window titles, field names, menu and menu selection names, and even
   values in selection lists.

.. describe:: kbd

   Mark a sequence of keystrokes.  What form the key sequence takes may depend
   on platform- or application-specific conventions.  When there are no relevant
   conventions, the names of modifier keys should be spelled out, to improve
   accessibility for new users and non-native speakers.  For example, an
   *xemacs* key sequence may be marked like ``:kbd:`C-x C-f```, but without
   reference to a specific application or platform, the same sequence should be
   marked as ``:kbd:`Control-x Control-f```.

.. describe:: keyword

   The name of a Python keyword.  Using this role will generate a link to the
   documentation of the keyword.  ``True``, ``False`` and ``None`` do not use
   this role, but simple code markup (````True````), given that they're
   fundamental to the language and should be known to any programmer.

.. describe:: mailheader

   The name of an RFC 822-style mail header.  This markup does not imply that
   the header is being used in an email message, but can be used to refer to any
   header of the same "style."  This is also used for headers defined by the
   various MIME specifications.  The header name should be entered in the same
   way it would normally be found in practice, with the camel-casing conventions
   being preferred where there is more than one common usage. For example:
   ``:mailheader:`Content-Type```.

.. describe:: makevar

   The name of a :command:`make` variable.

.. describe:: manpage

   A reference to a Unix manual page including the section,
   e.g. ``:manpage:`ls(1)```.

.. describe:: menuselection

   Menu selections should be marked using the ``menuselection`` role.  This is
   used to mark a complete sequence of menu selections, including selecting
   submenus and choosing a specific operation, or any subsequence of such a
   sequence.  The names of individual selections should be separated by
   ``-->``.

   For example, to mark the selection "Start > Programs", use this markup::

      :menuselection:`Start --> Programs`

   When including a selection that includes some trailing indicator, such as the
   ellipsis some operating systems use to indicate that the command opens a
   dialog, the indicator should be omitted from the selection name.

.. describe:: mimetype

   The name of a MIME type, or a component of a MIME type (the major or minor
   portion, taken alone).

.. describe:: newsgroup

   The name of a Usenet newsgroup.

.. describe:: option

   A command-line option of Python.  The leading hyphen(s) must be included.
   If a matching ``cmdoption`` directive exists, it is linked to.  For options
   of other programs or scripts, use simple ````code```` markup.

.. describe:: program

   The name of an executable program.  This may differ from the file name for
   the executable for some platforms.  In particular, the ``.exe`` (or other)
   extension should be omitted for Windows programs.

.. describe:: regexp

   A regular expression. Quotes should not be included.

.. describe:: samp

   A piece of literal text, such as code.  Within the contents, you can use
   curly braces to indicate a "variable" part, as in ``:file:``.

   If you don't need the "variable part" indication, use the standard
   ````code```` instead.


The following roles generate external links:

.. describe:: pep

   A reference to a Python Enhancement Proposal.  This generates appropriate
   index entries. The text "PEP *number*\ " is generated; in the HTML output,
   this text is a hyperlink to an online copy of the specified PEP.

.. describe:: rfc

   A reference to an Internet Request for Comments.  This generates appropriate
   index entries. The text "RFC *number*\ " is generated; in the HTML output,
   this text is a hyperlink to an online copy of the specified RFC.


Note that there are no special roles for including hyperlinks as you can use
the standard reST markup for that purpose.


.. _doc-ref-role:

Cross-linking markup
--------------------

To support cross-referencing to arbitrary sections in the documentation, the
standard reST labels are "abused" a bit: Every label must precede a section
title; and every label name must be unique throughout the entire documentation
source.

You can then reference to these sections using the ``:ref:`label-name``` role.

Example::

   .. _my-reference-label:

   Section to cross-reference
   --------------------------

   This is the text of the section.

   It refers to the section itself, see :ref:`my-reference-label`.

The ``:ref:`` invocation is replaced with the section title.

Alternatively, you can reference any label (not just section titles)
if you provide the link text ``:ref:`link text <reference-label>```.

Paragraph-level markup
----------------------

These directives create short paragraphs and can be used inside information
units as well as normal text:

.. describe:: note

   An especially important bit of information about an API that a user should be
   aware of when using whatever bit of API the note pertains to.  The content of
   the directive should be written in complete sentences and include all
   appropriate punctuation.

   Example::

      .. note::

         This function is not suitable for sending spam e-mails.

.. describe:: warning

   An important bit of information about an API that a user should be aware of
   when using whatever bit of API the warning pertains to.  The content of the
   directive should be written in complete sentences and include all appropriate
   punctuation.  In the interest of not scaring users away from pages filled
   with warnings, this directive should only be chosen over ``note`` for
   information regarding the possibility of crashes, data loss, or security
   implications.

.. describe:: versionadded

   This directive documents the version of Python which added the described
   feature to the library or C API. When this applies to an entire module, it
   should be placed at the top of the module section before any prose.

   The first argument must be given and is the version in question; you can add
   a second argument consisting of a *brief* explanation of the change.

   Example::

      .. versionadded:: 3.1
         The *spam* parameter.

   Note that there must be no blank line between the directive head and the
   explanation; this is to make these blocks visually continuous in the markup.

.. describe:: versionchanged

   Similar to ``versionadded``, but describes when and what changed in the named
   feature in some way (new parameters, changed side effects, etc.).

--------------

.. describe:: impl-detail

   This directive is used to mark CPython-specific information.  Use either with
   a block content or a single sentence as an argument, i.e. either ::

      .. impl-detail::

         This describes some implementation detail.

         More explanation.

   or ::

      .. impl-detail:: This shortly mentions an implementation detail.

   "\ **CPython implementation detail:**\ " is automatically prepended to the
   content.

.. describe:: seealso

   Many sections include a list of references to module documentation or
   external documents.  These lists are created using the ``seealso`` directive.

   The ``seealso`` directive is typically placed in a section just before any
   sub-sections.  For the HTML output, it is shown boxed off from the main flow
   of the text.

   The content of the ``seealso`` directive should be a reST definition list.
   Example::

      .. seealso::

         Module :mod:`zipfile`
            Documentation of the :mod:`zipfile` standard module.

         `GNU tar manual, Basic Tar Format <http://link>`_
            Documentation for tar archive files, including GNU tar extensions.

.. describe:: rubric

   This directive creates a paragraph heading that is not used to create a
   table of contents node.  It is currently used for the "Footnotes" caption.

.. describe:: centered

   This directive creates a centered boldfaced paragraph.  Use it as follows::

      .. centered::

         Paragraph contents.


Table-of-contents markup
------------------------

Since reST does not have facilities to interconnect several documents, or split
documents into multiple output files, Sphinx uses a custom directive to add
relations between the single files the documentation is made of, as well as
tables of contents.  The ``toctree`` directive is the central element.

.. describe:: toctree

   This directive inserts a "TOC tree" at the current location, using the
   individual TOCs (including "sub-TOC trees") of the files given in the
   directive body.  A numeric ``maxdepth`` option may be given to indicate the
   depth of the tree; by default, all levels are included.

   Consider this example (taken from the library reference index)::

      .. toctree::
         :maxdepth: 2

         intro
         strings
         datatypes
         numeric
         (many more files listed here)

   This accomplishes two things:

   * Tables of contents from all those files are inserted, with a maximum depth
     of two, that means one nested heading.  ``toctree`` directives in those
     files are also taken into account.
   * Sphinx knows that the relative order of the files ``intro``,
     ``strings`` and so forth, and it knows that they are children of the
     shown file, the library index.  From this information it generates "next
     chapter", "previous chapter" and "parent chapter" links.

   In the end, all files included in the build process must occur in one
   ``toctree`` directive; Sphinx will emit a warning if it finds a file that is
   not included, because that means that this file will not be reachable through
   standard navigation.

   The special file ``contents.rst`` at the root of the source directory is the
   "root" of the TOC tree hierarchy; from it the "Contents" page is generated.


Index-generating markup
-----------------------

Sphinx automatically creates index entries from all information units (like
functions, classes or attributes) like discussed before.

However, there is also an explicit directive available, to make the index more
comprehensive and enable index entries in documents where information is not
mainly contained in information units, such as the language reference.

The directive is ``index`` and contains one or more index entries.  Each entry
consists of a type and a value, separated by a colon.

For example::

   .. index::
      single: execution; context
      module: __main__
      module: sys
      triple: module; search; path

This directive contains five entries, which will be converted to entries in the
generated index which link to the exact location of the index statement (or, in
case of offline media, the corresponding page number).

The possible entry types are:

single
   Creates a single index entry.  Can be made a subentry by separating the
   subentry text with a semicolon (this notation is also used below to describe
   what entries are created).
pair
   ``pair: loop; statement`` is a shortcut that creates two index entries,
   namely ``loop; statement`` and ``statement; loop``.
triple
   Likewise, ``triple: module; search; path`` is a shortcut that creates three
   index entries, which are ``module; search path``, ``search; path, module`` and
   ``path; module search``.
module, keyword, operator, object, exception, statement, builtin
   These all create two index entries.  For example, ``module: hashlib`` creates
   the entries ``module; hashlib`` and ``hashlib; module``.

For index directives containing only "single" entries, there is a shorthand
notation::

   .. index:: BNF, grammar, syntax, notation

This creates four index entries.


Grammar production displays
---------------------------

Special markup is available for displaying the productions of a formal grammar.
The markup is simple and does not attempt to model all aspects of BNF (or any
derived forms), but provides enough to allow context-free grammars to be
displayed in a way that causes uses of a symbol to be rendered as hyperlinks to
the definition of the symbol.  There is this directive:

.. describe:: productionlist

   This directive is used to enclose a group of productions.  Each production is
   given on a single line and consists of a name, separated by a colon from the
   following definition.  If the definition spans multiple lines, each
   continuation line must begin with a colon placed at the same column as in the
   first line.

   Blank lines are not allowed within ``productionlist`` directive arguments.

   The definition can contain token names which are marked as interpreted text
   (e.g. ``unaryneg ::= "-" `integer```) -- this generates cross-references
   to the productions of these tokens.

   Note that no further reST parsing is done in the production, so that you
   don't have to escape ``*`` or ``|`` characters.


.. XXX describe optional first parameter

The following is an example taken from the Python Reference Manual::

   .. productionlist::
      try_stmt: try1_stmt | try2_stmt
      try1_stmt: "try" ":" `suite`
               : ("except" [`expression` ["," `target`]] ":" `suite`)+
               : ["else" ":" `suite`]
               : ["finally" ":" `suite`]
      try2_stmt: "try" ":" `suite`
               : "finally" ":" `suite`


Substitutions
-------------

The documentation system provides three substitutions that are defined by default.
They are set in the build configuration file :file:`conf.py`.

.. describe:: |release|

   Replaced by the Python release the documentation refers to.  This is the full
   version string including alpha/beta/release candidate tags, e.g. ``2.5.2b3``.

.. describe:: |version|

   Replaced by the Python version the documentation refers to. This consists
   only of the major and minor version parts, e.g. ``2.5``, even for version
   2.5.1.

.. describe:: |today|

   Replaced by either today's date, or the date set in the build configuration
   file.  Normally has the format ``April 14, 2007``.


.. rubric:: Footnotes

.. [1] There is a standard ``.. include`` directive, but it raises errors if the
       file is not found.  This one only emits a warning.


Differences to the LaTeX markup
===============================

Though the markup language is different, most of the concepts and markup types
of the old LaTeX docs have been kept -- environments as reST directives, inline
commands as reST roles and so forth.

However, there are some differences in the way these work, partly due to the
differences in the markup languages, partly due to improvements in Sphinx.  This
section lists these differences, in order to give those familiar with the old
format a quick overview of what they might run into.

Inline markup
-------------

These changes have been made to inline markup:

* **Cross-reference roles**

  Most of the following semantic roles existed previously as inline commands,
  but didn't do anything except formatting the content as code.  Now, they
  cross-reference to known targets (some names have also been shortened):

  | *mod* (previously *refmodule* or *module*)
  | *func* (previously *function*)
  | *data* (new)
  | *const*
  | *class*
  | *meth* (previously *method*)
  | *attr* (previously *member*)
  | *exc* (previously *exception*)
  | *cdata*
  | *cfunc* (previously *cfunction*)
  | *cmacro* (previously *csimplemacro*)
  | *ctype*

  Also different is the handling of *func* and *meth*: while previously
  parentheses were added to the callable name (like ``\func{str()}``), they are
  now appended by the build system -- appending them in the source will result
  in double parentheses.  This also means that ``:func:`str(object)``` will not
  work as expected -- use ````str(object)```` instead!

* **Inline commands implemented as directives**

  These were inline commands in LaTeX, but are now directives in reST:

  | *deprecated*
  | *versionadded*
  | *versionchanged*

  These are used like so::

     .. deprecated:: 2.5
        Reason of deprecation.

  Also, no period is appended to the text for *versionadded* and
  *versionchanged*.

  | *note*
  | *warning*

  These are used like so::

     .. note::

        Content of note.

* **Otherwise changed commands**

  The *samp* command previously formatted code and added quotation marks around
  it.  The *samp* role, however, features a new highlighting system just like
  *file* does:

     ``:samp:`open({filename}, {mode})``` results in :samp:`open({filename}, {mode})`

* **Dropped commands**

  These were commands in LaTeX, but are not available as roles:

  | *bfcode*
  | *character* (use :samp:`\`\`'c'\`\``)
  | *citetitle* (use ```Title <URL>`_``)
  | *code* (use ````code````)
  | *email* (just write the address in body text)
  | *filenq*
  | *filevar* (use the ``{...}`` highlighting feature of *file*)
  | *programopt*, *longprogramopt* (use *option*)
  | *ulink* (use ```Title <URL>`_``)
  | *url* (just write the URL in body text)
  | *var* (use ``*var*``)
  | *infinity*, *plusminus* (use the Unicode character)
  | *shortversion*, *version* (use the ``|version|`` and ``|release|`` substitutions)
  | *emph*, *strong* (use the reST markup)

* **Backslash escaping**

  In reST, a backslash must be escaped in normal text, and in the content of
  roles.  However, in code literals and literal blocks, it must not be escaped.
  Example: ``:file:`C:\\Temp\\my.tmp``` vs. ````open("C:\Temp\my.tmp")````.


Information units
-----------------

Information units (*...desc* environments) have been made reST directives.
These changes to information units should be noted:

* **New names**

  "desc" has been removed from every name.  Additionally, these directives have
  new names:

  | *cfunction* (previously *cfuncdesc*)
  | *cmacro* (previously *csimplemacrodesc*)
  | *exception* (previously *excdesc*)
  | *function* (previously *funcdesc*)
  | *attribute* (previously *memberdesc*)

  The *classdesc\** and *excclassdesc* environments have been dropped, the
  *class* and *exception* directives support classes documented with and without
  constructor arguments.

* **Multiple objects**

  The equivalent of the *...line* commands is::

     .. function:: do_foo(bar)
                   do_bar(baz)

        Description of the functions.

  IOW, just give one signatures per line, at the same indentation level.

* **Arguments**

  There is no *optional* command.  Just give function signatures like they
  should appear in the output::

     .. function:: open(filename[, mode[, buffering]])

        Description.

  Note: markup in the signature is not supported.

* **Indexing**

  The *...descni* environments have been dropped.  To mark an information unit
  as unsuitable for index entry generation, use the *noindex* option like so::

     .. function:: foo_*
        :noindex:

        Description.

* **New information units**

  There are new generic information units: One is called "describe" and can be
  used to document things that are not covered by the other units::

     .. describe:: a == b

        The equals operator.

  The others are::

     .. cmdoption:: -O

        Describes a command-line option.

     .. envvar:: PYTHONINSPECT

        Describes an environment variable.


Structure
---------

The LaTeX docs were split in several toplevel manuals.  Now, all files are part
of the same documentation tree, as indicated by the *toctree* directives in the
sources (though individual output formats may choose to split them up into parts
again).  Every *toctree* directive embeds other files as subdocuments of the
current file (this structure is not necessarily mirrored in the filesystem
layout).  The toplevel file is :file:`contents.rst`.

However, most of the old directory structure has been kept, with the
directories renamed as follows:

* :file:`api` -> :file:`c-api`
* :file:`dist` -> :file:`distutils`, with the single TeX file split up
* :file:`doc` -> :file:`documenting`
* :file:`ext` -> :file:`extending`
* :file:`inst` -> :file:`installing`
* :file:`lib` -> :file:`library`
* :file:`mac` -> merged into :file:`library`, with :file:`mac/using.tex`
  moved to :file:`using/mac.rst`
* :file:`ref` -> :file:`reference`
* :file:`tut` -> :file:`tutorial`, with the single TeX file split up


.. XXX more (index-generating, production lists, ...)


Building the documentation
==========================

You need to have Python 2.4 or higher installed; the toolset used to build the
docs is written in Python.  It is called *Sphinx*, it is not included in this
tree, but maintained separately.  Also needed are the docutils, supplying the
base markup that Sphinx uses, Jinja, a templating engine, and optionally
Pygments, a code highlighter.


Using make
----------

Luckily, a Makefile has been prepared so that on Unix, provided you have
installed Python and Subversion, you can just run ::

   cd Doc
   make html

to check out the necessary toolset in the :file:`tools/` subdirectory and build
the HTML output files.  To view the generated HTML, point your favorite browser
at the top-level index :file:`build/html/index.html` after running "make".

Available make targets are:

 * "html", which builds standalone HTML files for offline viewing.

 * "htmlhelp", which builds HTML files and a HTML Help project file usable to
   convert them into a single Compiled HTML (.chm) file -- these are popular
   under Microsoft Windows, but very handy on every platform.

   To create the CHM file, you need to run the Microsoft HTML Help Workshop
   over the generated project (.hhp) file.

 * "latex", which builds LaTeX source files as input to "pdflatex" to produce
   PDF documents.

 * "text", which builds a plain text file for each source file.

 * "linkcheck", which checks all external references to see whether they are
   broken, redirected or malformed, and outputs this information to stdout
   as well as a plain-text (.txt) file.

 * "changes", which builds an overview over all versionadded/versionchanged/
   deprecated items in the current version. This is meant as a help for the
   writer of the "What's New" document.

 * "coverage", which builds a coverage overview for standard library modules
   and C API.

 * "pydoc-topics", which builds a Python module containing a dictionary with
   plain text documentation for the labels defined in
   :file:`tools/sphinxext/pyspecific.py` -- pydoc needs these to show topic and
   keyword help.

A "make update" updates the Subversion checkouts in :file:`tools/`.


Without make
------------

You'll need to install the Sphinx package, either by checking it out via ::

   svn co http://svn.python.org/projects/external/Sphinx-0.6.5/sphinx tools/sphinx

or by installing it from PyPI.

Then, you need to install Docutils, either by checking it out via ::

   svn co http://svn.python.org/projects/external/docutils-0.6/docutils tools/docutils

or by installing it from http://docutils.sf.net/.

You also need Jinja2, either by checking it out via ::

   svn co http://svn.python.org/projects/external/Jinja-2.3.1/jinja2 tools/jinja2

or by installing it from PyPI.

You can optionally also install Pygments, either as a checkout via ::

   svn co http://svn.python.org/projects/external/Pygments-1.3.1/pygments tools/pygments

or from PyPI at http://pypi.python.org/pypi/Pygments.


Then, make an output directory, e.g. under `build/`, and run ::

   python tools/sphinx-build.py -b<builder> . build/<outputdirectory>

where `<builder>` is one of html, text, latex, or htmlhelp (for explanations see
the make targets above).