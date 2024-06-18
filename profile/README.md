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

This is a useful utility that allows you to visualize a given CPG (slice) using dot files and a corresponding converter.

## Usage

While each repository has its own `README` we mean to give you a broad how-to to get you up to speed.

## Projects and Publications Using Us

```
@inproceedings{USENIX:Wessels:2024,
  title={SSRF vs. Developers: A Study of SSRF-Defenses in PHP Applications}
  authors={Wessels, Malte and Koch, Simon and Pellegrino, Giancarlo and Johns, Martin},
  venue={USENIX Security},
  year={2024}
}
``` 
