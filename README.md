# SWIM Extension about Server Specification and Server Crashing

**About The Project**

This is the repository of the Self-Adaptive Software project about Server Specification and Server Crashing Extension of SWIM (A Simulator of Web Infrastructure and Management). The server specification extension is implemented by extending the Router class of Omnet++. It can be seen in [Router.h](https://github.com/yishakabreham/swim/blob/main/queueinglib/Router.h), [Router.cc](https://github.com/yishakabreham/swim/blob/main/queueinglib/Router.cc), and [Router.ned](https://github.com/yishakabreham/swim/blob/main/queueinglib/Router.ned). The server crash extension is implemented by new adaptation manager CrashAdaptationManager which can be seen in [CrashAdaptationManager.ned](https://github.com/yishakabreham/swim/blob/main/swim/src/managers/adaptation/CrashAdaptationManager.ned), [CrashAdaptationManager.cc](https://github.com/yishakabreham/swim/blob/main/swim/src/managers/adaptation/CrashAdaptationManager.cc), [CrashAdaptationManager.h](https://github.com/yishakabreham/swim/blob/main/swim/src/managers/adaptation/CrashAdaptationManager.h). 

**Installation**

This extension is built on the top of SWIM. SWIM uses Docker containers to automate deployment of the simulation into a virtual container. Docker is available for free at http://docker.com. Docker must be installed in your environment. The community edition is sufficient for running SWIM, which can be downloaded from here. SWIM itself is hosted on Docker Hub.

As mentioned, SWIM is hosted on Docker Hub, and online repository for Docker containers. You can follow the Creating and connecting to a container part [here](https://github.com/cps-sei/swim). Because we cannot build our docker image for the virtual machine, in order to use the extension there will be need manual setup to implement the extension. 

**Installation of Server Specification Extension**

In order to implement new algorithm we need to replace all the Router code in `~/seams-swim/queueinglib` with this [Router.h](https://github.com/yishakabreham/swim/blob/main/queueinglib/Router.h), [Router.cc](https://github.com/yishakabreham/swim/blob/main/queueinglib/Router.cc), and [Router.ned](https://github.com/yishakabreham/swim/blob/main/queueinglib/Router.ned). 

After that in `~/seams-swim/queueinglib` run the command `make` to take the effect. 

**Installation of Server Crashing Extension**

In order to implement server crashing extension we need to add new CrashAdaptationManager code in `~/seams-swim/swim/src/managers/adaptation`. The code that need to be added are [CrashingAdaptationManager.cc](https://github.com/yishakabreham/swim/blob/main/swim/src/managers/adaptation/CrashAdaptationManager.cc), [CrashingAdaptationManager.ned](https://github.com/yishakabreham/swim/blob/main/swim/src/managers/adaptation/CrashAdaptationManager.ned), and [CrashingAdaptationManager.h](https://github.com/yishakabreham/swim/blob/main/swim/src/managers/adaptation/CrashAdaptationManager.h). 

After that in `~/seams-swim/swim` run the command `make` to take the effect. 

**Running Server Specification Extension**

**Configuration:** 

The configuration to run server specification extension is defined in swim_sa.ned. In order to change the routing algorithm, routingAlgorithm under the LoadBalancer part can be defined. The supported algorithm now is “roundRobin” and “weightedRoundRobin”. In order to add server weight, serverWeight under LoadBalancer part can be defined with comma separated string (e.g. “3,2,1,1,1”). The sample is below: 

    loadBalancer: Router {
        @display("p=302,159");
        routingAlgorithm = "weightedRoundRobin";
        serverWeight = "3,2,1,1,1";
    }

**Run Extension**

To run the extension, it follows the SWIM way of running adaptation manager as a module. 

Start a Terminal Emulator from the Applications menu in the top-left corner. This opens a terminal within the container.
In this terminal, type the commands
   > cd ~/seams-swim/swim/simulations/swim_sa/
   > ./run.sh Reactive 1

**Getting Result**

After the simulation has finished, the results for this are put in the directory ~/seams-swim/results/SWIM_SA which defines a SQLite database of all the results. The results can be plotted using R (which is automated through a shell script) in either pdf or png format. In order to do so, open another terminal emulator, and type the commands below.

```
> cd ~/seams-swim/results/
> ../swim/tools/plotResults.sh SWIM_SA Reactive 1 plot.pdf (for pdf format)
OR 
> ../swim/tools/plotResults.sh SWIM_SA Reactive 1 plot.png (for png format)
```

The resulting plot will be saved as the file plot.pdf(or plot.png) in the results format.
 

**Running Server Crash Extension**

**Configuration:**

In order to configure the server crash extension, crashChance is used, which is defined in swim_sa.ini, and signifies the probability of a server crashing during one evaluation period. The implementation of the Crash Adaptation manager is done in the path   /src/managers/adaptation/ReactiveAdaptationManager.cc, and the extension can be run as follows.

**Run Extension:**

This follows the similar method for server specification extension, and the steps are as follow: 
Start a Terminal Emulator from the Applications menu in the top-left corner. This opens a terminal within the container.
In this terminal, type the commands
```
   > cd ~/seams-swim/swim/simulations/swim_sa/
   > ./run.sh Crash 1
```

**Getting Result**

Similarly, the results can be obtained in either pdf or png format as in the earlier case of Server Crash Extension.
```
> cd ~/seams-swim/results/
> ../swim/tools/plotResults.sh SWIM_SA Reactive 1 plot.pdf (for pdf format)
> OR
> ../swim/tools/plotResults.sh SWIM_SA Reactive 1 plot.png (for png format)
```
