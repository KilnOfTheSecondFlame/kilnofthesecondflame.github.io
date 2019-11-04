---
layout: single
title:  "Starting Tensorboard in a Jupyter notebook with a venv kernel"
date:   2019-11-04 18:11:00 +0100
categories: python jupyter-notebook tensorboard
---

# Install Tensorboard
Install Tensorboard in the same venv you will use in the Jupyter notebook (usually a dependency when you install TensorFlow and thus usually already installed)
```python
pip install tensorboard
```

# Start Tensorboard in the Jupyter notebook
You can use the jupyter magic for it
```python
%load_ext tensorboard
%tensorboard --logdir {logs_base}
```
![Jupyter Notebook tensorboard magic](/images/tensorboard-magic.png)

## pidfile for Tensorboard process (Windows)
I had the problem that Tensorboard tried to reuse an old instance that it thought still running. It turns out, that each Tensorboard process creates an Unix-style pidfile in `%TEMP%\.tensorboard-info`, which usually get's deleted before the kernel is terminated. But was still in the folder even though no python processes were running anymore. After deleting this file, a new process did start without a problem.

![Tensorboard pidfile in Windows](/images/tensorboard-pidfile.png)
