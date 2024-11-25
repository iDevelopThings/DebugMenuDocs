# Value Interaction Handler

The value handler lets us add an item which displays the provided value as a string so we can "watch" it.

This allows us to easily see the inner state of certain objects, or the result of certain calculations.

Currently there's only really two ways to handle this value pulling.

We can provide a "getter" delegate, which allows us to poll the getter for value changes.
This getter delegate must return a `FValueVariant` struct instance as a response. This allows us to return multiple
types as a single type, with blueprint support. It's not ideal, but it works.

Or we can provide a UObject and a member name, which will be used to pull the value from the UObject.

Currently we only support the following types:

- `int32`
- `float`
- `double`
- `bool`
- `FString`
- `uint8`

Here we're just setting a random value on the bp in tick, to show it working

![HandlerPreview_Value.gif](HandlerPreview_Value.gif)

## Blueprints

<primary-label ref="bp-features"/>

You can use the Add Interaction Handler node [**documented here**](ItemInteractionHandlers.md#item-interaction-for-blueprints) to add this interaction to an item.

![HandlerNode_Value.png](HandlerNode_Value.png)

## Extra

<primary-label ref="cpp-and-bp-support"/>

A value getter can be set via the `SetValueGetter` function

```C++
UFUNCTION(BlueprintCallable, Category = "DebugMenu|Interactions")
virtual void SetValueGetter(FBPItemInteractionValuePullValue InGetter)
```

A value can also be manually supplied via the `SetValue` function

```C++
UFUNCTION(BlueprintCallable, Category = "DebugMenu|Interactions", DisplayName="Set Value", meta=(ToolTip="Set the value displayed"))
virtual void SetValue(const FValueVariant& InValue)
```

## C++

<primary-label ref="cpp-only"/>

C++ Users can use the [techniques/methods discussed here](ItemInteractionHandlers.md#item-interaction-handler-methods)
to add this interaction to an item.

Simple example:

```C++
auto Handler = Item->AddInteractionHandler<UItemInteraction_Value>();
Handler.OnGetValue.BindLambda([SomeClass](UItemInteraction_Value* Interaction)
{
    return FValueVariant(SomeClass->SomeInt);
});
```

