---
layout: single
title:  "Installing .venv and R kernel in Jupyter noteboook"
date:   2019-11-03 15:18:00 +0100
categories: python jupyter-notebook kernel
---

# Installing virtualenv kernel and registering
Activate your virtualenv, and install the IPykernel package

```bash
pip install ipykernel
```

Register the kernel installed in the virtualenv with the Jupyter environment
```bash
ipython kernel install --user --name=.venv
```

# Installing R kernel and registering
From [IRKernel](https://irkernel.github.io/installation/)

Open an R console and install the package IRkernel

```R
install.packages('IRkernel')
```

Register the kernel with the Jupyter environment with a kernelspec

```R
IRkernel::installspec()
# Or a systemwide install
IRkernel::installspec(user = FALSE)
```

# Choosing Kernel
Either define the kernel when creating a new notebook.
![Kernels in Jupyter Notebook](/images/jupyter-kernels.png)

Or by changing it inside the notebook itself.
![Kernels in Jupyter Notebook](/images/kernel-inside-notebook.png)

# Removing kernels
```bash
jupyter kernelspec uninstall kernel-name
```
