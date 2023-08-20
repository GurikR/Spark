
##Databricks Ecosystem

**Spark API**

Spark SQL + Dataframes: Dataframes is programming abstraction provided Spark SQL, distributed query engine.

Streaming: need of batch process along with real time processing with streaming

**Spark Execution**
Spark uses cluter of machines to process big data by converting large task into smaller ones and distributing work across several machines

**Spark application** -> multiple jobs(parallized) -> each job has multiple stages -> each stage is set of ordered steps to complete job -> tasks are created by driver and assigned a partition of data to process (smallest unit of work)
<img width="701" alt="Screenshot 2023-08-21 000153" src="https://github.com/GurikR/Spark/assets/5446906/9d6a7e59-53ad-41eb-80b1-93b200b02360">


**Spark Cluster** 
Driver: is m/c in application runs, 3 main things a. maintaining info spark app, b.responding to users program, c.analizing distributing, scheduling work across executors

worker node: hosts the executor process it has fixed number of executors at any point in time.

executor: each executor holds a chunk of data to process called partition it's a collection of rows that's on one single m/c.
it's work is to carry on work assigned by driver, execute the code and report the state of computation

cores: slots of threads, spark parallizes at 2 levels one at executor and the other at slot level. each slots can be assigned a task so some might be idle at times.
<img width="692" alt="Screenshot 2023-08-21 001315" src="https://github.com/GurikR/Spark/assets/5446906/d9500e87-77fb-44c6-9895-7a817df4cba8">

