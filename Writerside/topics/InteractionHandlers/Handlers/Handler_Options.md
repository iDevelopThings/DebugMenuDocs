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

![HandlerPreview_Options.gif](HandlerPreview_Options.gif)

## Events

<secondary-label ref="bp"/>
<secondary-label ref="cpp"/>

For blueprints, you can bind to the `OnOptionSelectedDynamic` event

For C++, you can bind to the `OnOptionSelected` event

This is fired every time the currently selected option is changed, with the `FDebugItemOption` as the argument.

## Blueprints

<primary-label ref="bp-features"/>

You can use the Add Interaction Handler node [**documented here**](ItemInteractionHandlers.md#item-interaction-for-blueprints) to add this interaction to an item.

![HandlerNode_Options.png](HandlerNode_Options.png)

Blueprint users can use the following nodes to add an option to the interaction:

```C++
UItemInteraction_Options* AddOptionWithText(const FText& Display)
UItemInteraction_Options* AddOptionWithTextAndIndex(const int Index, const FText& Display)
UItemInteraction_Options* AddNewOption(const FDebugItemOption& Option)
```

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
