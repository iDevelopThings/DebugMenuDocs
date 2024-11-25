# Item Interaction Handlers

Since we avoid subclassing menu item, behaviours are added through interaction handlers.

These handlers are added to the item and are responsible for handling the interactions.

But not just that, they also receive the events from the item and can modify the item's behaviour.

## Item Interaction handler methods

<primary-label ref="cpp-only"/>

Various methods for working with interaction handlers on an Item.
Most of them are used internally, but are also public for you to use.

### CallInteractionHandlerMethod

Calls the specified handler method on the specified handler, with the specified arguments.

```C++
template <typename InteractionType, typename... TArgs>
void CallInteractionHandlerMethod(
    InteractionType* Handler,
    void (InteractionType::*Method)(TArgs...),
    TArgs&&... Args
)
```

Example:

```C++
CallInteractionHandlerMethod(Handler, &UDebugItemInteraction::OnAddedToParent);
```

### CallInteractionHandlerMethodOnAll

Calls the specified handler method on all handlers attached to this item, with the specified arguments.

```C++
template <typename InteractionType, typename... TArgs>
void CallInteractionHandlerMethodOnAll(
    void (InteractionType::*Method)(TArgs...),
    TArgs... Args
)
```

Example:

```C++
CallInteractionHandlerMethodOnAll(&UDebugItemInteraction::OnAddedToParent);
```

### ForEachHandler

Simple method to iterate over all handlers attached to this item.

```C++
void ForEachHandler(const TFunctionRef<void(UDebugItemInteraction* Handler)>& Fn)
```

### GetInteractionHandler

Gets the handler of the specified type.

```C++
template <typename T>
T* GetInteractionHandler()
```

Example:

```C++
Item->GetInteractionHandler<UItemInteraction_ExecCommand>();
```

### AddInteractionHandler

Adds an interaction handler of the specified type to our item

The args passed are forwarded to the handlers `Initialize` method.

```C++
template <typename T, typename... InArgTypes>
T* AddInteractionHandler(InArgTypes&&... Args)
```

Example:

```C++
Item->AddInteractionHandler<UItemInteraction_ExecFunction>(
   /* UFunction* */ InFunction
);
```

### AddInteractionHandlerWithBuilder

Similar to `AddInteractionHandler` but allows us to pass a builder function to run extra construction logic before the
handler is fully initialized.

```C++
template <typename T, typename... InArgTypes>
T* AddInteractionHandlerWithBuilder(
    TFunctionRef<void(T* Handler)> BuilderFn,
    InArgTypes&&... Args
)
```

For example, with the previous example, we might decide to specify the function a different way:

```C++
UClass* SomeClassRef = ... ;
Item->AddInteractionHandlerWithBuilder<UItemInteraction_ExecFunction>(
    [InFunction](UItemInteraction_ExecFunction* Handler) {
        Handler->Function = SomeClassRef->FindFunctionByName( ... );
    }
);
```




## Item Interaction for blueprints

<primary-label ref="bp-features"/>

Now... for blueprint users, it's a bit more difficult. 

For the majority of built in interactions, I've provided methods that you can call to add the interaction.

Let's take the [`UItemInteraction_Value`](Handler_Value.md) interaction as an example

To clarify, this interaction adds an item to our menu, which lets us watch a provided value(which also works with BP).
So if you have a float value you want to watch, you can use this interaction to do so.

This interaction has `Add Value Interaction` `Create Value Interaction` `Create Value Interaction(Via Property Name)` nodes.

All provided interactions follow this same naming convention of:

`Add {Name} Interaction` - Adds this interaction to a provided item

`Create {Name} Interaction` - Creates a new item and adds this interaction to it