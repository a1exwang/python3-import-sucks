# Python import SUCKS!



Here is the directory structure and Python code
```
$ find .
toplevel1
toplevel1/broken_package
toplevel1/broken_package/__init__.py
toplevel2
toplevel2/broken_package
toplevel2/broken_package/child2
toplevel2/broken_package/child2/child2.py

$ cat load.py
import sys
sys.path.append("./toplevel2")
sys.path.append("./toplevel1")

from broken_package.child2 import child2

$ python --version
Python 3.8.2
```


#### So, what's wrong?
If you run the above code, you will get the error message, even though the `broken_package.child2` exists.
If you comment out the line `sys.path.append("./toplevel2")`, the import will be successful.

```
Traceback (most recent call last):
  File "load.py", line 5, in <module>
    from broken_package.child2 import child2
ModuleNotFoundError: No module named 'broken_package.child2'
```

Basically, if there is a `__init__.py` in the upper level module, in this case `broken_package`, Python will not find submodules in the module that is located in another module path.


[For Detailed explaination](http://python-notes.curiousefficiency.org/en/latest/python_concepts/import_traps.html#the-init-py-trap)

