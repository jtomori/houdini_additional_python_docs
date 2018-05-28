# houdini_additional_python_docs
*Additional documentation of Houdini Python modules*
<br><br>


Info
----
[Generated documentation can be found here](https://jtomori.github.io/houdini_additional_python_docs/)

If you did some scripting in Houdini, then chances are that you have found [*toolutils*](https://jtomori.github.io/houdini_additional_python_docs/toolutils.html) module quite handy. But searching in Houdini online help is not very helpful, you will not find much information about it. Maybe some useful code snippets, but not its documentation.

As it turns out there are some handy modules coming with Houdini, but they can be a bit hidden to many users. So I decided to do a small project and auto-generate documentation from docstrings from those modules. I used [*Sphinx*](http://www.sphinx-doc.org/en/master/) for this.

In this readme I will show you process of generating it. It is defenitely not a perfect approach as it did not handle some modules. But it still worked pretty well on majority of them and generated nice and organized webpages.

Current documentation was generated from `Houdini 16.5.378`
<br><br>


Guide (linux)
-------------

*   Create a new virtual environment (in my case I am using [*virtualenvwrapper*](https://virtualenvwrapper.readthedocs.io/en/latest/))
    ```
    $ mkvirtualenv h_additional_docs
    ```
*   Activate it
    ```
    $ workon h_additional_docs
    ```

*   Install *Sphinx* (e.g. using *pip*)
    ```
    $ pip install sphinx
    ```

*   Create a folder for our work and enter it
    ```
    $ mkdir h_additional_docs
    $ cd h_additional_docs
    ```

*   Copy Python files from Houdini: `$HH/python2.7libs`
    ```
    $ cp -r $HH/python2.7libs .
    ```
    `$HH` will be present after sourcing Houdini environment, if you are outside of Houdini environment, then replace `$HH` with your Houdini installation directory, e.g.:
    ```
    $ cp -r /opt/hfs16.5.378/houdini/python2.7libs .
    ```

    During documentation generation *Sphinx* will import our Houdini modules. However some of them are not possible to be imported because they refer to non-available Houdini *ui* module. 
    
    What I did for now was to simply exclude those modules. Ideas for making *Sphinx* working with *ui* module are welcome.

    Here is list of excluded modules:
    ```
    /autorig: mocapgui.py
    /: autorigs
    /: bvhviewer
    /: generateHDAToolsForOTL.py
    /: generate_proto.py
    /: hdefereval.py
    /: hotkeys
    /: hou.py
    /: inlinecpp.py
    /: loadHelpcardOTLExample.py
    /: nodegraphalign.py
    /: nodegraphautoscroll.py
    /: nodegraphbase.py
    /: nodegraphconnect.py
    /: nodegraphdisplay.py
    /: nodegraphdispopts.py
    /: nodegraphedittext.py
    /: nodegraphfastfind.py
    /: nodegraphflags.py
    /: nodegraphfurutils.py
    /: nodegraphgestures.py
    /: nodegraphhooks.py
    /: nodegraphhotkeys.py
    /: nodegraphinfo.py
    /: nodegraphlayout.py
    /: nodegraphpalettes.py
    /: nodegraphpopupmenus.py
    /: nodegraphprefs.py
    /: nodegraph.py
    /: nodegraphselectposhooks.py
    /: nodegraphselectpos.py
    /: nodegraphsnap.py
    /: nodegraphstates.py
    /: nodegraphtitle.py
    /: nodegraphui.py
    /: nodegraphutils.py
    /: nodegraphview.py
    /: poselib
    /: whoosh
    ```

*   run *Sphinx* setup
    ```
    $ sphinx-quickstart
    ```
    Enable splitting source and build dirs and enable autodoc and githubpages extensions, in my case the setup looked like this:
    ```
    $ sphinx-quickstart 
    Welcome to the Sphinx 1.7.4 quickstart utility.

    Please enter values for the following settings (just press Enter to
    accept a default value, if one is given in brackets).

    Selected root path: .

    You have two options for placing the build directory for Sphinx output.
    Either, you use a directory "_build" within the root path, or you separate
    "source" and "build" directories within the root path.
    > Separate source and build directories (y/n) [n]: y

    Inside the root directory, two more directories will be created; "_templates"
    for custom HTML templates and "_static" for custom stylesheets and other static
    files. You can enter another prefix (such as ".") to replace the underscore.
    > Name prefix for templates and static dir [_]: 

    The project name will occur in several places in the built documentation.
    > Project name: Houdini Python modules
    > Author name(s): jtomori
    > Project release []: 16.5.378

    If the documents are to be written in a language other than English,
    you can select a language here by its language code. Sphinx will then
    translate text that it generates into that language.

    For a list of supported codes, see
    http://sphinx-doc.org/config.html#confval-language.
    > Project language [en]: 

    The file name suffix for source files. Commonly, this is either ".txt"
    or ".rst".  Only files with this suffix are considered documents.
    > Source file suffix [.rst]: 

    One document is special in that it is considered the top node of the
    "contents tree", that is, it is the root of the hierarchical structure
    of the documents. Normally, this is "index", but if your "index"
    document is a custom template, you can also set this to another filename.
    > Name of your master document (without suffix) [index]: 

    Sphinx can also add configuration for epub output:
    > Do you want to use the epub builder (y/n) [n]: 
    Indicate which of the following Sphinx extensions should be enabled:
    > autodoc: automatically insert docstrings from modules (y/n) [n]: y
    > doctest: automatically test code snippets in doctest blocks (y/n) [n]: 
    > intersphinx: link between Sphinx documentation of different projects (y/n) [n]: 
    > todo: write "todo" entries that can be shown or hidden on build (y/n) [n]: 
    > coverage: checks for documentation coverage (y/n) [n]: 
    > imgmath: include math, rendered as PNG or SVG images (y/n) [n]: 
    > mathjax: include math, rendered in the browser by MathJax (y/n) [n]: 
    > ifconfig: conditional inclusion of content based on config values (y/n) [n]: 
    > viewcode: include links to the source code of documented Python objects (y/n) [n]: 
    > githubpages: create .nojekyll file to publish the document on GitHub pages (y/n) [n]: y

    A Makefile and a Windows command file can be generated for you so that you
    only have to run e.g. `make html' instead of invoking sphinx-build
    directly.
    > Create Makefile? (y/n) [y]: 
    > Create Windows command file? (y/n) [y]: n
    ```

*   To make importing of Houdini-related modules into *Sphinx* easier, we can replace system Python interpreter with the Houdini one

    Locate the `sphinx-build` script
    ```
    $ which sphinx-build
    ```
    And edit its first line (shebang) - point it to `hython` (match your Houdini version)
    ```
    #!/opt/hfs16.5.378/bin/hython
    ```

*   Edit *Sphinx* configuration to add our modules into system path

    edit `source/conf.py` and add the following lines
    ```
    import os
    import sys
    sys.path.insert(0, os.path.abspath('../python2.7libs'))
    ```

*   Tell *Sphinx* to create documentation from modules

    edit `source/index.rst` and add `modules` keyword (preserve indentation)

    it should like like this:
    ```
    .. Houdini Python modules documentation master file, created by
       sphinx-quickstart on Sat May 26 15:50:01 2018.
       You can adapt this file completely to your liking, but it should at least
       contain the root `toctree` directive.

    Welcome to Houdini Python modules documentation!
    ===================================================

    .. toctree::
       :maxdepth: 3
       :caption: Contents:

       modules

    Indices and tables
    ==================

    * :ref:`genindex`
    * :ref:`modindex`
    * :ref:`search`

    ```

*   Generate *rst* files from modules
    ```
    $ sphinx-apidoc -o source python2.7libs
    ```

*   Build html documentation
    ```
    $ make html
    ```

*   Now you have nice online documentation of Houdini Python modules, you will find it in `build/html` directory