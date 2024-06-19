# PHP-CPG

Welcome to the PHP-CPG organization. This organization aims to collect, maintain, and distribute our PHP Code Property Graph implementation, related tooling, and references to projects using this code.

This organization was founded with our publication of `SSRF vs. Developers: A Study of SSRF-Defenses in PHP Applications`. 
If you depend on the CPG, please cite us:

```
@inproceedings{USENIX:Wessels:2024,
  title={SSRF vs. Developers: A Study of SSRF-Defenses in PHP Applications}
  authors={Wessels, Malte and Koch, Simon and Pellegrino, Giancarlo and Johns, Martin},
  venue={USENIX Security},
  year={2024}
}
``` 
## Repositories

This organization contains multiple repositories spanning the Code Property Graph implementation itself, as well as additional tooling and quality-of-life utilities.

### [Patched PHP](https://github.com/PHP-CPG/php-src)

We had to patch the original PHP interpreter to allow for the processing of constant strings in our bytecode dump.
Using our fork of the interpreter is a hard requirement, and we try to keep as up-to-date as possible.

### [Code Property Graph](https://github.com/PHP-CPG/CPG)

This repository contains the code and tooling to convert PHP projects into a CPG.
We only support PHP Bytecode but plan to eventually create passes for PHP Source Code.
You can create a Docker container based on our Patched PHP interpreter, which takes a project and returns a finished CPG, alleviating the dependency fuzzing.

### [Slicer](https://github.com/PHP-CPG/slicer)

We implemented the extraction of an inter-functional program slice from a bytecode CPG. 
It takes a function call as a slicing criterion and then extracts the DDG- and CFG-related subgraph.

### [Scala Master](https://github.com/PHP-CPG/scala-master)

This utility allows you to schedule and distribute tasks across multiple code property graphs, handling large scale static analysis experiments.

### [Plotter](https://github.com/PHP-CPG/plotter)

This useful utility allows you to visualize a given CPG (slice) using dot files and a corresponding converter.

## Create a Basic Large-Scale CPG Converter

While each repository has its own `README.md` we mean to give you a broad how-to here to get you up to speed.
This little tutorial only covers the build and deployment using docker to create a dummy scala-master instance which will iterate over a set of PHP projects, creating a CPG for each.
Please refer to the individual `README` files for more in-depth information.

### Dependencies

We have tested our instructions on a Linux machine (Arch) using Docker version 26.1.4, build 5650f9b102.

### Steps 

1. First, you must create the basic docker image containing our patched PHP interpreter. Everything else depends on it.
   The corresponding docker file is provided [here](https://github.com/PHP-CPG/CPG/tree/master/resources/docker/PHP-StringPatched).
   To build it, just clone our Code Property Graph [repository](https://github.com/PHP-CPG/CPG) and go to the linked folder.
   ```
   $> ./create.sh
   ```
   Be patient - this will take some time.
3. Next, we want to create the docker container containing our CPG converter. The corresponding file is provided [here](https://github.com/PHP-CPG/CPG/tree/master/resources/docker/multilayer-php-cpg).
   To build it, change the directory to the linked folder.
   ```
   $> ./create.sh
   ```
   Now you can already convert single projects into a CPG.
   ```
   $> ./run.sh /path/to/project/root/ /path/to/the/folder/to/store/the/cpg/
   ```
4. Our final step towards large-scale CPG creation is using the default scala-master.
   It comes equipped with an empty consumer and will take on the task of parallelizing our CPG creation process.
   Clone the scala-master [repository](https://github.com/PHP-CPG/scala-master) and switch to the [docker folder](https://github.com/PHP-CPG/scala-master/tree/master/resources/docker/template).
   ```
   $> ./create.sh
   ```
   Now you can point the scala master to a folder containing multiple PHP projects, and it will create CPGs (as best it can) for all of them.
   ```
   $> ./run.sh /path/to/folder/containing/multiple/projects/ /path/to/folder/to/put/cpgs/ /tmp/ [workerCount]
   // e.g. ./run.sh /php/projects/ /cpgs/ /tmp/ 8 - this will run 8 parallel CPG creation processes in parallel, no number means 10 processes
   ```

### Next Steps

You can now create CPGs automatically, in parallel, and scheduled, but you most likely also want to analyze them using your novel tool.
To do this, you first need to create a *consumer* - a tool that takes in a CPG, processes it, and then outputs the results in a JSON file.
You can integrate this into the presented toolchain by creating a new docker container based on the `scala-master`; you build the project within this container and then adapt the `main.conf` section for the consumer.
Point the `run` value towards the executable of your tool and adapt the `parameter` to suit your needs.
But bear in mind that the scala-master will only replace two values, `{cpg}` and `{out}`, in the parameter string. The first points towards the to-be-analyzed CPG, and the second defines the result output file.
When you have created your new Docker container, you can run it exactly as in step 4. A nice plus is that any already existing CPG will not be recreated to save time and CPU cycles.

Our [slicer](https://github.com/PHP-CPG/slicer) might help you analyze the CPG, and our [plotting utility](https://github.com/PHP-CPG/plotter) greatly helped us during development, so give them a look.

## Projects and Publications Using Us

```
@inproceedings{USENIX:Wessels:2024,
  title={SSRF vs. Developers: A Study of SSRF-Defenses in PHP Applications}
  authors={Wessels, Malte and Koch, Simon and Pellegrino, Giancarlo and Johns, Martin},
  venue={USENIX Security},
  year={2024}
}
``` 
