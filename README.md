# Introduction

This repository contains tips for working with Apache Spark as a Service and Data Science Experience

### Table of contents

[Modular Python Code](./modular_python_code/README.md)

[Performance Tips](./performance/README.md)

 - [General Tips](#general-tips)
   - [Access the spark history server from notebook (python)](#access-the-spark-history-server-from-notebook-python)
 
### General Tips
I may move this to its own section if it grows big enough

#### Access the spark history server from notebook (python)

Add a cell:

```
import os
print("https://cdsx.ng.bluemix.net/data/analytics/{0}/monitoring/hsui".format(os.environ["NOTEBOOK_TENANT_ID"]))
```

Run the cell - this will print out a clickable url that takes you directly to the spark history server in Bluemix.

