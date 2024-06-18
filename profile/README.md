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

This organization contains multiple repositories spanning the Code Property Graph implementation itself as well as additional tooling and quality of life utilities.

### [Patched PHP](https://github.com/PHP-CPG/php-src)

We had to patch the original PHP interpreter to allow for the processing of constant strings.
This [repository](https://github.com/PHP-CPG/php-src) contains our patched version which we try to keep as up to date as possible.

### Code  Property Graph

Our Code Property Graph [repository](https://github.com/PHP-CPG/CPG) contains the code and tooling to convert PHP projects into a CPG.
We only support PHP Bytecode, but we plan to create passes for PHP Source Code eventually.
You can create a Docker container based on our Patched PHP interpreter, which takes a project and returns a finished CPG.

### Slicer

### Scala Master

### Plotter


