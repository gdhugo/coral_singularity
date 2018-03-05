# coral_singularity
Singularity image for the CORAL group at Washington University School of Medicine

[![https://www.singularity-hub.org/static/img/hosted-singularity--hub-%23e32929.svg](https://www.singularity-hub.org/static/img/hosted-singularity--hub-%23e32929.svg)](https://singularity-hub.org/collections/687)

To run on the CHPC cluster:

1. Login and then load all required modules
```
load cuda-9.1
load singularity
```

2. Pull the singularity image:
```
singularity pull shub://gdhugo/coral_singularity
```

3. Invoke with GPU tools:
```
singularity shell --nv gdhugo-coral_singularity-master-latest.simg
```
