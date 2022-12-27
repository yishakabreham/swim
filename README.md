# swim

**About The Project**

This is the repository of the Self-Adaptive Software project about Server Specification and Server Crashing Extension of SWIM (A Simulator of Web Infrastructure and Management). The server specification extension is implemented by extending the Router class of Omnet++. It can be seen in this code. The server crash extension is implemented by new adaptation manager CrashAdaptationManager which can be seen here. 

**Installation**

This extension is built on the top of SWIM. SWIM uses Docker containers to automate deployment of the simulation into a virtual container. Docker is available for free at http://docker.com. Docker must be installed in your environment. The community edition is sufficient for running SWIM, which can be downloaded from here. SWIM itself is hosted on Docker Hub.

**Connecting to Docker**


**Running SWIM Extension**

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
 

**Server Specification Extension**

**Server Crash Extension**
**Configuration:**In order to configure the server crash extension, crashChance is used, which is defined in swim_sa.ini, and signifies the probability of a server crashing during one evaluation period. The implementation of the Crash Adaptation manager is done in the path   /src/managers/adaptation/ReactiveAdaptationManager.cc, and the extension can be run as follows.

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
