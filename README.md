# houdini_additional_python_docs
*Additional documentation of Houdini Python modules*

H version
16.5.378

create virtualenv
mkvirtualenv h_docs_test

activate
workon h_docs_test

install sphinx
pip install sphinx

get python files, remove the ones generating errors
Only in houdini_libs_bak/autorig: mocapgui.py
Only in houdini_libs_bak/: autorigs
Only in houdini_libs_bak/: bvhviewer
Only in houdini_libs_bak/: generateHDAToolsForOTL.py
Only in houdini_libs_bak/: generate_proto.py
Only in houdini_libs_bak/: hdefereval.py
Only in houdini_libs_bak/: hotkeys
Only in houdini_libs_bak/: hou.py
Only in houdini_libs_bak/: inlinecpp.py
Only in houdini_libs_bak/: loadHelpcardOTLExample.py
Only in houdini_libs_bak/: nodegraphalign.py
Only in houdini_libs_bak/: nodegraphautoscroll.py
Only in houdini_libs_bak/: nodegraphbase.py
Only in houdini_libs_bak/: nodegraphconnect.py
Only in houdini_libs_bak/: nodegraphdisplay.py
Only in houdini_libs_bak/: nodegraphdispopts.py
Only in houdini_libs_bak/: nodegraphedittext.py
Only in houdini_libs_bak/: nodegraphfastfind.py
Only in houdini_libs_bak/: nodegraphflags.py
Only in houdini_libs_bak/: nodegraphfurutils.py
Only in houdini_libs_bak/: nodegraphgestures.py
Only in houdini_libs_bak/: nodegraphhooks.py
Only in houdini_libs_bak/: nodegraphhotkeys.py
Only in houdini_libs_bak/: nodegraphinfo.py
Only in houdini_libs_bak/: nodegraphlayout.py
Only in houdini_libs_bak/: nodegraphpalettes.py
Only in houdini_libs_bak/: nodegraphpopupmenus.py
Only in houdini_libs_bak/: nodegraphprefs.py
Only in houdini_libs_bak/: nodegraph.py
Only in houdini_libs_bak/: nodegraphselectposhooks.py
Only in houdini_libs_bak/: nodegraphselectpos.py
Only in houdini_libs_bak/: nodegraphsnap.py
Only in houdini_libs_bak/: nodegraphstates.py
Only in houdini_libs_bak/: nodegraphtitle.py
Only in houdini_libs_bak/: nodegraphui.py
Only in houdini_libs_bak/: nodegraphutils.py
Only in houdini_libs_bak/: nodegraphview.py
Only in houdini_libs_bak/: poselib
Only in houdini_libs_bak/: whoosh

go to proj dir
cd h_docs_test

sphinx-quickstart
enable splitting source and build dirs
enable autodocstring extension

locate sphinx-build script
which sphinx-build

edit it - change shebang
#!/opt/hfs16.5.378/bin/hython

edit source/conf.py
import os
import sys
sys.path.insert(0, os.path.abspath('../houdini_libs'))

edit source/index.rst (add modules)
.. toctree::
   :maxdepth: 3
   :caption: Contents:

   modules

generate rst files from modules
sphinx-apidoc -o source houdini_libs

build docs
make html