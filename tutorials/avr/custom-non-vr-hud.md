# Customizing Buttons and Widgets in the Non-VR Pawn HUD in the Advanced VR Framework 3.x

I'm going to break down the how the Non-VR Pawn HUD works in [Advanced VR Framework](https://www.humancodeable.com) (version 3.x) and how to customize it with your own widgets. By the way, if you're looking for how to use widgets with the VR pawn, [here is the official tutorial](https://youtu.be/_Q82fp1nH40).

---

Here is my use case in user story form:

> As a developer </br>
> I want to be able to provide my non-VR users with custom HUD functionality </br>
> So they can have quick access to that functionality </br>

AVR 3.x has a pre-built HUD for non-VR players that comes with some default buttons. If you or pawn is a custom copy of or inherits from `BP_Pawn_Non_VR_Demo` (which I would highly recommend doing), you should see something like this:

### Adding a new HUD menu button type

![Image of non-VR HUD](https://docs.google.com/drawings/d/e/2PACX-1vRtqz-XsWd_aMpjOLBbKZaPpYN8rrMxVDYaGAtk6Oc7hjADxzb4U8oXRMJEprFCO7xfI4z3iDson3dg/pub?w=1392&h=756)
*The default non-VR HUD for a non-VR pawn*

The buttons that you see are defined in the non-vr pawn's `Comp_UI_NonVR` component on its `NonVRHUD` property, which is of type `TArray<Struct_Non_VRHUD>`. If you don't know typed array syntax, `TArray<Struct_Non_VRHUD>` just means a `TArray` (Unreal Engine's custom array class) that only contains `Struct_Non_VRHUD`. The `Struct_Non_VRHUD` contains two properties: `MenuField` of type `Enum_Non_VR_HUD`, which is an enum that contains all HUD menu types; and `QuickAccessKey` of type `Key`, which is used to bind a key to the value in `MenuField`. 

![Image of Comp_UI_NonVR](https://docs.google.com/drawings/d/e/2PACX-1vTJc4iALqVaPCduw8FFa7MGARDtH47rGyVTlrCNmvjireV4liJnzfcubbrbdbba3umhqM1_cX5SNZTV/pub?w=1078&h=609)
*The `Comp_UI_NonVR`'s `Non VRHUD` values on the non-VR pawn.*

`Enum_Non_VR_HUD` is where you can add custom HUD menu types. Lets add a 'Custom Button Type' value.

![Adding a new enum value](https://docs.google.com/drawings/d/e/2PACX-1vQY5RqyRtZ3JeiDvqXtrLetTdd6VMlrxp1frRqKgJV5_yrzedW6hHgdBcH1sekwDkOC2_ZHsMKOEU0V/pub?w=1390&h=917)
*Click 'New', then add the Display Name of your new enum value.*

You can now select your custom value in the `MenuField` drop down under `Non VRHUD` on the `Comp_UI_NonVR` component on your non-vr pawn!
