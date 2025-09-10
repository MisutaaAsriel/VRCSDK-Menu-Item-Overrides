# The Menu Item Overrides Community Package for the VRChat
This is an experimental VRChat SDK compatible package for [`Alexejhero/Menu-Item-Overrides`](https://github.com/Alexejhero/Menu-Item-Overrides), a tool by Alexejhero to hide or move menu items in Unity, including those added by other packages

&nbsp;
## Installation

### Via Repository (Recommended)
1. [Add my repo](https://misutaaasriel.github.io/Dreemurrs-Repository/) to the VCC or your VPM utility of choice.
2. Add the `com.5pdev.menu-item-overrides` package to your project, which will include `dev.pardeike.harmony` as a dependency.

### As a User Package (Advanced)
1. Install the latest release of [Harmony for the VRChat SDK](../../../VRCHarmony)
2. Download `com.5pdev.menu-item-overrides-X.X.X.zip` from the [latest release](../../releases/latest)
3. Extract it to a safe location
4. Add this folder as a [User Package](https://vcc.docs.vrchat.com/vpm/packages/#user-packages) to the VCC or your VPM utility of choice

&nbsp;
## Important Notes
> [!WARNING]
> ### Compatibility Changes
> Menu Item Overrides depends on APIs provided by both either [`pardeike/Harmony`](https://github.com/pardeike/Harmony), or [`BepInEx/HarmonyX`](https://github.com/BepInEx/HarmonyX) and its dependencies, to function.
> 
> The original package ships with a copy of [`BepInEx/HarmonyX`](https://github.com/BepInEx/HarmonyX) and its dependencies, *which are **incompatible** with UDON Sharp and the VRChat SDK.* **These have been removed during the [packaging step](#developer-transparency).**

> [!TIP]
> ### Library Upgrades for ARM64 Compatibility
> For users of the ARM64 or Apple Silicon editions of the Unity Editor, the version of Harmony shipped with the VRChat Base SDK is **out of date** and therefor incompatible with your hardware.
>
> As a workaround, this package references [`MisutaaAsriel/VRCHarmony`](../../../VRCHarmony), an updated, VRChat SDK compatible version of Harmony, as a required VPM package dependency, for your *convenience*. It may be disabled at any time by adding `VRC_USE_INCLUDED_HARMONY` to your scripting defines.

> [!NOTE]
> ### Developer Transparency
> The core code and functionality provided by this package remains **unchanged** from the originating project. However, for reasons explained above, embedded dependencies have been removed.
>
> For full honesty, and open transparency, this project does the following via [GitHub Actions](../../actions):
> - Checks out the latest copy of [`Alexejhero/Menu-Item-Overrides`](https://github.com/Alexejhero/Menu-Item-Overrides)
> - Replaces the Package Manifest `package.json` with a VPM compatible version...
>   - ...adding [`dev.pardeike.harmony`](../../../VRCHarmony) as a VPM Package Dependency
>   - ...extending the version number with build information to [reflect VPM package updates](#semantic-versioning)
>   - ...and including relevant developer information
> - Copies the original `LICENSE.txt`, and a specially paired `.meta` file, to the root of the project directory
> - Removes the `Editor/Dependencies` directory from the package, alongside its relevant `.meta` file
> - Packages the files as a [VPM Package](https://vcc.docs.vrchat.com/vpm/packages/#community-packages)
> - Publishes the package to the [releases](../../releases) page

&nbsp;
## Usage

> [!NOTE]
> This section has been predominantly copied from the original project, for your convenience, with only mild alterations for formatting or clarity provided. Please see the original project for up to date information.

Open the Menu Item Overrides configuration pane by navigating to the following from the menu bar:

#### `Tools ➜ Menu Item Overrides ➜ Configuration`

The following window that will appear will allow you to add a list of overrides for menu items, which can modify the path of the menu item, the priority, or both.

![](https://github.com/Alexejhero/Menu-Item-Overrides/raw/main/.github/images/window.png)

- By toggling the `H` button, you can hide a menu item entirely.
- By enabling `Override Path`, you may specify a new location for the menu item.
  - Paths ending in `/` are treated as submenus. This is indicated by the lit up `/*` to the right of the item listing.
- By enabling `Override Priority`, you may specify a new priority for the menu item.
  - `+=` indicates that the specified priority is an offset and will be added to the original
  - `=` indicates that the original priority will be overriden entirely.

> [!WARNING]
> Since submenus don't have their own priority, and instead are ordered based on their children, `+=` is the only priority override method available to them. 

**Overrides are applied top-to-bottom**, meaning that the following two setups are equivalent:

![](https://github.com/Alexejhero/Menu-Item-Overrides/raw/main/.github/images/example-1.png)
![](https://github.com/Alexejhero/Menu-Item-Overrides/raw/main/.github/images/example-2.png)

> [!TIP]
> ### Additional features
> 
> - The `Debug Mode` toggle will append the priorities of each item to the end of their path, so you can better see how to modify them.
>   - This is not present in any of the above screenshots because they were taken before this feature was added.
> - `Tools ➜ Menu Item Overrides ➜ See Report...` allows you to see a list of all of the menu items and their priorities _before_ they were modified by this package.

> [!WARNING]
> ### Limitations
> 
> - A **restart** of the Unity Editor is **required if this package is *uninstalled*** to return menu items to their original state.
> - Submenus may at times be cached by the Unity Editor. **This has the following caveats:**
>   - Changing the priority of an entire submenu will only take effect if the editor is restarted **or** if the submenu is moved, or hidden and unhidden.
>   - Removing an entire submenu and replacing it with a single item will make the editor behave weirdly, if you really want to do that you can include a ZWSP at the end of the name for the single item

&nbsp;
## Additional Notes
> [!NOTE]
> ### Semantic Versioning
> The versioning scheme, `1.2.3+4.5`, for the VPM package is as follows:
> 1. Menu Item Overrides Major Number
> 2. Menu Item Overrides Minor Number
> 3. Menu Item Overrides Build Number
> 4. Project Commit Number — *This has been ammended to reflect an earlier version of this package.*
> 5. GitHub Action Run Number
> 
> This is done with the *intent* that the package versions be treated in the following order:
> ```
> Menu Item Overrides Major Update
>   Menu Item Overrides Minor Update
>     New Menu Item Overrides Build
>       Change to the VPM package or repository
>         New VPM package build available
> ```
> This way, new builds of Menu Item Overrides always take precedence, and are reflected in the package version. Following that, changes to the repository, such as changes to the package layout or metadata, will increment the version number, and lastly, a new build of the package regardless of changes will also increment the counter on the end.
> 
> Thus, hopefully, versions maintain order within the VCC and other VPM utilities.
