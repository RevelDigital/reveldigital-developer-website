Revel Digital Player API for Windows
====================================

## Introduction

The Revel Digital Player API provides runtime access to the Revel Digital player software. This capability allows complete freedom to manipulate the signage, while it's playing, to
achieve any level of functionality required.

The player software is built on the [UWP (Universal Windows Platform)](https://docs.microsoft.com/en-us/windows/uwp/) and utilizes a Javascript scripting engine for interpretation of user supplied code.
Scripts are able to leverage the complete UWP Framework.

At the heart of the API is the [`Controller`](https://reveldigital.github.io/ReveDigital.Player.UWP.Doc/api/RevelDigital.Player.RevelScript.IController.html).
The Controller has a reference to the currently active [`Schedule`](https://reveldigital.github.io/ReveDigital.Player.UWP.Doc/api/RevelDigital.Player.RevelScript.Schedule.html) and
[`Template`](https://reveldigital.github.io/ReveDigital.Player.UWP.Doc/api/RevelDigital.Player.RevelScript.Template.html).
Each [`Template`](https://reveldigital.github.io/ReveDigital.Player.UWP.Doc/api/RevelDigital.Player.RevelScript.Template.html) has a list of its Modules which together compose the template content.
Each template [`Module`](https://reveldigital.github.io/ReveDigital.Player.UWP.Doc/api/RevelDigital.Player.RevelScript.Module.html)
has a reference to the actual UWP control responsible for rendering its content.
The UWP control is accessed through the [`IRevelControl`](https://reveldigital.github.io/ReveDigital.Player.UWP.Doc/api/RevelDigital.Player.RevelScript.IRevelControl.html)
interface and has a number of RevelDigital specific methods and properties.
The IRevelControl interface can also be treated as a reference to a UWP [Control](https://docs.microsoft.com/en-us/uwp/api/windows.ui.xaml.controls.control)
for performing any UWP specific operations. Similarily the [`ITemplate`](https://reveldigital.github.io/ReveDigital.Player.UWP.Doc/api/RevelDigital.Player.RevelScript.ITemplate.html)
interface can be treated as a reference to the UWP [Page](https://docs.microsoft.com/en-us/uwp/api/windows.ui.xaml.controls.page).

As a rule, the classes in this API are representative of definitions for the schedules, templates, modules, etc.
That is they should be considered read-only and are purely data bound. Interfaces on the other hand represent the underlying UWP controls.
These objects are normally the focus of any scripting since they provide access to the live template objects and directly affect the template visuals.

### Example script

The following example will fade out an image when a hot spot is clicked. The template looks like this:

![template](/img/script-example-1.png)

The image is named `Static Image 1` and the hot spot is named `Hot Spot 1`.
These names are assigned at template design time and are always accessible from script directly by name.
**Spaces and other special characters in the name are always substituted with an underscore in script**.

To edit the script for this template, click to open the Menu in the template designer, then click RevelScript Editor. Then enter the following script:

```javascript
Hot_Spot_1.add_Tapped(function() {
  Static_Image_1.FadeOut();
});
```

In this example an event handler was added for the [Tapped event](https://docs.microsoft.com/en-us/uwp/api/windows.ui.xaml.uielement#Windows_UI_Xaml_UIElement_Tapped).
This in turn called the [FadeOut](https://reveldigital.github.io/ReveDigital.Player.UWP.Doc/api/RevelDigital.Player.RevelScript.IRevelControl.html#RevelDigital_Player_RevelScript_IRevelControl_FadeOut)
method on the image control.

### Snippets

The script editor has a number of built-in snippets available for some of the more common scripting tasks. Only zones currently added to the template will be available in the snippet dropdown.

![template](/img/script-example-2.png)

These snippets will auto generate the script necessary to perform the function selected.

!!! Note
    Make sure your platform is properly selected at the top/right of the script editor window.


## Technical Reference

Please refer to our technical API website for more details on actual controls, events, and methods available.

**[https://reveldigital.github.io/ReveDigital.Player.UWP.Doc/api/index.html](https://reveldigital.github.io/ReveDigital.Player.UWP.Doc)**