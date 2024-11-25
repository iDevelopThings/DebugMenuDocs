# Exec Function Interaction Handler

In short, this lets us add an item which will call the provided UFUNCTION when we select the item.

If this function takes parameters, a simple modal like popup will show to input some values.

**NOTE:** this input only handles basic types right now.

If the function is defined on the CheatManager/CheatManagerExtension classes, then we'll try to find the active class
instance
and call the function on that instance.

Otherwise, we call all functions on ClassDefaultObjects, since we have no way to determine the correct instance to call
the function on.

**Its worth noting** these are just treated as a kind of fire and forget, we can't handle "toggles", parameters etc, since we have no way to reliably get that information.

## Blueprints

<primary-label ref="bp-features"/>

Nodes:
<deflist>

<def title="Add Exec Function Interaction">
Adds this interaction to the specified item

<code>UDebugMenu* Menu</code> - The menu to add the item to

<code>UDebugMenuItem* OptionalParent</code> - The parent item, menu root is used if not provided

<code>UFunction* InFunction</code> - A pointer to the UFunction we want to call

Returns the interaction handler
</def>

<def title="Create Exec Function Item(by ufunction ptr)">
Creates a new item with this interaction

Inputs:

<code>UDebugMenu* Menu</code> - The menu to add the item to

<code>FString InDisplayName</code> - The display name of the item

<code>UFunction* InFunction</code> - A pointer to the UFunction we want to call

<code>UDebugMenuItem* Parent</code> - The parent item, menu root is used if not provided


Outputs:

<code>UDebugMenuItem* OutItem</code> - The created item

<code>UItemInteraction_ExecFunction* OutInteraction</code> - The created interaction
</def>

<def title="Create Exec Function Item(by exec name)">
Creates a new item with this interaction

Inputs:

<code>UDebugMenu* Menu</code> - The menu to add the item to

<code>FString InDisplayName</code> - The display name of the item

<code>FString UFunctionName</code> - The name of the UFunction we want to call(this will search all ufunctions for a match)

<code>UDebugMenuItem* Parent</code> - The parent item, menu root is used if not provided


Outputs:

<code>UDebugMenuItem* OutItem</code> - The created item

<code>UItemInteraction_ExecFunction* OutInteraction</code> - The created interaction
</def>

</deflist>

## C++

<primary-label ref="cpp-only"/>

C++ Users can use the [techniques/methods discussed here](ItemInteractionHandlers.md#item-interaction-handler-methods)
to add this interaction to an item.

Simple example:

```C++

// If we have this class:
UCLASS()
class UMyClass : public UObject {
   GENERATED_BODY()
public:
    // Static is fine, we handle this
    UFUNCTION(Exec)
    static void SomeFunction(FString Param) { ... }
    
    // Gets called with the CDO
    UFUNCTION(Exec)
    void SomeOtherFunction(FString Param) { ... }
}


Item->AddInteractionHandler<UItemInteraction_ExecFunction>(
    UMyClass::StaticClass()->FindFunctionByName(TEXT("SomeFunction"))
);
Item->AddInteractionHandler<UItemInteraction_ExecFunction>(
    UMyClass::StaticClass()->FindFunctionByName(TEXT("SomeOtherFunction"))
);
```
