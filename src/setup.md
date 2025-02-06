
# Setup

Before using the library, the user must set up the MLFlow execution, as well as library specific configurations: 

```python
prov4ml.start_run(
    prov_user_namespace: str,
    experiment_name: Optional[str] = None,
    provenance_save_dir: Optional[str] = None,
    collect_all_processes: Optional[bool] = False,
    save_after_n_logs: int = 100,
    rank : Optional[int] = None, 
    disable_codecarbon : bool = False,
)
```

The parameters are as follows:

| Parameter | Type     | Description                |
| :-------- | :------- | :------------------------- |
| `prov_user_namespace` | `string` | **Required**. User namespace for the provenance graph |
| `experiment_name` | `string` | **Required**. Name of the experiment |
| `provenance_save_dir` | `string` | **Required**. Directory to save the provenance graph |
| `collect_all_processes` | `bool` | **Optional**. Whether to collect all processes |
| `save_after_n_logs` | `int` | **Optional**. Save the graph after n logs |
| `rank` | `int` | **Optional**. Rank of the process |
| `disable_codecarbon` | `Optional[bool]` | **Optional**. Whether to use codecarbon to calculate stats. |

At the end of the experiment, the user must end the run:

```python
prov4ml.end_run(
    create_graph: Optional[bool] = False, 
    create_svg: Optional[bool] = False, 
)
```

| Parameter | Type     | Description                |
| :-------- | :------- | :------------------------- |
| `create_graph` | `bool` | **Optional**. Whether to create the graph |
| `create_svg` | `bool` | **Optional**. Whether to create the svg |

This call allows the library to save the provenance graph in the specified directory. 

<div style="background-color: #ffcc00; color: #333; padding: 15px; border-left: 5px solid #cc3300; font-weight: bold; margin: 20px; border-radius: 5px;">
    ⚠️ If create_svg is True then create_graph has to be necessairly set to True, as the creation of the former requires the latter. 
</div>


[Home](README.md) | [Prev](installation.md) | [Next](prov_graph.md)
