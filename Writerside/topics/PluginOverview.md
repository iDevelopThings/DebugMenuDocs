# Plugin Overview


The plugin is composed of multiple systems which all work together to provide the functionality.

To begin, from the outside, there's a "Window Manager", this basically hosts menus(but is not limited to hosting menus, but support is limited to c++ only)

This allows us to drag our menus around in the viewport, it also allows us to essentially minimize them and have multiple open at the same time.

When we create a Menu, it will create a window, and add the slate menu widget to our window as it's content.

Windows and Menus share an ID, this is how we can interact with our window/menu after it's created.

Our point of entry for a lot of the creation/interaction is provided via the ``UDebugMenuSubsystem`` this is a LocalPlayer SubSystem, and all menu/window lifetimes are tied to the LocalPlayer.


You can view [DebugMenuSubsystem](DebugMenuSubsystem.md) for more information on how to interact with the system/[create windows](DebugMenuSubsystem.md#creating-a-menu).
