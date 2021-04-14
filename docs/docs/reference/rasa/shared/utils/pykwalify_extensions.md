---
sidebar_label: pykwalify_extensions
title: rasa.shared.utils.pykwalify_extensions
---

This module regroups custom validation functions, and it is
loaded as an extension of the pykwalify library:

https://pykwalify.readthedocs.io/en/latest/extensions.html#extensions

#### require\_response\_keys

```python
require_response_keys(responses: List[Dict[Text, Any]], _: Dict, __: Text) -> bool
```

Validates that response dicts have either the &quot;text&quot; key or the &quot;custom&quot; key.
