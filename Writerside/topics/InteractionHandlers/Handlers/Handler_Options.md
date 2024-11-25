# Options Interaction Handler

This lets us set a list of values which we can cycle through on the item.

An "Option" is the following struct:
```c++
USTRUCT(BlueprintType)
struct DEBUGMENU_API FDebugItemOption
{
	GENERATED_BODY()

	UPROPERTY(EditAnywhere, BlueprintReadWrite)
	int Index = 0;

	UPROPERTY(EditAnywhere, BlueprintReadWrite)
	FText Display;
};
```

## Events
<secondary-label ref="bp"/>
<secondary-label ref="cpp"/>

For blueprints, you can bind to the `OnOptionSelectedDynamic` event

For C++, you can bind to the `OnOptionSelected` event

This is fired every time the currently selected option is changed, with the `FDebugItemOption` as the argument.


## Blueprints

Blueprint users can use the following nodes to add an option to the interaction:

```C++
UItemInteraction_Options* AddOptionWithText(const FText& Display)
UItemInteraction_Options* AddOptionWithTextAndIndex(const int Index, const FText& Display)
UItemInteraction_Options* AddNewOption(const FDebugItemOption& Option)
```


<primary-label ref="bp-features"/>

Nodes:
<deflist>

<def title="Add Options Interaction">
Adds this interaction to the specified item

<code>UDebugMenu* Menu</code> - The menu to add the item to

<code>UDebugMenuItem* OptionalParent</code> - The parent item, menu root is used if not provided

<code>TArray&lt;FDebugItemOption&gt; InOptions</code> - A list of options to show

Returns the interaction handler
</def>

<def title="Create Options Interaction">
Creates a new item with this interaction

Inputs:

<code>UDebugMenu* Menu</code> - The menu to add the item to

<code>FString InDisplayName</code> - The display name of the item

<code>TArray&lt;FDebugItemOption&gt; InOptions</code> - A list of options to show

<code>UDebugMenuItem* Parent</code> - The parent item, menu root is used if not provided


Outputs:

<code>UDebugMenuItem* OutItem</code> - The created item

<code>UItemInteraction_Options* OutInteraction</code> - The created interaction
</def>

</deflist>

## C++

<primary-label ref="cpp-only"/>

C++ Users can use the following methods to add an option:

```C++
UItemInteraction_Options* AddOption(const FString& Display);
UItemInteraction_Options* AddOption(const FText& Display);
UItemInteraction_Options* AddOption(const int Index, const FString& Display);
UItemInteraction_Options* AddOption(const int Index, const FText& Display);
UItemInteraction_Options* AddOption(const FDebugItemOption& Option);
```

C++ Users can use the [techniques/methods discussed here](ItemInteractionHandlers.md#item-interaction-handler-methods)
to add this interaction to an item.

Simple example:

```C++

auto Handler = Item->AddInteractionHandler<UItemInteraction_Options>(TArray<FDebugItemOption>{
    {0, FText::FromString("Option 1")},
    {1, FText::FromString("Option 2")},
    {2, FText::FromString("Option 3")}
});
Handler->AddOption(TEXT("Another Option")); // Index will automatically be set to 3

```
