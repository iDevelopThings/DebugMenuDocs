# UDebugMenuItem

## Some available methods:

### Get Parent

<secondary-label ref="cpp"/>
<secondary-label ref="bp"/>

Returns the parent item that owns this widget
Root menu item will have no parent(nullptr)

```C++ 
UDebugMenuItem* GetParent() const
```

### Has Children

<secondary-label ref="cpp"/>
<secondary-label ref="bp"/>

Do we have any children?

```C++ 
bool HasChildren() const
```

### Get Child Count

<secondary-label ref="cpp"/>
<secondary-label ref="bp"/>

How many children do we have?

```C++ 
int32 GetChildCount() const
```

### Get Children

<secondary-label ref="cpp"/>
<secondary-label ref="bp"/>

Returns the direct child items of this item
NOTE: This does not include children of children, only direct children

```C++ 
TArray<UDebugMenuItem*> GetChildren() const
```

### Get Menu

<secondary-label ref="cpp"/>
<secondary-label ref="bp"/>

Returns the menu instance that owns this item

```C++ 
UDebugMenu* GetMenu() const
```

C++ can also use the templated version:

```C++
T* GetMenu() const
```

### Get Owning Player

<secondary-label ref="cpp"/>
<secondary-label ref="bp"/>

Returns the LocalPlayer that owns this menu.

```C++ 
ULocalPlayer* GetOwningPlayer() const
```

### Get Subsystem

<secondary-label ref="cpp"/>
<secondary-label ref="bp"/>

Returns the subsystem from the local player

```C++ 
UDebugMenuSubsystem* GetSubsystem() const
```

### Get Item Path

<secondary-label ref="cpp"/>
<secondary-label ref="bp"/>

Currently item paths arent used for anything, in the future, it'll allow us to easily use full paths for item
access/construction.

```C++ 
FString GetItemPath() const
```

### Get Display Name

<secondary-label ref="cpp"/>
<secondary-label ref="bp"/>

Returns the display name of the item, this is what will be shown in the UI

```C++ 
FString GetDisplayName() const
```

### Get Display Name As Text

<secondary-label ref="cpp"/>
<secondary-label ref="bp"/>

Same as above, but as FText

```C++ 
FText GetDisplayNameAsText() const
```

### Set Display Name

<secondary-label ref="cpp"/>
<secondary-label ref="bp"/>

Sets the display name of the item, this is what will be shown in the UI

```C++ 
UDebugMenuItem* SetDisplayName(const FString& InDisplayName)
```

### Get Description

<secondary-label ref="cpp"/>
<secondary-label ref="bp"/>

The description is kind of like a tooltip. When an item is focused in the
menu, if it has a description, it'll be shown to the right of the menu.

```C++ 
FString GetDescription() const
```

### Set Description

<secondary-label ref="cpp"/>
<secondary-label ref="bp"/>

Sets the description of the item, this is what will be shown in the UI

```C++ 
UDebugMenuItem* SetDescription(const FString& InDescription)
```



## Events(Blueprints/C++)

<primary-label ref="cpp-and-bp-support"/>

All of these events are available in both C++ and Blueprints
Blueprint versions are suffixed with `BP`

### OnItemAdded

<deflist>
    <def title="Menu">
        UDebugMenu* - The menu where the item was added
    </def>
    <def title="Parent">
        UDebugMenuItem* - The parent item
    </def>
    <def title="Item">
        UDebugMenuItem* - The item that was added
    </def>
</deflist>

### OnItemToggled

<deflist>
    <def title="Item">
        UDebugMenuItem* - The item that was toggled
    </def>
    <def title="bToggled">
        bool - The new state of the item
    </def>
</deflist>


### OnItemExpansionChange

<deflist>
    <def title="Item">
        UDebugMenuItem* - The item that was expanded/collapsed
    </def>
    <def title="bExpanded">
        bool - The new state of the item
    </def>
</deflist>

### OnItemExecute

<deflist>
    <def title="Item">
        UDebugMenuItem* - The item that was executed
    </def>
    <def title="Args">
        TArray&lt;FString&gt; - The arguments passed to the item
    </def>
</deflist>

### OnItemExecuteNoArgs

<deflist>
    <def title="Item">
        UDebugMenuItem* - The item that was executed
    </def>
</deflist>

### OnItemFocusChange

<deflist>
    <def title="Item">
        UDebugMenuItem* - The item that was focused
    </def>
    <def title="bFocused">
        bool - The new state of the item
    </def>
</deflist>