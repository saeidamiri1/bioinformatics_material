---
date: 2024-11-16
description: Hail
categories:
  - Hail
authors:
  - saeidamiri1
---

# Hail 
[Hail module](https://hail.is/) is an open-source, scalable framework for exploring and analyzing genomic data which is a module in Python on the top of Apache Spark.. For more detail, refer to its [tutorial](https://hail.is/docs/0.2/index.html).

<!-- more -->

## How to run on Beluga
### Load Java
```
module load StdEnv/2020
module load java/11.0.2
```

### Path of Hail and Spark 
```
base_hail=/lustre03/project/6004655/COMMUN/runs/samamiri/general_files/hail
export SPARK_HOME=$base_hail/spark-3.1.3-bin-hadoop3.2
```

### Path of Log files
```
export SPARK_LOG_DIR=$HOME
```

### Start Spark 
```
${SPARK_HOME}/sbin/start-master.sh
```

### Activate Python environment
```
source ${base_hail}/hail_env2/bin/activate
export PYTHONPATH=$base_hail/hail_env2/lib/python3.10/site-packages
module  load python/3.10.2  
```

### Run Python
```
${base_hail}/hail_env2/bin/python3.10
```

### import hail 
```
import hail as hl
```

To check if the Hail module is loaded correctly in your Python environment, you can run a simple test script. Here's an example:

```
>>> import hail as hl
>>> hl.init()
Picked up JAVA_TOOL_OPTIONS: -Xmx2g
Picked up JAVA_TOOL_OPTIONS: -Xmx2g
WARNING: An illegal reflective access operation has occurred
WARNING: Illegal reflective access by org.apache.spark.unsafe.Platform (file:/lustre03/project/6004655/COMMUN/runs/samamiri/general_files/hail/spark-3.1.3-bin-hadoop3.2/jars/spark-unsafe_2.12-3.1.3.jar) to constructor java.nio.DirectByteBuffer(long,int)
WARNING: Please consider reporting this to the maintainers of org.apache.spark.unsafe.Platform
WARNING: Use --illegal-access=warn to enable warnings of further illegal reflective access operations
WARNING: All illegal access operations will be denied in a future release
2024-11-15 10:11:27.033 WARN  NativeCodeLoader:60 - Unable to load native-hadoop library for your platform... using builtin-java classes where applicable
Setting default log level to "WARN".
To adjust logging level use sc.setLogLevel(newLevel). For SparkR, use setLogLevel(newLevel).
Running on Apache Spark version 3.1.3
SparkUI available at http://beluga3.int.ets1.calculquebec.ca:4040
Welcome to
     __  __     <>__
    / /_/ /__  __/ /
   / __  / _ `/ / /
  /_/ /_/\_,_/_/_/   version 0.2.109-b71b065e4bb6
LOGGING: writing to /lustre03/project/6004655/COMMUN/runs/samamiri/general_files/hail/hail_env1/hail-20241115-1011-0.2.109-b71b065e4bb6.log
```

If Hail loads correctly, you should see the initialization message from Hail. 