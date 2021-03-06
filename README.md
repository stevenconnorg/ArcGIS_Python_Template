# ArcGIS_Python_Template
Example of how to set up a Python Toolbox for ESRI ArcGIS

## Overview

This project serves as a starting point when creating ArcGIS Python Tools.

In the ESRI world, "Python Tool" and "Python Toolbox" have specific
meanings.  They were added starting sometime around ArcGIS 10.1. 

Before "Python Toolboxes" it was still possible to write sripts in
Python for use in ArcGIS. Back then interfacing a script to ArcGIS
meant using ArcCatalog to define what parameters the script takes and
storing those definitions in a proprietary binary file. The bad thing
about this approach that it is hard to keeping the ArcGIS binary file
and the script in sync. Change the parameters in the python and the
definitions stopped working. Since the ArcGIS file is in binary form,
you can forget putting it into version control and being able to
update it from a text editor.

With Python Toolboxes, everything is stored in the plain text Python
source files, so it's cleaner and very easy to put into version
control.

Conceptually, "Python tools" live inside "Python toolboxes" and that's
how they appear in ArcCatalog. There can be many tools in one toolbox.

In practice, I break everything out into separate files,
so that's what I have done in this template.

This template just shows you how to set up a Python toolbox, it does nothing interesting on its own.

To use it, copy the repository as a functioning starting point, then add your own code.

Of course if you want, you could clone the template, make improvements, and send pull requests to me!

## Improvements 4/2018

I added a sample shapefile to the project so that it can actually run its unit test
and so that I could add an example of using Python a namedtuple to access columns by name.

I use Visual Studio 2017 Community now all the time to develop and
test Python. It's free and has excellent code completion
("Intellisense") and debugging. Therefore I have added solution and project files

## TODO

Write unit test for sample_tool.py

## Files

sample.pyt - This is the Python toolbox; it will show up right away in ArcCatalog as a toolbox.

sample_tool.py - This is a class defining a tool. It acts as "glue" to connect the
"business logic" in some_sample_code.py to the toolbox.

some_sample_code.py - This is the code that would actually do some work.

The template ESRI provides has all the code in one PYT file. This is okay for little tiny tools, 
in fact you can easily share a toolbox written this way because it's all in one file. 
But it's hard to debug and hard to maintain.

My intention is that once you set up the toolbox and tool files, you will seldom touch them.
Minor errors in those sections can confuse ArcCatalog, causing your entire toolbox to fail to load.

Keeping the toolbox code and the tool code in separate files also means you can very easily move tools from one toolbox to another.
You just have to change one line in the PYT file to add or remove a tool. It also makes debugging easier.

Keeping the code actually doing the work in a separate file means it can be tested stand-alone in a debugger.
You can hard code paths and settings in the unit test section and run the business logic by itself. 
It's much faster than trying to do everything through ESRI ArcCatalog typing parameters in over and over.

Note that you have to quit and restart ArcCatalog to get it to notice changes in the toolbox code, 
this really slows down debugging too. If you know a work around ("refresh" does not do it), please tell me.
By contrast keeping business logic in separate files means you can update and save that file and then
immediately re-run the tool in ArcMap or ArcCatalog.

## Unit Tests

I try to put a unit test in each python file. This means you can develop the code in that file independently,
running it in a debugger and confirming it does what you expect before putting together all the pieces. 

You can run sample.pyt as a standalone script. It will pull in the tools and then list out what it knows about them.

## Resources

https://desktop.arcgis.com/en/arcmap/latest/analyze/creating-tools/defining-parameter-data-types-in-a-python-toolbox.htm

https://desktop.arcgis.com/en/arcmap/latest/analyze/creating-tools/controlling-the-progress-dialog-box.htm

