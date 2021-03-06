# CPU Load Generator

A CPU Load generator that constantly increases the CPU utilization of a machine from 1% to 100%.
Forked from [SriramKeerthi-Gist](https://gist.github.com/SriramKeerthi/0f1513a62b3b09fecaeb) and added functionality.

## Instructions to execute the program
Four _command-line_ arguments can be specified.

* **stepSize** - TYPE: _decimal_ value in the range (0.0, 1.0). This specifies the increase in CPU load for every cycle.
* **duration** - TYPE: _number_. This specifies the number of milliseconds for which the CPU load needs to be maintained for, before being increased again.
* **isAlt** - TYPE: _boolean_. Consider a time slice to be 100ms. In the default state (when **isAlt** is *false*), CPU load is generated by making the current thread sleep for `(1 - load) * 100`ms. We could, however, generate the same CPU load with a different CPU usage pattern, such as an alternating one. When **isAlt** is *true*, CPU load is generated by making the current thread sleep multiple times, but for shorter durations, within the considered time slice (100ms). This leads to an alternating CPU usage pattern to create the same CPU load.
* **segments** - TYPE: _number_. This specifies the number of times the CPU usage alternates, when **isAlt** is set to true. Suppose, the time slice is 100ms, and **segments** = 2, then to generate a CPU load of 50%, the thread would sleep twice for 25ms, once every 50ms.


Run the following command to compile.
```commandline
javac SimulateConstIncreaseCPULoad.java
```

Run the following command to generate a non-alternating CPU load using default **stepSize** and default **duration**.
```commandline
java SimulateConstIncreaseCPULoad
```

Run the following command to generate a non-alternating CPU load with a **stepSize** of 1% and **duration** of 4000ms.
```commandline
java SimulateConstIncreaseCPULoad 0.01 4000
```

Run the following command to generate an alternating CPU load with a **stepSize** of 1%, a **duration** of 4000ms, and with 2 **segments**.
```commandline
java SimulateConstIncreaseCPULoad 0.01 4000 true 2
```

## Using the dockerized application
Use the dockerized application and run any one of the above commands,
```commandline
docker run pkaushi1/cpu-load-generator:v2 <command>
```
_Note:_ The above commands are also present in the Dockerfile. One could uncomment the required command, rebuild the docker image and then just run
```commandline
docker run <imagetag>
```

# Load Average Generator

A 1 minute load average generator that constantly increases the load average for the past minute.

## Instructions to execute the program
Two _command-line_ arguments can be specified.

* **START\_LOAD\_AVERAGE\_CORE** - TYPE: _decimal_ (default = 1/numCores). This specifies the starting value of 1min load average for a given core. This value signifies the number of processes that would be executed in the first minute.
* **STEP\_SIZE** - TYPE: _decimal_ (default = 0.2). This specifies the increase in load average that is to be generated every minute. 


Run the following command to compile.
```commandline
javac SimulateConstIncreaseLoadAverage.java
```

Run the following command to run the load average generator using the default values for START\_LOAD\_AVERAGE and STEP\_SIZE.
```commandline
java SimulateConstIncreaseLoadAverage
```

## Using the dockerized application
Use the dockerized application and run any one of the above commands,
```commandline
docker run pkaushi1/cpu-loadavg-generator:latest <command>
```
_Note:_ The above command is also set as the command to execute when the container is launched. So, one could just type the below command to run the load average generator.
```commandline
docker run pkaushi1/cpu-loadavg-generator:latest
```
