
# Example of usage with PyTorch Lightning

This section provides an example of how to use Prov4ML with PyTorch Lightning.

In any lightning module the calls to `train_step`, `validation_step`, and `test_step` can be overridden to log the necessary information.

<div style="display: flex; align-items: center; margin: 20px 0;">
    <hr style="flex-grow: 0.05; border: 2px solid #009B77; margin: 0;">
    <span style="background: white; padding: 0 10px; font-weight: bold; color: #009B77;">Example:</span>
    <hr style="flex-grow: 1; border: 2px solid #009B77; margin: 0;">
</div>


```python
def training_step(self, batch, batch_idx):
    x, y = batch
    y_hat = self(x)
    loss = self.loss(y_hat, y)
    prov4ml.log_metric("MSE_train", loss, prov4ml.Context.TRAINING, step=self.current_epoch)
    prov4ml.log_flops_per_batch("train_flops", self, batch, prov4ml.Context.TRAINING,step=self.current_epoch)
    return loss
```


<hr style="border: 2px solid #009B77; margin: 20px 0;">

This will log the mean squared error and the number of flops per batch for each the training step.

Alternatively, the `on_train_epoch_end` method can be overridden to log information at the end of each epoch.

<div style="display: flex; align-items: center; margin: 20px 0;">
    <hr style="flex-grow: 0.05; border: 2px solid #009B77; margin: 0;">
    <span style="background: white; padding: 0 10px; font-weight: bold; color: #009B77;">Example:</span>
    <hr style="flex-grow: 1; border: 2px solid #009B77; margin: 0;">
</div>

```python
def on_train_epoch_end(self) -> None:
    prov4ml.log_metric("epoch", self.current_epoch, prov4ml.Context.TRAINING, step=self.current_epoch)
    prov4ml.save_model_version(self, f"model_version_{self.current_epoch}", prov4ml.Context.TRAINING, step=self.current_epoch)
    prov4ml.log_system_metrics(prov4ml.Context.TRAINING,step=self.current_epoch)
    prov4ml.log_carbon_metrics(prov4ml.Context.TRAINING,step=self.current_epoch)
    prov4ml.log_current_execution_time("train_epoch_time", prov4ml.Context.TRAINING, self.current_epoch)
```

<hr style="border: 2px solid #009B77; margin: 20px 0;">


<div style="display: flex; justify-content: center; gap: 10px; margin-top: 20px;">
    <a href="usage_pytorch.md" style="text-decoration: none; background-color: #006269; color: white; padding: 10px 20px; border-radius: 5px; font-weight: bold; transition: 0.3s;">← Prev</a>
    <a href="." style="text-decoration: none; background-color: #006269; color: white; padding: 10px 20px; border-radius: 5px; font-weight: bold; transition: 0.3s;">🏠 Home</a>
    <a href="usage_itwinAI_logger.md" style="text-decoration: none; background-color: #006269; color: white; padding: 10px 20px; border-radius: 5px; font-weight: bold; transition: 0.3s;">Next →</a>
</div>

# Example of usage with PyTorch Lightning Logger

When integrating with lightning, a much easier way to produce the provenance graph is through the ProvMLLogger. 

<div style="display: flex; align-items: center; margin: 20px 0;">
    <hr style="flex-grow: 0.05; border: 2px solid #009B77; margin: 0;">
    <span style="background: white; padding: 0 10px; font-weight: bold; color: #009B77;">Example:</span>
    <hr style="flex-grow: 1; border: 2px solid #009B77; margin: 0;">
</div>


```python
trainer = L.Trainer(
    accelerator="cuda",
    devices=1,
    max_epochs=EPOCHS,
    enable_checkpointing=False, 
    log_every_n_steps=1, 
    logger=[prov4ml.ProvMLLogger()],
)
```

<hr style="border: 2px solid #009B77; margin: 20px 0;">

When logging in such a way, there is no need to call the start_run and end_run directives, and everything will be logged automatically. 
If necessary, it's still possible to call all yprov4ml directives, such as log_param and log_metrics, and the data will be saved in the current execution directory. 