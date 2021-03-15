---
sidebar_label: rasa.core.agent
title: rasa.core.agent
---

#### load\_from\_server

```python
async load_from_server(agent: "Agent", model_server: EndpointConfig) -> "Agent"
```

Load a persisted model from a server.

## Agent Objects

```python
class Agent()
```

The Agent class provides a convenient interface for the most important
Rasa functionality.

This includes training, handling messages, loading a dialogue model,
getting the next action, and handling a channel.

#### load

```python
 | @classmethod
 | load(cls, model_path: Text, interpreter: Optional[NaturalLanguageInterpreter] = None, generator: Union[EndpointConfig, NaturalLanguageGenerator] = None, tracker_store: Optional[TrackerStore] = None, lock_store: Optional[LockStore] = None, action_endpoint: Optional[EndpointConfig] = None, model_server: Optional[EndpointConfig] = None, remote_storage: Optional[Text] = None, path_to_model_archive: Optional[Text] = None) -> "Agent"
```

Load a persisted model from the passed path.

#### is\_core\_ready

```python
 | is_core_ready() -> bool
```

Check if all necessary components and policies are ready to use the agent.

#### is\_ready

```python
 | is_ready() -> bool
```

Check if all necessary components are instantiated to use agent.

Policies might not be available, if this is an NLU only agent.

#### parse\_message\_using\_nlu\_interpreter

```python
 | async parse_message_using_nlu_interpreter(message_data: Text, tracker: DialogueStateTracker = None) -> Dict[Text, Any]
```

Handles message text and intent payload input messages.

The return value of this function is parsed_data.

**Arguments**:

- `message_data` _Text_ - Contain the received message in text or\
  intent payload format.
- `tracker` _DialogueStateTracker_ - Contains the tracker to be\
  used by the interpreter.
  

**Returns**:

  The parsed message.
  

**Example**:

  
  {\
- `&quot;text&quot;` - &#x27;/greet{&quot;name&quot;:&quot;Rasa&quot;}&#x27;,\
- `&quot;intent&quot;` - {&quot;name&quot;: &quot;greet&quot;, &quot;confidence&quot;: 1.0},\
- `&quot;intent_ranking&quot;` - [{&quot;name&quot;: &quot;greet&quot;, &quot;confidence&quot;: 1.0}],\
- `&quot;entities&quot;` - [{&quot;entity&quot;: &quot;name&quot;, &quot;start&quot;: 6,\
- `&quot;end&quot;` - 21, &quot;value&quot;: &quot;Rasa&quot;}],\
  }

#### handle\_message

```python
 | async handle_message(message: UserMessage, message_preprocessor: Optional[Callable[[Text], Text]] = None, **kwargs, ,) -> Optional[List[Dict[Text, Any]]]
```

Handle a single message.

#### predict\_next

```python
 | async predict_next(sender_id: Text, **kwargs: Any) -> Optional[Dict[Text, Any]]
```

Handle a single message.

#### log\_message

```python
 | async log_message(message: UserMessage, message_preprocessor: Optional[Callable[[Text], Text]] = None, **kwargs: Any, ,) -> Optional[DialogueStateTracker]
```

Append a message to a dialogue - does not predict actions.

#### execute\_action

```python
 | async execute_action(sender_id: Text, action: Text, output_channel: OutputChannel, policy: Text, confidence: float) -> Optional[DialogueStateTracker]
```

Handle a single message.

#### trigger\_intent

```python
 | async trigger_intent(intent_name: Text, entities: List[Dict[Text, Any]], output_channel: OutputChannel, tracker: DialogueStateTracker) -> None
```

Trigger a user intent, e.g. triggered by an external event.

#### handle\_text

```python
 | async handle_text(text_message: Union[Text, Dict[Text, Any]], message_preprocessor: Optional[Callable[[Text], Text]] = None, output_channel: Optional[OutputChannel] = None, sender_id: Optional[Text] = DEFAULT_SENDER_ID) -> Optional[List[Dict[Text, Any]]]
```

Handle a single message.

If a message preprocessor is passed, the message will be passed to that
function first and the return value is then used as the
input for the dialogue engine.

The return value of this function depends on the ``output_channel``. If
the output channel is not set, set to ``None``, or set
to ``CollectingOutputChannel`` this function will return the messages
the bot wants to respond.

:Example:

&gt;&gt;&gt; from rasa.core.agent import Agent
&gt;&gt;&gt; from rasa.core.interpreter import RasaNLUInterpreter
&gt;&gt;&gt; agent = Agent.load(&quot;examples/moodbot/models&quot;)
&gt;&gt;&gt; await agent.handle_text(&quot;hello&quot;)
[u&#x27;how can I help you?&#x27;]

#### toggle\_memoization

```python
 | toggle_memoization(activate: bool) -> None
```

Toggles the memoization on and off.

If a memoization policy is present in the ensemble, this will toggle
the prediction of that policy. When set to ``False`` the Memoization
policies present in the policy ensemble will not make any predictions.
Hence, the prediction result from the ensemble always needs to come
from a different policy (e.g. ``TEDPolicy``). Useful to test
prediction
capabilities of an ensemble when ignoring memorized turns from the
training data.

#### load\_data

```python
 | async load_data(training_resource: Union[Text, TrainingDataImporter], remove_duplicates: bool = True, unique_last_num_states: Optional[int] = None, augmentation_factor: int = 50, tracker_limit: Optional[int] = None, use_story_concatenation: bool = True, debug_plots: bool = False, exclusion_percentage: Optional[int] = None) -> List[DialogueStateTracker]
```

Load training data from a resource.

#### train

```python
 | train(training_trackers: List[DialogueStateTracker], **kwargs: Any) -> None
```

Train the policies / policy ensemble using dialogue data from file.

**Arguments**:

- `training_trackers` - trackers to train on
- `**kwargs` - additional arguments passed to the underlying ML
  trainer (e.g. keras parameters)

#### persist

```python
 | persist(model_path: Text) -> None
```

Persists this agent into a directory for later loading and usage.

#### create\_processor

```python
 | create_processor(preprocessor: Optional[Callable[[Text], Text]] = None) -> MessageProcessor
```

Instantiates a processor based on the set state of the agent.
