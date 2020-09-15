# Customizing Buttons and Widgets in the Non-VR Pawn HUD in the Advanced VR Framework 3.x

I'm going to break down the how the Non-VR Pawn HUD works in [Advanced VR Framework](https://www.humancodeable.com) (version 3.x) and how to customize it with your own widgets. By the way, if you're looking for how to use widgets with the VR pawn, [here is the official tutorial](https://youtu.be/_Q82fp1nH40).

---

Here is my use case in user story form:

> As a developer </br>
> I want to be able to provide my non-VR users with custom HUD functionality </br>
> So they can have quick access to that functionality </br>

AVR 3.x has a pre-built HUD for non-VR players that comes with some default buttons. If you or pawn is a custom copy of or inherits from `BP_Pawn_Non_VR_Demo` (which I would highly recommend doing), you should see something like this:

#### Assumptions
- Everything is set up properly in your level to use non-vr functionality. If this isn't the case, check out [this tutorial on Non-VR Pawn setup.](https://youtu.be/nRG7u22dO8s)

### Adding a New HUD Menu Button Type

![Image of non-VR HUD](https://docs.google.com/drawings/d/e/2PACX-1vRtqz-XsWd_aMpjOLBbKZaPpYN8rrMxVDYaGAtk6Oc7hjADxzb4U8oXRMJEprFCO7xfI4z3iDson3dg/pub?w=1392&h=756)
*The default non-VR HUD for a non-VR pawn*

### Comp_UI_NonVR, Struct_Non_VRHUD, and Enum_Non_VR_HD

The buttons that you see are defined in the non-vr pawn's `Comp_UI_NonVR` component on its `NonVRHUD` property, which is of type `TArray<Struct_Non_VRHUD>`. If you don't know typed array syntax, `TArray<Struct_Non_VRHUD>` just means a `TArray` (Unreal Engine's custom array class) that only contains `Struct_Non_VRHUD`. The `Struct_Non_VRHUD` contains two properties: `MenuField` of type `Enum_Non_VR_HUD`, which is an enum that contains all HUD menu types; and `QuickAccessKey` of type `Key`, which is used to bind a key to the value in `MenuField`. 

![Image of Comp_UI_NonVR](https://docs.google.com/drawings/d/e/2PACX-1vTJc4iALqVaPCduw8FFa7MGARDtH47rGyVTlrCNmvjireV4liJnzfcubbrbdbba3umhqM1_cX5SNZTV/pub?w=1078&h=609)
*The `Comp_UI_NonVR`'s `Non VRHUD` values on the non-VR pawn.*

`Enum_Non_VR_HUD` is where you can add custom HUD menu types. Lets add a 'Custom Button Type' value.

![Adding a new enum value](https://docs.google.com/drawings/d/e/2PACX-1vQY5RqyRtZ3JeiDvqXtrLetTdd6VMlrxp1frRqKgJV5_yrzedW6hHgdBcH1sekwDkOC2_ZHsMKOEU0V/pub?w=1390&h=917)
*Click 'New', then add the Display Name of your new enum value.*

You can now select your custom value in the `MenuField` drop down under `Non VRHUD` on the `Comp_UI_NonVR` component on your non-vr pawn! Do that to an existing entry in `Non VRHUD` or create a new entry and set the value on that.

### Displaying a Custom Widget for Your Button

Clicking on your button in game probably doesn't do anything, so lets change that. 

#### Widget_Initial_NonVR_Hud

The widget class that controls what gets displayed when you click a hud menu buton is `Widget_Initial_NonVR_Hud`. In the `Set_Window` event's flow, you should see a `Select` method that displays all of the `Enum_Non_VR_HUD` values along with the corresponding widget they should display. Since this isn't a tutorial about Widget building, we're going to just use a pre-built widget that comes with AVR to show how this works. Lets use `Widget_NonVR_Objects`. Set that as the class under your custom enum, compile, run the game, and click your button. 

#### Allocate_HUDPosition

![Showing the custom widget](https://docs.google.com/drawings/d/e/2PACX-1vRSRZos6RY1OMqkfLssS841aCxQVHlyF5Uyt_Bm0j9hg1WjEndgg4QGNuFIK0jEBslazanixnpGbkKq/pub?w=1392&h=806)
*Once you click your custom menu button, you should see the widget pop up on the left.*

Clicking on your button should display the Object widget on the left side of the screen. You can control where the HUD shows up by assigning a value to your custom `Enum_Non_VRHUD` value in the `Allocate_HUDPosition` macro in the ` Widget_Initial_NonVR_Hud`. 

### THE END
