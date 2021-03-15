---
sidebar_label: validator
title: rasa.validator
---

## Validator Objects

```python
class Validator()
```

A class used to verify usage of intents and utterances.

#### \_\_init\_\_

```python
 | __init__(domain: Domain, intents: TrainingData, story_graph: StoryGraph) -> None
```

Initializes the Validator object.

#### from\_importer

```python
 | @classmethod
 | async from_importer(cls, importer: TrainingDataImporter) -> "Validator"
```

Create an instance from the domain, nlu and story files.

#### verify\_intents

```python
 | verify_intents(ignore_warnings: bool = True) -> bool
```

Compares list of intents in domain with intents in NLU training data.

#### verify\_example\_repetition\_in\_intents

```python
 | verify_example_repetition_in_intents(ignore_warnings: bool = True) -> bool
```

Checks if there is no duplicated example in different intents.

#### verify\_intents\_in\_stories

```python
 | verify_intents_in_stories(ignore_warnings: bool = True) -> bool
```

Checks intents used in stories.

Verifies if the intents used in the stories are valid, and whether
all valid intents are used in the stories.

#### verify\_utterances

```python
 | verify_utterances(ignore_warnings: bool = True) -> bool
```

Compares list of utterances in actions with utterances in responses.

#### verify\_utterances\_in\_stories

```python
 | verify_utterances_in_stories(ignore_warnings: bool = True) -> bool
```

Verifies usage of utterances in stories.

Checks whether utterances used in the stories are valid,
and whether all valid utterances are used in stories.

#### verify\_story\_structure

```python
 | verify_story_structure(ignore_warnings: bool = True, max_history: Optional[int] = None) -> bool
```

Verifies that the bot behaviour in stories is deterministic.

**Arguments**:

- `ignore_warnings` - When `True`, return `True` even if conflicts were found.
- `max_history` - Maximal number of events to take into account for conflict identification.
  

**Returns**:

  `False` is a conflict was found and `ignore_warnings` is `False`.
  `True` otherwise.

#### verify\_nlu

```python
 | verify_nlu(ignore_warnings: bool = True) -> bool
```

Runs all the validations on intents and utterances.

#### verify\_domain\_validity

```python
 | verify_domain_validity() -> bool
```

Checks whether the domain returned by the importer is empty.

An empty domain is invalid.
