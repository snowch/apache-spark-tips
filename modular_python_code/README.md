### Overview

This document contains tips for modular Python code on IBM's Spark as a Service and IBM's Data Science Experience.

### Table of contents

- [Extracting common code into modules](#Extracting-common-code-into-modules)
- [Installing pip modules only once](#Installing-pip-modules-only-once)


### Extracting common code into modules

When working with larger spark notebooks, you may want to extract some of the code into modules that you can include in your notebook:  See this stackoverflow post for some options: http://stackoverflow.com/questions/41876516/how-to-supply-user-functions-modules-in-dsx/41890895#41890895

### Installing pip modules only once

You want to include your `pip install ...` statements in a notebook to make the notebook reproducible by ensuring anyone setting up the notebook gets the same modules that you have.  However, it is inconvenient to run `pip install ...` everytime you run all cells in the notebook.  See here for a solution: http://stackoverflow.com/questions/41481291/how-to-prevent-pip-install-running-every-time-i-run-the-whole-notebook
