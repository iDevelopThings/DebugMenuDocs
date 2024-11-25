# Exec Command(On/Off) Interaction Handler
This is basically the same as the [Exec Command](Handler_ExecCommand.md) handler, but with the ability to toggle the command on/off.

We just internally store the "toggle" state, and execute the command with the provided on/off values.

## Blueprints

<primary-label ref="bp-features"/>

Nodes:
<deflist>

<def title="Add Exec Command(with on/off) Interaction">
Adds this interaction to the specified item

<code>UDebugMenu* Menu</code> - The menu to add the item to

<code>UDebugMenuItem* OptionalParent</code> - The parent item, menu root is used if not provided

<code>FString InCommand</code> - The command string to execute

<code>FString InOnValue</code> - For example "on" or "1"

<code>FString InOffValue</code> - For example "off" or "0"

Returns the interaction handler
</def>

<def title="Create Exec Command(with on/off) Item">
Creates a new item with this interaction

Inputs:

<code>UDebugMenu* Menu</code> - The menu to add the item to

<code>FString InDisplayName</code> - The display name of the item

<code>FString InCommand</code> - The command string to execute

<code>FString InOnValue</code> - For example "on" or "1"

<code>FString InOffValue</code> - For example "off" or "0"

<code>UDebugMenuItem* Parent</code> - The parent item, menu root is used if not provided


Outputs:

<code>UDebugMenuItem* OutItem</code> - The created item

<code>UItemInteraction_ExecCommandWithOnOff* OutInteraction</code> - The created interaction
</def>

</deflist>

## C++

<primary-label ref="cpp-only"/>

C++ Users can use the [techniques/methods discussed here](ItemInteractionHandlers.md#item-interaction-handler-methods)
to add this interaction to an item.

Simple example:

```C++

Item->AddInteractionHandler<UItemInteraction_ExecCommandWithOnOff>(
    "stat fps",
    "1", "0"
);

```
