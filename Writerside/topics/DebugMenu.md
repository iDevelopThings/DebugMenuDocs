# UDebugMenu

To create a menu you can view the [DebugMenuSubsystem::CreateMenu docs here](DebugMenuSubsystem.md#creating-a-menu).

## Overview of properties available

<table column-width="fixed">
    <tr>
        <td>Name</td>
        <td width="40">C++?</td>
        <td width="40">BP?</td>
        <td>Info</td>
    </tr>
    <tr>
        <td><code>ULocalPlayer* LocalPlayer</code></td>
        <td>✅</td>
        <td>✅</td>
        <td>This is the title displayed on any of the UI.</td>
    </tr>
    <tr>
        <td><code>TSharedPtr&lt;SDebugWindow&gt; Window</code></td>
        <td>✅</td>
        <td>❌</td>
        <td>A reference to the underlying DebugWindow instance, once it's been created</td>
    </tr>
    <tr>
        <td><code>TSharedPtr&lt;SDebugMenu&gt; Menu</code></td>
        <td>✅</td>
        <td>❌</td>
        <td>A reference to the underlying DebugMenu instance, once it's been created</td>
    </tr>
    <tr>
        <td><code>FName Id</code></td>
        <td>✅</td>
        <td>✅</td>
        <td>The ID assigned to this menu/window during creation</td>
    </tr>
    <tr>
        <td><code>FString Title</code></td>
        <td>✅</td>
        <td>✅</td>
        <td>Title displayed on all UI relating to this menu/window.</td>
    </tr>
    <tr>
        <td><code>USlateWidgetStyleAsset* WindowStyle</code></td>
        <td>✅</td>
        <td>✅</td>
        <td>An optional style override used for the menus window. You can create a new slate widget style asset using <code>DebugWindowStyle</code> as the style type.</td>
    </tr>
    <tr>
        <td><code>USlateWidgetStyleAsset* MenuItemStyle</code></td>
        <td>✅</td>
        <td>✅</td>
        <td>An optional style override used for the menus items. You can create a new slate widget style asset using <code>DebugMenuItemStyle</code> as the style type.</td>
    </tr>
    <tr>
        <td><code>UDebugMenuItem* Root</code></td>
        <td>✅</td>
        <td>✅</td>
        <td>This is basically a hidden root item, any items added to your menu at the top level, will be added to this item.</td>
    </tr>
</table>

## Get Owing Player

<secondary-label ref="cpp"/>
<secondary-label ref="bp"/>

Returns the LocalPlayer that owns this menu.

```C++ 
ULocalPlayer* GetOwningPlayer() const
```

## Get Subsystem

<secondary-label ref="cpp"/>
<secondary-label ref="bp"/>
Quick access to the subsystem using the local player assigned to this menu.

```C++
UDebugMenuSubsystem* GetSubsystem() const
```

## Get Children

<secondary-label ref="cpp"/>
<secondary-label ref="bp"/>
Returns the direct child items of the root item.

```C++
TArray<UDebugMenuItem*> GetChildren() const
```

## Get Root Item

<secondary-label ref="cpp"/>
<secondary-label ref="bp"/>

Returns the root item of the menu.

```C++
UDebugMenuItem* GetRootItem() const
```

## Get Window

<secondary-label ref="cpp"/>
<secondary-label ref="no-bp"/>
Access to the DebugWindow reference(just a proxy to the var)

```C++
TSharedPtr<SDebugWindow> GetWindow() const
```

## Get Menu

<secondary-label ref="cpp"/>
<secondary-label ref="no-bp"/>

Access to the DebugMenu reference(just a proxy to the var)

```C++
TSharedPtr<SDebugMenu> GetMenu() const
```

## On Build Menu

<secondary-label ref="cpp"/>
<secondary-label ref="bp"/>
Allows us to hook into creation process for subclasses, so we can define our items here.

```C++
void OnBuildMenu()
```

## Add To Viewport

<secondary-label ref="cpp"/>
<secondary-label ref="bp"/>

This actually creates our Slate SDebugWindow & SDebugMenu instances, initializes everything and adds it to the viewport.

```C++
void AddToViewport()
```

## Activate

<secondary-label ref="cpp"/>
<secondary-label ref="bp"/>

The same as `AddToViewport` but a better/more applicable name, that goes alongside `Deactivate`.

```C++
void Activate()
```

## Deactivate

<secondary-label ref="cpp"/>
<secondary-label ref="bp"/>

This completely destroys our window/menu instance and removes them from our WindowManager & Viewport.

```C++
void Deactivate()
```

## Collapse

<secondary-label ref="cpp"/>
<secondary-label ref="bp"/>
Basically "minimizes" our window, hiding it from the main viewport
and adding it to our window managers window list.

```C++
bool Collapse()
```

## UnCollapse

<secondary-label ref="cpp"/>
<secondary-label ref="bp"/>
Basically opens our window back up from it's collapsed state.

```C++
bool UnCollapse()
```

## Is Collapsed

<secondary-label ref="cpp"/>
<secondary-label ref="bp"/>
Is it collapsed?

```C++
bool IsCollapsed() const
```
