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

## Events

<secondary-label ref="bp"/>
<secondary-label ref="cpp"/>

For blueprints, you can bind to the `OnOptionSelectedDynamic` event

For C++, you can bind to the `OnOptionSelected` event

This is fired every time the currently selected option is changed, with the `FDebugItemOption` as the argument.

## Blueprints

<primary-label ref="bp-features"/>

Nodes:
<deflist>

<def title="Add Value Interaction">
Adds this interaction to the specified item

<code>UDebugMenu* Menu</code> - The menu to add the item to

<code>UDebugMenuItem* OptionalParent</code> - The parent item, menu root is used if not provided

<code>FBPItemInteractionValuePullValue InGetter</code> - Getter delegate to poll for new value

Returns the interaction handler
</def>

<def title="Create Value Interaction">
Creates a new item with this interaction

Inputs:

<code>UDebugMenu* Menu</code> - The menu to add the item to

<code>FString InDisplayName</code> - The display name of the item

<code>FBPItemInteractionValuePullValue InGetter</code> - Getter delegate to poll for new value

<code>UDebugMenuItem* Parent</code> - The parent item, menu root is used if not provided


Outputs:

<code>UDebugMenuItem* OutItem</code> - The created item

<code>UItemInteraction_Value* OutInteraction</code> - The created interaction
</def>

<def title="Create Value Interaction(Via Property Name)">
Creates a new item with this interaction - Allowing us to specify a UObject and a property name to pull the value from

Inputs:

<code>UDebugMenu* Menu</code> - The menu to add the item to

<code>FString InDisplayName</code> - The display name of the item

<code>UObject* ObjectInstance</code> - Object instance to pull the value from

<code>FName PropertyName</code> - Property name on the above object

<code>UDebugMenuItem* Parent</code> - The parent item, menu root is used if not provided


Outputs:

<code>UDebugMenuItem* OutItem</code> - The created item

<code>UItemInteraction_Value* OutInteraction</code> - The created interaction
</def>

</deflist>

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

