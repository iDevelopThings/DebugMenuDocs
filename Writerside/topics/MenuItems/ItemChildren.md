# Menu Item Children

``EDebugItemFlags`` enum helps us to define how the menu item behaves
``EDebugItemHandlingFlags`` enum helps specify additional flags for said above behavior

For the most part, we avoid subclassing UDebugMenuItem to provide functionalities, since this can be limiting.

## Adding Children(From Blueprint)

<primary-label ref="bp-features"/>

There's a global `Add Item` blueprint node that allows you to add children to a menu/item

```C++
UFUNCTION(BlueprintCallable, Category = "DebugMenu|Item", DisplayName = "Add Item", meta=(ToolTip = "Adds a child item to this item", DefaultToSelf = "InMenu"))
static UDebugMenuItem* AddChildItem(
    UDebugMenu* InMenu,
    UPARAM(DisplayName = "Parent")
    UDebugMenuItem* InParent,
    UPARAM(DisplayName = "Name")
    const FString& InName,
    UPARAM(DisplayName = "Custom Widget Class", meta=(MustImplement="/Script/DebugMenu.DebugMenuItemWidgetInterface", AdvancedDisplay))
    TSubclassOf<UUserWidget> ItemClass = nullptr
);
```

You can also add items from a DataTable, but, these are for very specific functionalities...

```C++
UFUNCTION(BlueprintCallable, Category = "DebugMenu|Item", DisplayName = "Add Items(From DataTable)", meta=(ToolTip = "Populate items from a datatable", DefaultToSelf = "InMenu"))
static void AddItemsFromDataTable(
    UDebugMenu* InMenu,
    UDebugMenuItem* InParent,
    UPARAM(meta=(RequiredAssetDataTags = "RowStructure=/Script/DebugMenu.DebugItemTableRow")) 
    UDataTable* DataTable
);
```

## Adding Children(From C++)

<primary-label ref="cpp-only"/>

There exists a few methods to easily add children to an item

```C++
typedef TFunctionRef<void(UDebugMenuItem* Item)> FConstructFn;

UDebugMenuItem* AddChild(const FString& InName, FConstructFn ConstructFn)
UDebugMenuItem* AddExpandableChild(const FString& InName, FConstructFn ConstructFn)
UDebugMenuItem* AddToggleableChild(const FString& InName, FConstructFn ConstructFn)
```

``ConstructFn`` parameter is a "builder" function that allows you to construct the child item with the desired
properties/functionality.

For example:

```C++
Item->AddChild("FPS", [this](UDebugMenuItem* Item) {
    Item->AddInteractionHandler<UItemInteraction_ExecCommandWithOnOff>(
    "stat fps",
    "on", "off"
    );
});
Item->AddChild("Group Name", [this](UDebugMenuItem* Item) {
    Item->AddChild("Child Name", [this](UDebugMenuItem* Item) {
        ....
    });
});
```
