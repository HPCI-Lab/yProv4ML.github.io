
# Reproducing Experiments using Provenance Files

With workflow streamlined by yProv4ML, it is trivial to guarantee reproducibility of experiments even just sharing a single provenance file. 
To guarantee the necessary amount of information are present in the prov.json file however, some calls to the library have to be executed. 

```python
log_execution_command(cmd : str)
```

Simply logs the execution command for it to be retrieved by the reproduction script later. This is often a call to python3

```python
log_source_code(path: str = None)
```

Logs as an artifact a path to the source code. This could be a single python file (e.g. main.py), a repository link (if the path is not specified in the arguments), or an entire directory of source files. 
In case the source code is not on github, the source files are all copied inside the artifacts directory, and the path logged inside the provenance file will reference whis copy. 

```python
log_input(inp, log_copy_in_prov_directory=True)
```

The directive `log_input` saves with incremental ids a various number of inputs, which are user defined. 

```python
log_output(out, log_copy_in_prov_directory=True)
```

The directive `log_output` saves with incremental ids a various number of outputs, which are user defined. 

```admonish warning
Currently, the order of logging of inputs and outputs does matter, which means that concurrent executions will have to log information in order, for a run to be considered reproducible. 
```

[Home](README.md) | [Prev](registering_metrics.md) | [Next](usage_pytorch.md)
