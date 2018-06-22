# houdini_additional_python_docs
*Additional documentation of Houdini Python modules*
<br><br>


Info
----
[Generated documentation can be found here](https://jtomori.github.io/houdini_additional_python_docs/)

If you did some scripting in Houdini, then chances are that you have found [*toolutils*](https://jtomori.github.io/houdini_additional_python_docs/toolutils.html) module quite handy. But searching in Houdini online help is not very helpful, you will not find much information about it. Maybe some useful code snippets, but not its documentation.

As it turns out there are some handy modules coming with Houdini, but they can be a bit hidden to many users. So I decided to do a small project and auto-generate documentation from docstrings from those modules. I used [*Sphinx*](http://www.sphinx-doc.org/en/master/) for this.

Current documentation was generated from `Houdini 16.5.496`
<br><br>

Update
------
My initial approach involved using `hython` as interpreter for `sphinx-build` and I was deleting modules which would not import. 

It is not needed anymore since I found out [autodoc_mock_imports](http://www.sphinx-doc.org/en/master/ext/autodoc.html#confval-autodoc_mock_imports) option which you can find in [conf.py](./source/conf.py). This means that listed modules will not be documented, but all modules that depend on them will be documented fine (they will be importable by *Sphinx*). This allowed me to generate documentation for much more modules. It is still not perfect, but if you have any suggestions, then you are most welcome to let me know :).
<br><br>

Guide (linux)
-------------

*   Install *Sphinx* (e.g. using *pip*)
    ```
    $ pip install sphinx
    ```

*   Clone this repo and enter it
    ```
    $ git clone https://github.com/jtomori/houdini_additional_python_docs.git
    $ cd houdini_additional_python_docs
    ```

*   Copy Python files from Houdini: `$HH/python2.7libs`
    ```
    $ cp -r $HH/python2.7libs .
    ```
    `$HH` will be present after sourcing Houdini environment, if you are outside of Houdini environment, then replace `$HH` with your Houdini installation directory, e.g.:
    ```
    $ cp -r /opt/hfsXX.X.XXX/houdini/python2.7libs .
    ```

    Some of the modules do not need to be docummented, so delete them
    ```
    $ rm -r python2.7libs/whoosh python2.7libs/hou.py
    ```

    Those two modules are already docummented
    * [hou](http://www.sidefx.com/docs/houdini/hom/hou/)
    * [whoosh](http://whoosh.readthedocs.io/en/latest/)

*   Generate *rst* files from modules
    ```
    $ sphinx-apidoc -o source python2.7libs
    ```

*   Build html documentation
    ```
    $ make html
    ```

*   Now you have nice online documentation of Houdini Python modules, you will find it in `build/html` directory. You can push it to `gh-pages` branch.