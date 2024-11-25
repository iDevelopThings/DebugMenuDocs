# Exec Command(On/Off) Interaction Handler

This is basically the same as the [Exec Command](Handler_ExecCommand.md) handler, but with the ability to toggle the
command on/off.

We just internally store the "toggle" state, and execute the command with the provided on/off values.

![HandlerPreview_ExecToggleOnOff.gif](HandlerPreview_ExecToggleOnOff.gif)

## Blueprints

<primary-label ref="bp-features"/>


You can use the Add Interaction Handler node [**documented here**](ItemInteractionHandlers.md#item-interaction-for-blueprints) to add this interaction to an item.

![HandlerNode_ExecCommandOnOff.png](HandlerNode_ExecCommandOnOff.png)

<deflist>
<def title="Command">The command to execute</def>
<def title="OnValue">The string to use to set this command to it's "on" state</def>
<def title="OffValue">The string to use to set this command to it's "off" state</def>
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
