# BCUI Tracking Menu

**Tracking Menu** - Replaces the tracking icon on the minimap with an icon that has a popup menu that allows you to choose which tracking ability to activate. The menu is displayed when you mouse over the icon and is hidden when your mouse is no longer over the icon or the menu. The list of abilities in the menu is automatically populated\* with the tracking abilities available to your character, and should update when you acquire new tracking abilities.

## Usage

* `/bctm_report`
    * Returns all of the localized strings used by the mod. Mainly for debugging purposes.
* `/bctm_showmenu`
    * Shows the tracking menu centered under the cursor.
* `/bctm_hidemenu`
    * Hides the tracking menu.
* `/bctm_getloc`
    * Prints out the current location of the cursor on the screen. This is meant to be used along with `bcTM_ShowMenu()` function.
* `/bctm_showoptions`
    * Shows the option window.
* `/bctm_hideoptions`
    * Hides the option window.
* `/script bcTM_ShowMenu(x, y, anchor);`
    * Shows the tracking menu at the specified location, using the specified anchor point. Valid anchor points are: `topright`, `topleft`, `bottomright`, `bottomleft`, `center` (default).
    * Example: `/script bcTM_ShowMenu(400, 300, 'topright');`
* `/bctm_tracktarget`
    * Casts the tracking ability corresponding to the target's creature type (if available).
    * Sample macro for Hunters:
        ```lua
        /bctm_tracktarget
        /cast Hunter’s Mark
        ```
         \- if the target is not tracked, casts the appropriate tracking ability
         
         \- if the target is already tracked, casts Hunter's Mark

## Credits

* Thanks to Malecandra for helping come up with this idea in the first place.
* Big thanks to Jet for localizing all of the strings to French and doing most (if not all) of the code changes to hook that up.
* The `bcTM_pairsByKeys()` function was taken from the LUA reference available at [http://www.lua.org/pil/19.3.html](http://www.lua.org/pil/19.3.html).
* Thanks to Markus for localizing the strings to German and clueing me in to the escape codes for the different characters.
* The idea for the positioning slider came from a discussion with Malecandra about how Cosmos allows the user to reposition its side bars.
* Thanks to Astus for laying the ground work for the "blink while inactive" and "hide while dead" functionality.
* Ttang Oul - added tracking target's type.

## Revision History

### 2025-02-07 v1.41

* Added a check for tracking the target so the same tracking ability isn't cast multiple times.

### 2025-02-05 v1.40

* Added a command to track the target's creature type.
* Updated localization strings.

### 2005-08-03 v1.39

* Modified the way the mod was saving its variables. Using a single table now to make things easier to deal with.
* Added key bindings for the individual abilities. Just go to the regular Key Bindings window. They'll show up under the BCUI Tracking Menu section.
* New interface number.
* Updated localization strings.
* Updated `ReadMe.html`.

### 2005-06-20 v1.34

* Updated localization strings.
* New interface number.

### 2005-04-05 v1.32

* Tweaked French localization. (Thanks Islorgris)
* Tweaked German localization. (Thanks Alexspeed)

### 2005-03-30 v1.30

* Slight change to make the Tracking Menu hide the Aspect Menu if necessary.
* Updated German localization. (Thanks Ghandi)

### 2005-03-29 v1.28

* Modified `bcTM_ShowMenu()`. It now takes parameters for the location and anchor point to show the menu:
    * Macro example: `/script bcTM_ShowMenu(x, y, 'anchor');`
    * `x, y` = location returned from `/bctm_getloc`
    * `anchor` = the point of the menu to set at the given location. Possible values: `topright`, `topleft`, `bottomright`, `bottomleft`, `center` (default)
* Added `/bctm_getloc`. It prints out the current location of the cursor on the screen. This is meant to be used along with `/bctm_showmenu`.
* Fixed the issue with the `frameStrata` being too high for the icon. It should no longer overlap bag contents when they're open.
* Added the functionality to allow the icon to blink if there is no tracking ability currently active. (Credit due to Astus for the idea and groundwork)
* Added the functionality to allow the icon to hide while the player is dead. (Credit due to Astus for the idea and groundwork)
* New interface number.
* Various other code tweaks.

### 2005-02-18 v1.21

* Found that I wasn't using the localized tooltip text. Doh! Fixed.
* Added a UI configuration panel with various options for showing/hiding the menu as well as a slider you can use to set the position of the icon around the border of the minimap. To open the options panel, open the menu, then click on Options at the top.
    * Show/Hide on mouse over/out.
    * Show/Hide on left clicking the icon.
    * Show/Hide on button press. Requires you to bind a key through the default keybindings interface to activate.
    * Hide on spell cast. Hides the menu when you click on a button to activate a tracking ability.
* Added the following slash commands:
    * `/bctm_showmenu` - Shows the menu centered under the mouse.
    * `/bctm_hidemenu` - Hides the menu.
    * `/bctm_showoptions` - Shows the configuration options panel.
    * `/bctm_hideoptions` - Hides the configuration options panel.
* Modified the `/bctm_report` command to return all localized strings, not just the ones being looked for in the spell book.
* Added a keybinding that allows you to bind a key that, when pressed, will show the popup menu centered under the mouse if it's not currently visible, and hide it if it is. Note that the "Show on button press" and/or "Hide on button press" options must be checked in the configuration panel for this to work.
* Was made aware of a bug that the menu would still list a tracking ability that you had unlearned during the current play session. Added code to reset the available abilities when the menu was re-initialized.
* Noticed that the size of the menu was a bit off when the list got longer. Tweaked a few values to try to keep it consistent.

### 2005-02-01 v1.14

* Added German localization strings.
* Tweaked the French localization strings.
* Added version numbers.
* Added the `/bctm_report` command to list out the current values being searched for in the spellbook. Mainly a debugging tool.

### 2005-01-23 v1.10

* I think I've fixed a display problem that I introduced with the "don't show the icon when you don't have any tracking abilities" code. Please let me know if you run into any other oddities while using the mod.

### 2005-01-15 v1.09

* Displayed strings are now localized to English and French. If anyone out there wishes to translate them into another language, just send me the text and I'll get it hooked up.
* The list of abilities on the menu is now sorted alphabetically. If other sorting/grouping options are desired, let me know and I'll see what I can do.
* The icon in the minimap cluster will no longer show if no tracking abilities are available to the current character.
* Fixed a nil reference if the `MiniMapTrackingFrame` was hidden for some reason, as well as a few other minor code changes and optimizations.
* Added Sense Demons to the list of abilities to check for.

### 2005-01-07 v1.04

* Fix: The tracking menu should no longer crash the game client when right-clicked when no tracking abilities were active. Evidently, calling `CancelTrackingBuff()` with no active tracking ability causes problems. Thanks go out to Brent and Amberly for helping track this down.
* Added more verbose comments throughout the code.

### 2004-12-XX v1.0