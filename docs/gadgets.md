Revel Digital Gadgets
=====================

#Introduction

Gadgets are a simple means of providing customizable, dynamic content to any template. The Revel Digital platform includes a number of ready-to-use
gadgets for everything from weather conditions to social media feeds. Creating your own gadget is simple if you have some basic understanding of HTML
and Javascript.

![template](/img/gadget-example.png)

#What's in a gadget

A gadget is nothing more than an XML file which defines the properties of the gadget along with the HTML and Javascript for rendering the gadget content.

Here's a template for a sample gadget:

```xml
<?xml version="1.0" encoding="UTF-8" ?> 
<Module> 
<ModulePrefs title="Sample Gadget" description="" author="" background="transparent">
  <UserPref name="myStringPref" display_name="Example string preference" datatype="string" default_value="Hello World!" required="true" />
  <UserPref name="myEnumPref" display_name="Example enum preferences" datatype="enum" default_value="first">
    <EnumValue value="first" display_value="First" />
    <EnumValue value="second" display_value="Second" />
  </UserPref>
  <UserPref name="myStylePref" display_name="Example style preferences" datatype="style" default_value="font-family:Verdana;color:rgb(255, 255, 255);font-size:24px;text-align:left;" required="true" />
  <UserPref name="myBooleanPref" display_name="Example boolean preference" datatype="bool" default_value="true" />
  <UserPref name="myColorPref" display_name="color" datatype="color" default_value="#ff00ff" />
  
  <!-- The following preferences should not be modified -->
  <UserPref name="ForeColor" datatype="hidden" />
  <UserPref name="BackColor" datatype="hidden" />
  <UserPref name="rdW" display_name="Width" required="true" default_value="280" datatype="hidden" />
  <UserPref name="rdH" display_name="Height" required="true" default_value="190" datatype="hidden" />
  <UserPref name="rdKey" display_name="Device Registration Key" default_value="*|DEVICE.REGISTRATIONKEY|*" datatype="hidden" />
</ModulePrefs>
<Content type="html">
<![CDATA[

<style type="text/css">
  body *
  {
    line-height: 1.2em; 
    letter-spacing: 0; 
    word-spacing: normal;
  }

  body
  {
    background: transparent;
    width: __UP_rdW__px;
    height: __UP_rdH__px;
    overflow: hidden;
  }
  .my-style
  {
    __UP_myStylePref__;
  }
</style>

<!-- Preferences can be inlined in your HTML like so -->
<div class="my-style" id="container">__UP_myStringPref__</div> 

<script type="text/javascript">

  var prefs = new gadgets.Prefs();

  // This function is called after the gadget has been initialized.
  function onLoad() {
    
    <!-- Preferences can be accessed at runtime like so -->
    alert(prefs.getString('myStringPref'));
  }

  gadgets.util.registerOnLoadHandler(onLoad);
  
</script>

]]>
</Content>
</Module>
```

###Module prefs

You'll see in the sample gadget a section for module preferences called `<ModulePrefs>`. It's here that you'll define any customizable properties for your gadget.
A preference is defined with a `<UserPref>` element and can have any of the following data types:

  * `string` for simple string properties
  * `enum` for defining a list of selectable options
  * `bool` for a checkbox type property
  * `style` for defining a number of CSS type styles
  * `hidden` for providing properties to the gadget which are not visible to the template designer
  
These preferences are then available in the gadget content either by direct substitution:

```html
<!-- This will substitute the myStringPref property -->
<div class="my-style" id="container">__UP_myStringPref__</div>
```

or by utilizing the gadget Javascript API method to retrieve a property value:

```javascript
/* Preferences can be accessed at runtime like so */
alert(prefs.getString('myStringPref'));
```

###Module content

The `<Content>` section of the gadget is where your HTML/Javascript is contained. This is the visible portion of the gadget and can contain most any valid HTML markup.
It's recommended to include the following script for initializing the gadget:

```html
<script type="text/javascript">

  var prefs = new gadgets.Prefs();

  // This function is called after the gadget has been initialized.
  function onLoad() {
  }

  gadgets.util.registerOnLoadHandler(onLoad);
  
</script>
```

This ensures the properties will be accessible via the `prefs` object.

###Publishing your gadget

Once you have your gadget XML ready to go, you'll need to make it available to the Revel Digital template editor.
Most any web hosting provider will do, but we recommend [Github](https://pages.github.com/) for it's simplicity.

You can read more on [Github Pages here](https://pages.github.com/). This is a great option for simple hosting.

###Adding your gadget to a template

Now that your gadget is available on the web we can add it to your template.

![template](/img/gadget-1.png)

Add a new **Gadget zone** to your template, and paste the URL to your gadget XML in the Source field. Click the refresh icon to load your gadget properties in the editor.

Now you can preview the template to see your work!

#Yeoman generator

Our Yeoman generator can scaffold a template for you automatically.

First, install [Yeoman](https://yeoman.io) and [generator-reveldigital-gadget](https://github.com/RevelDigital/generator-reveldigital-gadget) using [npm](https://www.npmjs.com/)
(we assume you have pre-installed [node.js](https://nodejs.org/)).

```sh
npm install -g yo
npm install -g generator-reveldigital-gadget
```

Then generate your new gadget:

```sh
yo reveldigital-gadget
```
