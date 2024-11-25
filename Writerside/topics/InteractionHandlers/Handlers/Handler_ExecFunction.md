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

You can use the Add Interaction Handler node [**documented here**](ItemInteractionHandlers.md#item-interaction-for-blueprints) to add this interaction to an item.

![HandlerNode_ExecFunction.png](HandlerNode_ExecFunction.png)

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
