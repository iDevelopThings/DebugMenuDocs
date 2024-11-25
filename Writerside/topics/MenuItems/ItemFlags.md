# Menu Item Flags

``EDebugItemFlags`` enum helps us to define how the menu item behaves
``EDebugItemHandlingFlags`` enum helps specify additional flags for said above behavior

For the most part, we avoid subclassing UDebugMenuItem to provide functionalities, since this can be limiting.

## Item Flags

### GetItemFlags

<secondary-label ref="cpp"/>
<secondary-label ref="bp"/>

```C++ 
EDebugItemFlags GetItemFlags() const
```

### SetItemFlags

<secondary-label ref="cpp"/>
<secondary-label ref="bp"/>

```C++ 
UDebugMenuItem* SetItemFlags(const EDebugItemFlags InFlags)
```

### AddItemFlags

<secondary-label ref="cpp"/>
<secondary-label ref="bp"/>

```C++ 
UDebugMenuItem* AddItemFlags(const EDebugItemFlags InFlags)
```

### ToggleItemFlags

<secondary-label ref="cpp"/>
<secondary-label ref="bp"/>

```C++ 
UDebugMenuItem* ToggleItemFlags(const EDebugItemFlags InFlags, bool bToggleValue = true)
```

### EDebugItemFlags

<secondary-label ref="cpp"/>
<secondary-label ref="bp"/>

```C++ 
bool HasItemFlags(const EDebugItemFlags InFlags) const
```


## Handling Flags


### GetHandlingFlags

<secondary-label ref="cpp"/>
<secondary-label ref="bp"/>

```c++
EDebugItemHandlingFlags GetHandlingFlags() const
```

### SetHandlingFlags

<secondary-label ref="cpp"/>
<secondary-label ref="bp"/>

```c++
UDebugMenuItem* SetHandlingFlags(const EDebugItemHandlingFlags InHandlingFlags)
```

### AddHandlingFlags

<secondary-label ref="cpp"/>
<secondary-label ref="bp"/>

```c++
UDebugMenuItem* AddHandlingFlags(const EDebugItemHandlingFlags InHandlingFlags)
```

### ToggleHandlingFlags

<secondary-label ref="cpp"/>
<secondary-label ref="bp"/>

```c++
UDebugMenuItem* ToggleHandlingFlags(const EDebugItemHandlingFlags InHandlingFlags, bool bToggleValue = true)
```

### HasHandlingFlags

<secondary-label ref="cpp"/>
<secondary-label ref="bp"/>

```c++
bool HasHandlingFlags(const EDebugItemHandlingFlags InHandlingFlags) const
```
