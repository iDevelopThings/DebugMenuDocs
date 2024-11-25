# UDebugMenuSubsystem

## Accessing the subsystem

From blueprints, there's 3 blueprint functions you can use.

``GetDebugMenu`` - This takes a WorldContextObject, and gets the first player controller in the world. Not great, but
can be fine sometimes.

``GetDebugMenuFromLocalPlayer`` - Takes a local player, and gets the subsystem from that.

``GetDebugMenuFromPlayerController`` - Takes a player controller, and gets the subsystem from that.

C++ is basically the same, but we just have override functions.

```C++
static UDebugMenuSubsystem* Get(const UObject* WorldContextObject = nullptr);
static UDebugMenuSubsystem* Get(const ULocalPlayer* LocalPlayer);
static UDebugMenuSubsystem* Get(const APlayerController* PlayerController);
```

## Debug Menus

### Creating a Menu

`CreateMenu` will create our UDebugMenu instance and add it to the system, it's not added to our window manager or
viewport yet.
This allows us to configure it before we show it.

```C++
UDebugMenu* CreateMenu(
    FName Id,
    FString Title,
    TSubclassOf<UDebugMenu> MenuClass = nullptr,
    UDebugMenu* Template              = nullptr
);
```

<table>
    <tr>
        <td>Param</td>
        <td>Info</td>
    </tr>
    <tr>
        <td><code>Id</code></td>
        <td>This should be a unique ID to identify your window & menu, this will allow us to access it in the future via this id.</td>
    </tr>
    <tr>
        <td><code>Title</code></td>
        <td>This is the title displayed on any of the UI.</td>
    </tr>
    <tr>
        <td><code>MenuClass</code></td>
        <td>If you've subclassed UDebugMenu in C++ or Blueprint, this will be used to create your menu, otherwise it'll use the default.</td>
    </tr>
    <tr>
        <td><code>Template</code></td>
        <td>If provided, it'll be used to instantiate your menu, most of the time this can be left null, it's just an option provided to `NewObject`, incase you need it.</td>
    </tr>
</table>

### ``ActivateDebugMenu(FName Id)``

This is just shorthand for `Menu->Activate();`
If the menu is not added to the viewport/window manager yet, it'll run all the creation/initialization

### ``DeactivateDebugMenu(FName Id)``

This is just shorthand for `Menu->Deactivate();`

If our menu is active, it'll run all the cleanup/destruction logic.

### ``UDebugMenu* GetMenu(FName Id) const``

Allows us to grab a menu via its ID.

C++ also has a templated version:  ```T* GetMenu(FName Id) const```

## Window Manager Interaction

### ``DestroyWindowManager``

This will completely destroy the manager and all windows/menus associated with it.
I just exposed this so it's there if you need it, but it's mainly just used during cleanup/subsystem de-init.

### ``ToggleWindowManager``

This will allow us to toggle the visibility of the window manager. Completely hiding all of it's ui.

### ``IsWindowManagerHidden``

This will return if the window manager is hidden or not.

### ``ShowWindowManager``

This will show the window manager if it's hidden.

### ``HideWindowManager``

This will hide the window manager if it's shown.