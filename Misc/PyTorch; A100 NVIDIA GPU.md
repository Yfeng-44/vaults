# Problem

```
nvidia-smi
```
Can show the GPU info but 
```
torch.cuda.is_available()
```
cannot.

# Reason
Use is not in the *video* linux user group, which make NVML cannot assign visibility to GPU.

# Workaround
`sudo usermod -a -G video username`
then reboot