
# Example of usage with PyTorch

This section provides an example of how to use Prov4ML with PyTorch.

The following code snippet shows how to log metrics, system metrics, carbon metrics, and model versions in a PyTorch training loop.


<div style="display: flex; align-items: center; margin: 20px 0;">
    <hr style="flex-grow: 0.05; border: 2px solid #009B77; margin: 0;">
    <span style="background: white; padding: 0 10px; font-weight: bold; color: #009B77;">Example:</span>
    <hr style="flex-grow: 1; border: 2px solid #009B77; margin: 0;">
</div>


```python
for epoch in tqdm(range(EPOCHS)):
    for i, (x, y) in enumerate(train_loader):
        optim.zero_grad()
        y_hat = mnist_model(x)
        loss = F.cross_entropy(y_hat, y)
        loss.backward()
        optim.step()
        prov4ml.log_metric("MSE_train", loss, context=prov4ml.Context.TRAINING, step=epoch)
    
    # log system and carbon metrics (once per epoch), as well as the execution time
    prov4ml.log_carbon_metrics(prov4ml.Context.TRAINING, step=epoch)
    prov4ml.log_system_metrics(prov4ml.Context.TRAINING, step=epoch)
    # save incremental model versions
    prov4ml.save_model_version(mnist_model, f"mnist_model_version_{epoch}", prov4ml.Context.TRAINING, epoch)
     
```

<hr style="border: 2px solid #009B77; margin: 20px 0;">


<div style="display: flex; justify-content: center; gap: 10px; margin-top: 20px;">
    <a href="examples.md" style="text-decoration: none; background-color: #006269; color: white; padding: 10px 20px; border-radius: 5px; font-weight: bold; transition: 0.3s;">← Prev</a>
    <a href="." style="text-decoration: none; background-color: #006269; color: white; padding: 10px 20px; border-radius: 5px; font-weight: bold; transition: 0.3s;">🏠 Home</a>
    <a href="usage_lightning.md" style="text-decoration: none; background-color: #006269; color: white; padding: 10px 20px; border-radius: 5px; font-weight: bold; transition: 0.3s;">Next →</a>
</div>