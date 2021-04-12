---
sidebar_label: generator
title: rasa.core.nlg.generator
---

## NaturalLanguageGenerator Objects

```python
class NaturalLanguageGenerator()
```

Generate bot utterances based on a dialogue state.

#### generate

```python
 | async generate(template_name: Text, tracker: "DialogueStateTracker", output_channel: Text, **kwargs: Any, ,) -> Optional[Dict[Text, Any]]
```

Generate a response for the requested template.

There are a lot of different methods to implement this, e.g. the
generation can be based on templates or be fully ML based by feeding
the dialogue state into a machine learning NLG model.

#### create

```python
 | @staticmethod
 | create(obj: Union["NaturalLanguageGenerator", EndpointConfig, None], domain: Optional[Domain]) -> "NaturalLanguageGenerator"
```

Factory to create a generator.
