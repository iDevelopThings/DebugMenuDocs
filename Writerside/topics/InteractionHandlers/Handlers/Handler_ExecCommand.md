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

You can use the Add Interaction Handler node [**documented here**](ItemInteractionHandlers.md#item-interaction-for-blueprints) to add this interaction to an item.

![HandlerNode_ExecCommand.png](HandlerNode_ExecCommand.png)

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
