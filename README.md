# coral_singularity
Singularity image for the CORAL group at Washington University School of Medicine

[![https://www.singularity-hub.org/static/img/hosted-singularity--hub-%23e32929.svg](https://www.singularity-hub.org/static/img/hosted-singularity--hub-%23e32929.svg)](https://singularity-hub.org/collections/687)

To run on the CHPC cluster:

1. Login and then load singularity. No need to load cuda as only the driver is required on the host. Cuda will be installed in the singularity image. This is nice, because then we can install any cuda version we need (as long as it is compatible with the driver), and it will work.
```
load singularity
```

2. Pull the singularity image:
```
singularity pull shub://gdhugo/coral_singularity
```

If you want to pull a specific image:
```
singularity pull shub://gdhugo/coral_singularity:scikit
```

3. Invoke with GPU tools (--nv switch):
```
singularity shell --nv gdhugo-coral_singularity-master-latest.simg
```
