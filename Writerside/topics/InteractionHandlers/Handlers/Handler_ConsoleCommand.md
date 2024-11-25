# Console Variable Interaction Handler

In short, this will add an item which is linked to CVar, and will toggle the value of the CVar when executed.

Right now, it assumes we can handle all items in a bool like state(on/off).

## Blueprints

<primary-label ref="bp-features"/>

Nodes:
<deflist>
<def title="Add Console Command Interaction">
Adds this interaction to the specified item

<code>UDebugMenu* Menu</code> - The menu to add the item to

<code>UDebugMenuItem* OptionalParent</code> - The parent item, menu root is used if not provided

<code>FString ConsoleVarName</code> - The name of the console variable

Returns the interaction handler
</def>
<def title="Create Console Command Item">
Creates a new item with this interaction

Inputs:

<code>UDebugMenu* Menu</code> - The menu to add the item to

<code>FString InDisplayName</code> - The display name of the item

<code>FString ConsoleVarName</code> - The name of the console variable

<code>UDebugMenuItem* Parent</code> - The parent item, menu root is used if not provided


Outputs:

<code>UDebugMenuItem* OutItem</code> - The created item

<code>UItemInteraction_ConsoleCommand* OutInteraction</code> - The created interaction
</def>
</deflist>


## C++

<primary-label ref="cpp-only"/>

C++ Users can use the [techniques/methods discussed here](ItemInteractionHandlers.md#item-interaction-handler-methods) to add this interaction to an item.

Simple example:

```C++
// If we have this CVar defined somewhere

static TAutoConsoleVariable<int32> CVarTestingInt32(
	TEXT("Testing.int32"),
	0,
	TEXT("Int32 test cvar"),
	ECVF_Default
);

Item->AddInteractionHandler<UItemInteraction_ConsoleCommand>("Testing.int32");
```
