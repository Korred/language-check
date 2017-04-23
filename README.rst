language-check
==============

Python wrapper for LanguageTool.

This fork drops support for LanguageTool version <= 3.5 in favor of version 3.6 and above.

Example usage
-------------

From the interpreter:

>>> import language_check
>>> tool = language_check.LanguageTool('en-US')
>>> text = u'A sentence with a error in the Hitchhiker’s Guide tot he Galaxy'
>>> matches = tool.check(text)
>>> len(matches)
2

``Match`` object attributes:

(based on Model from https://languagetool.org/http-api/swagger-ui/#!/default/post_check)

shortMessage,
message,
offset,
length,
replacements, 
context,
contextoffset,
ruleId,
subId,
ruledescription,
urls,
issueType,
category,
categoryId,



Print a ``Match`` object:

>>> print(matches[1])
Line 1, column 51, Rule ID: TOT_HE[1]
Message: Did you mean 'to the'?
Suggestion: to the
...

Automatically apply suggestions to the text:

>>> language_check.correct(text, matches)
'A sentence with an error in the Hitchhiker’s Guide to the Galaxy'

From the command line::

    $ echo 'This are bad.' > example.txt

    $ language-check example.txt
    example.txt:1:1: THIS_NNS[3]: Did you mean 'these'?


Installation
------------

To install via pip::

    $ pip install --upgrade language-check

If you are using Python 2, you'll need to install 3to2 beforehand::

    $ pip install --upgrade 3to2


Prerequisites
-------------

- `Python 3.3+ <https://www.python.org>`_ (or 2.7)
- `lib3to2 <https://bitbucket.org/amentajo/lib3to2>`_
  (if installing for Python 2)
- `LanguageTool 3.6 or greater <https://www.languagetool.org>`_ (Java 6.0+) - download manually and place into language-check folder
