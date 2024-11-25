# How do I use it?(TLDR version)

## (Optional) Subclass debug menu

**Note: Subclassing debug menu is optional** But this would allow you to add custom styles

![HowDoI_CreateBP.png](HowDoI_CreateBP.png)

![HowDoI_PickParentClass.png](HowDoI_PickParentClass.png)

## Create menu

Somewhere in your project, create a new menu and call activate on it.

![HowDoI_CreateMenu.png](HowDoI_CreateMenu.png)

You can create a menu from almost anywhere, and activate it at a later point, this could be via an input action or something. We don't control this "toggle" logic on menus, because thats your choice :)

## Adding items

### Subclass Method:

Hook into the `OnBuildMenu` method

![HowDoI_OnBuild.png](HowDoI_OnBuild.png)

**Debug menu to your hearts content**

![HowDoI_BeginBuildingOnBuild.png](HowDoI_BeginBuildingOnBuild.png)

### Non-subclass method:

You can add items and such from anywhere, as long as you have a reference to the menu.

![HowDoI_BeginBuilding_NonSC.png](HowDoI_BeginBuilding_NonSC.png)