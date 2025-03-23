---
layout: post
title:  "How to run HECTOR in Google Colab"
date:   2025-03-22 18:00:00 +0800
categories: RCM
---
How to run the HECTOR climate model:

## Run in Google Colab  

Create a new Colab notebook, and install the pyhector python library.

```bash
!pip install pyhector
```

```python
import pyhector

output = pyhector.run(pyhector.ssp126)
output
```

## Video

(Coming soon.)
