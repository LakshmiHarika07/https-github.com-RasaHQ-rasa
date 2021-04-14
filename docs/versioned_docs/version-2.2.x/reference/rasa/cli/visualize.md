---
sidebar_label: visualize
title: rasa.cli.visualize
---

#### add\_subparser

```python
add_subparser(subparsers: SubParsersAction, parents: List[argparse.ArgumentParser]) -> None
```

Add all visualization parsers.

**Arguments**:

- `subparsers` - subparser we are going to attach to
- `parents` - Parent parsers, needed to ensure tree structure in argparse
