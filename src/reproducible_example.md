# Reproducible Example


<div style="display: flex; align-items: center; margin: 20px 0;">
    <hr style="flex-grow: 0.05; border: 2px solid #009B77; margin: 0;">
    <span style="background: white; padding: 0 10px; font-weight: bold; color: #009B77;">Example:</span>
    <hr style="flex-grow: 1; border: 2px solid #009B77; margin: 0;">
</div>

```python
import prov4ml

prov4ml.start_run(
    prov_user_namespace="www.example.org",
    experiment_name="reproducible_example", 
    provenance_save_dir="prov",
    save_after_n_logs=100,
    collect_all_processes=True, 
)

prov4ml.log_source_code()
prov4ml.log_execution_command("python3 examples/reproducibility_example.py")

def square(x): 
    return x**2

for i in range(1, 10): 
    prov4ml.log_input(i)
    o = square(i)
    prov4ml.log_output(o)

prov4ml.end_run(True, True)
```

<hr style="border: 2px solid #009B77; margin: 20px 0;">



<div style="display: flex; justify-content: center; gap: 10px; margin-top: 20px;">
    <a href="prov_getters_example.md" style="text-decoration: none; background-color: #006269; color: white; padding: 10px 20px; border-radius: 5px; font-weight: bold; transition: 0.3s;">← Prev</a>
    <a href="." style="text-decoration: none; background-color: #006269; color: white; padding: 10px 20px; border-radius: 5px; font-weight: bold; transition: 0.3s;">🏠 Home</a>
    <a href="." style="text-decoration: none; background-color: #006269; color: white; padding: 10px 20px; border-radius: 5px; font-weight: bold; transition: 0.3s;">Next →</a>
</div>