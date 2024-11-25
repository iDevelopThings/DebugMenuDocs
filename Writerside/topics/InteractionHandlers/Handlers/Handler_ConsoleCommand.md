# Console Variable Interaction Handler

In short, this will add an item which is linked to CVar, and will toggle the value of the CVar when executed.

Right now, it assumes we can handle all items in a bool like state(on/off).

Preview:

![HandlerPreview_ConsoleCommandToggle.gif](HandlerPreview_ConsoleCommandToggle.gif)

## Blueprints

<primary-label ref="bp-features"/>

You can use the Add Interaction Handler node [**documented here**](ItemInteractionHandlers.md#item-interaction-for-blueprints) to add this interaction to an item.

![HandleNoder_ConsoleCommand.png](HandleNoder_ConsoleCommand.png)

## C++

<primary-label ref="cpp-only"/>

C++ Users can use the [techniques/methods discussed here](ItemInteractionHandlers.md#item-interaction-handler-methods)
to add this interaction to an item.

Simple example:

```C++
// If we have this CVar defined somewheres

static TAutoConsoleVariable<int32> CVarTestingInt32(
	TEXT("Testing.int32"),
	0,
	TEXT("Int32 test cvar"),
	ECVF_Default
);

Item->AddInteractionHandler<UItemInteraction_ConsoleCommand>("Testing.int32");
```
