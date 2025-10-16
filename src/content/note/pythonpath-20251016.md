---
title: How to set to use a custome module in python
description: How to set to use a custome module in python
publishDate: "2025-10-16T22:40:00Z"
---

To use custom module in python script, set PYTHONPATH environment variable to add the dir the custom module in.

```bash
export PYTHONPATH="/path/to/dir_module_in:$PYTHONPATH"

python script_using_custom_module.py
```

