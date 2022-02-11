# jsspp2022_submission_data

This repository contains data, scripts, and code for making the research in a JSSPP'22 submission reproducible.

## Simulator code

The simulator is hosted in [another repository](https://github.com/wrench-project/scheduling_using_simulation_simulator). All experiments are
conducted with the simulator with commit tag `XXXX`. A Docker image is
provided in which the simulator is been installed in
`/usr/local/bin/scheduling_using_simulation_simulator`. The Docker file is 
available in `simulator/Dockerfile` directory. Cloning this repository into a
container for that image is likely the easiest way to run all scripts
mentioned hereafter. Here are the steps for building the image, starting a
container, and logging into it.

```
cd simulator/
docker build -t reproducible_research .
docker run -it --rm reproducible_research /bin/bash
cat README
```

## Workflow JSON files

All JSON workflow description files, which are [WfCommons instances](https://wfcommons.org/instances) used in this work are available in the `workflows` directory. 

## Script to run all simulations

A script to run all simulations is available in `run_script/run_all_simulations.py`. It requires that a Mongo daemon run locally, so that simulation output can be stored in a database.  This script takes as input a number of threads to use and a list of compute platform configurations to simulate. For instance, to run this script in the Docker container:

```
mkdir /tmp/db
mongod --dbpath=/tmp/db & 
cd jsspp2022_submission_data/run_scripts
./run_all_simulations.py 4 0,1,2,3,4,5,6,7,8
```

Note that the above will run for a VERY long time (we ran it on VMS on the
cloud, one per platform configuration, with 48 threads on each). We highly
recommend you use the provided database dump below.

## Simulation raw output

Simulation raw output is available as a Mongo database dump in the `mongo_db_dump` directory as a zipped archive, `simulation-result-dump.zip`. This is the output that was generating running the above script for all 9 platform configurations presented in the paper. 

Here are the steps to inject the database dump into a Mongo daemon that has been started locally:

```
mkdir /tmp/db
mongod --dbpath=/tmp/db &
cd jsspp2022_submission_data/mongo_db_dump/
unzip simulation-result-dump.zip
mongorestore simulation-result-dump
```

## Scripts to extract simulation output from Mongo

A script to extract and summarize simulation output data from the Mongo database is available in `extract_script/extract_all_results.py`. This script generates several `*.dict` files, which are also included in the `extract_script` directory.  If you want to run the script to (re-) generate these `*.dict` files, make sure that a Mongo daemon runs locally that has been fed the database dump in directory `mongo_db_dump` directory. 


## Scripts to plot/analyze the simulation output

Scripts to plot/analyze extracted simulation output data are available in the `plot_scripts` directory.  These scripts take as input the `*.dict` files available in the `extract_scripts` directory.

---
