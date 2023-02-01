### Objective:
To help users with NosqlBench adoption and to improve, make efficient the dev and production DSE stress testing, thereby, accelerating testing cycles and go to production timelines.

### What is NosqlBench ?
NoSQLBench is a performance testing tool for the NoSQL ecosystem. It brings together features and capabilities that are not found in any other tool.

You can run common testing workloads directly from the command line.
You can generate virtual data sets of arbitrary size, with deterministic data and statistically shaped values.
You can design custom workloads that emulate your application, contained in a single file, based on statement templates - no IDE or coding required.
You can immediately plot your results in a docker and grafana stack on Linux with a single command line option.
When needed, you can open the access panels and rewire the runtime behavior of NoSQLBench to do advanced testing, including a full scripting environment with Javascript.
CQL Support is built into the tool, however, it is more like a machine harness so others can write their own clients for other system’s.

### Origins & Current State:
The building blocks of this project are rooted in procedural data generation capability was known before as 'Virtual Data Set' and a core runtime and scripting harness called ‘Engine Block’ project. The CQL piece was built and supported within DataStax and battle tested.

In March of 2020, DataStax and the project maintainers open sourced this project, and was renamed to nosqlbench.io. More information on this link.

### runing the different samples workload
if you are using nb.jar file then command "java -jar nb.jar" otherwise use "nb" directly.
example -
1)
$ java -jar nb.jar start driver=stdout workload=nosqlb-lvl-1.yaml cycles=10
or
$ ./nb start driver=stdout workload=nosqlb-lvl-1.yaml cycles=10

2)
with schema phase option -
java -jar nb.jar start driver=stdout workload=nosqlb-lvl-2.yaml tags=phase:schema

with rampup phase option -
java -jar nb.jar start driver=stdout workload=nosqlb-lvl-2.yaml tags=phase:rampup cycles=10

3)
with main phase option -
java -jar nb.jar start driver=stdout workload=nosqlb-lvl-3.yaml tags=phase:main cycles=100

4)
with binding options
java -jar nb.jar start driver=stdout workload=bindings.yaml  cycles=10

example with CQL driver -
note - cassandra is running on localhost/127.0.0.1 with default port.
5)
with schema creation:
java -jar nb.jar start driver=cql workload=nosqlb-lvl-2.yaml tags=phase:schema hosts=127.0.0.1 localdc=datacenter1

6)
with ramp up phase:
java -jar nb.jar start driver=cql workload=nosqlb-lvl-2.yaml tags=phase:rampup hosts=127.0.0.1 localdc=datacenter1

7)
with ramp up phase cycle 100:
java -jar nb.jar start driver=cql workload=nosqlb-lvl-2.yaml tags=phase:rampup hosts=127.0.0.1 localdc=datacenter1 cycles=100

8)
with main phase cycle 10:
java -jar nb.jar start driver=cql workload=nosqlb-lvl-3.yaml tags=phase:main hosts=127.0.0.1 localdc=datacenter1 cycles=10

9)
For testing at scale, it is highly recommended that you set threads to a value higher than the default of 1. hint: you can use threads=auto for reasonable default, or consult the topic on threads with `help threads` for more information.
java -jar nb.jar start driver=cql workload=nosqlb-lvl-3.yaml tags=phase:main hosts=127.0.0.1 localdc=datacenter1 cycles=1M threads=auto
