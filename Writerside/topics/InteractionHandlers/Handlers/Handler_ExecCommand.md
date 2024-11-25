# Exec Command Interaction Handler

This is very similar to the [Console Command](Handler_ConsoleCommand.md) & [Exec Function](Handler_ExecFunction.md)
handlers.

However, with the console command handler, it only works with CVars, and with the Exec Function handler, you need to
provide a UFUNCTION to execute.

What if we just want to execute a regular cheat manager/exec command without finding it and such?

Well, that's what this does.

Commands are first routed to the cheat local players `Exec()` function, and then to GEngine's `Exec()` function.

## Blueprints

<primary-label ref="bp-features"/>

Nodes:
<deflist>

<def title="Add Exec Command Interaction">
Adds this interaction to the specified item

<code>UDebugMenu* Menu</code> - The menu to add the item to

<code>UDebugMenuItem* OptionalParent</code> - The parent item, menu root is used if not provided

<code>FString InCommand</code> - The command string to execute

Returns the interaction handler
</def>

<def title="Create Exec Command Item">
Creates a new item with this interaction

Inputs:

<code>UDebugMenu* Menu</code> - The menu to add the item to

<code>FString InDisplayName</code> - The display name of the item

<code>FString InCommand</code> - The command string to execute

<code>UDebugMenuItem* Parent</code> - The parent item, menu root is used if not provided


Outputs:

<code>UDebugMenuItem* OutItem</code> - The created item

<code>UItemInteraction_ExecCommand* OutInteraction</code> - The created interaction
</def>

</deflist>

## C++

<primary-label ref="cpp-only"/>

C++ Users can use the [techniques/methods discussed here](ItemInteractionHandlers.md#item-interaction-handler-methods)
to add this interaction to an item.

Simple example:

```C++

Item->AddInteractionHandler<UItemInteraction_ExecCommand>(
    "stat fps"
);

```
