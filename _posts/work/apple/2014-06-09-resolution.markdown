---
layout:     post
title:      "分辨率"
subtitle:   " \"resolution, 分辨率\""
date:       2014-06-09 12:00:00
author:     "awd"
header-img: "img/post-bg-2015.jpg"
tags:
    - Apple
---
http://iosdesign.ivomynttinen.com/

The iOS Design Guidelines

Design great-looking apps for Apple iOS devices.
Designing iOS apps can be difficult sometimes, but finding correct and up-to-date information about all of Apples’ devices shouldn’t be. These design guidelines will help any designer who’s building neat things for iOS get started within seconds.
 
700 Icons for iOS and Android Design only $15
ADVERTISEMENT
About these guidelines

These guidelines describe how to design apps that follow the official HIG for iOS by Apple, not what you can do with custom controls. Sometimes it makes sense to break the rules. The purpose of this document is to guide you, not to provide solutions for complex and unique design problems.

This unofficial documentation will be updated and extended regularly. Last update: September 28, 2015.

Resolutions and Display Specifications

Device	Retina	Portrait (px)	Landscape (px)
iPhone 6+
6+, 6S+
Retina HD	1080 x 1920	1920 x1080
iPhone 6
6, 6S
Retina	750 x 1334	1334 x 750
iPhone 5
5, 5S, 5C
Retina	640 x 1136	1136 x 640
iPhone 4
4, 4S
Retina	640 x 960	960 x 640
iPhone
1st, 2nd & 3rd Generation
No	320 x 480	480 x 320
iPad Air / Retina iPad
1st & 2nd Generation / 3rd & 4th
No	1536 x 2048	2048 x 1536
iPad Pro	No	2048 x 2732	2732 x 2048
iPad Mini
2nd & 3rd Generation
Retina	1536 x 2048	2048 x 1536
iPad
Mini, 1st & 2nd Generation
No	768 x 1024	1024 x 768
Difference between Points and Pixels

Pixels are the smallest physical element that we can control on a digital display. The more pixels can be fitted into a specific screen size, the higher the PPI (pixels-per-inch), and the clearer the rendered content becomes.

Points are a resolution-independent measurement. Depending on the screens pixel density, a point can contain multiple pixels (e.g., 1 pt contains 2 x 2 pixels on a regular retina display).

When you are designing for various display types, you should think in points, but design in pixels. This means you will still need to export all your assets in 3 different resolutions, no matter in which resolution you are designing your app.

NOTE

As long as it is not stated otherwise (by appending „px“ to a value), this guide always refers to points when it comes to specific dimensions. If you need the value in pixels, just multiply by 2 for Retina screens or by 3 for Retina HD screens.

Device	Asset Resolution	PPI	Display Size
iPhone 6+
6+, 6S+
@3x	401	5.5″
iPhone 6
6, 6S
@2x	326	4.7″
iPhone 5
5, 5S, 5C
@2x	326	4.0″
iPhone 4
4, 4S
@2x	326	3.5″
iPhone
1st, 2nd & 3rd Generation
@1x	163	3.5″
iPad Pro	@2x	264	12.9″
iPad Air / Retina iPad
1st & 2nd Generation/ 3rd & 4th
@2x	264	9.7″
iPad Mini
2nd & 3rd Generation
@2x	326	7.9″
iPad Mini
1st Generation
@1x	163	7.9″
iPad
1st & 2nd Generation
@1x	132	9.7″
Downsampling on iPhone 6+

Rendered pixels and physical pixels are equal on all iOS devices, with one exception: the Retina HD screen of the iPhone 6 Plus. Because its screen has a lower pixel resolution than what would be a natural @3x resolution, the rendered content is automatically resized to approximately 87% of the original size (from 2208 x 1242 pixels to fit the display resolution of 1920 x 1080 pixels).

Difference between iPhone 5S 6 6+ displays
The difference between displays of iPhone 5S, 6 and 6+. More in-depth information here.
App Icons

Device	App Icon	AppStore Icon	Spotlight	Settings
iPhone 6+
6+, 6S+
180x180 px	1024x1024 px	120x120 px	87x87 px
iPhone
6S, 6, 5S, 5, 5C, 4S, 4
120x120 px	1024x1024 px	80x80 px	58x58 px
Old iPhones
1st, 2nd, 3rd Generation
57x57 px	1024x1024 px	29x29 px	29x29 px
iPad Pro	167x167 px	1024x1024 px	120x120 px	58x58 px
Retina iPads
Mini 2 & 3, Air, 3 & 4
152x152 px	1024x1024 px	80x80 px	58x58 px
Old iPads
1, 2, Mini 1
76x76 px	1024x1024 px	40x40 px	29x29 px
Automatically applied effects

App icons assets are generally added to the application package as plain, squared PNG files in various dimensions. When rendered on a device, iOS applies various effects to app icons.

ROUNDED CORNERS

The old simple radii values for rounded corners are gone. Since iOS 7, app icons have been using the shape of a superellipse. Since Apple did not release an official template of the shape, you will have to use one of the unofficial templates out there that replicate the shape in more or less accurate ways.

iOS 8 app icon radius shape
The rounded corners should not be included in the final exported assets, but you might need them in your design process if you want to add effects, such as a stroke or shadows, that are aligned to the corner of the icon.

WARNING

If you are masking your icon asset with the superellipse shape because you want to apply effects aligned to the corners, make sure not to use any transparency for the area outside the mask. Transparency is not supported at all for app icons and instead is rendered as plain black. If your mask is not 100% accurate, users will see small black fragments on the rounded edges. It’s recommend to set the background of the canvas to be the same as the app icon background.

BORDER STROKE (IN SOME SITUATIONS)

If the app icon you are using has a white background, a 1 pixel gray border stroke will be applied to make it easier to recognize the edges of the icon. This is only done in the settings app (if your application is listed there) and the AppStore.

LEGACY EFFECTS (IOS 6 AND PREVIOUS VERSIONS)

On older iOS versions, these effects are applied automatically: rounded corners (not the same shape as iOS 7+ icons are using), drop shadows on the home screen and a gloss effect that can be disabled.

Grid system

iOS 8 app icon grid system
Apple developed a golden ratio grid system that can be used to size and align elements on your icon correctly. Nevertheless, even Apple designers are not following the grid system very strictly with the native apps’ icons. Feel free to break the rules if your icon simply works better without aligning all elements strictly to the grid.

Typography

The default system font on all iOS versions previous iOS 9 is Helvetica Neue. With the release of iOS 9, Apple introduced a brand new font called San Francisco, which replaced Helvetica Neue as the default font. San Francisco comes in two shapes: „SF UI Display“ and „SF UI Text“, while „Display“ is primarly used for UI components, „Text“ features a wider letter spacing and should be used for longer texts. You can download the San Francisco fonts here if you are a member of Apple’s Developer program. In addition to the default font, many alternative font faces are available to use. You can find a complete list of pre-installed typefaces here.

Font Sizes

Element	Size (pt)	Weight	Spacing (pt)	Type
Nav Bar Title	17	Medium	0.5	Display
Nav Bar Button	17	Regular	0.5	Display
Search Bar	13.5	Regular	0	Text
Tab Bar Button	10	Regular	0.1	Text
Table Header	12.5	Regular	0.25	Text
Table Row	16.5	Regular	0	Text
Table Row Subline	12	Regular	0	Text
Table Footer	12.5	Regular	0.2	Text
Action Sheets	20	Regular / Medium	0.5	Display
Custom Fonts

Technically, any True Type Font (.ttf) can be used within an iOS app, but be careful about licenses. It should be safe to use fonts that are completely free for commercial usage. App licenses for commercial fonts are rarely available, and if they are, securing them can turn out to be somewhat expensive. MyFonts currently offers the biggest collection of fonts that can be licensed for mobile app usage.

Color Palette

iOS 8 default colors
Since iOS 7, Apple has been using a vibrant color palette for the interface of the OS and pre-installed apps. While you can use the default iOS color palette listed above, you can also (and probably should, if you want to stand out) use your own colors.

Iconography

In iOS apps, icons have always been a great way to support text labels with a visual relationship to the performed action or to replace text completely (often for very common actions such as „New“, „Delete“, etc.). Usually, we are dealing with icons that are part of the Navigation Bar, Tool Bar or Tab Bar.

Bar Button Icons

Icons used in bars should always have two different states: the default state in outlined style with a stroke width of 1 or 1.5pt and the active state with a solid color fill.

iOS button bar outline and solid icons
You should never include any additional effects such as a drop-shadow or inner shadows on button icons because these are relicts from previous iOS versions (before the iOS 7 redesign). Button icons should be drawn in one solid color on a transparent background—the shape of the icon is used as a mask, and the color will be applied programmatically.

Activity View Icons

Icons in the Activity View (also known as Share Popover) used to be designed in outline style, but since iOS 8, Apple has reverted back to solid fill icons on a plain white background.

iOS activity sheet icons
Commonly used design elements

iOS offers a great collection of ready-to-use views and controls that allow app developers to quickly build interfaces. Some elements can be customized to a certain level, but other cannot and probably also should not be. When designing an application for iOS, you should know your set of tools and stick to them whenever possible. However, in some cases, it might be worthwhile to build a custom control because you need a more custom look or want to change the functionality of an already existing control (danger zone). Almost anything is possible,and sometimes it makes sense to break the rules, but always think twice before doing so.

Status Bar

The Status Bar contains basic system information such as the current carrier, time, battery status and more. It’s visually connected to the Navigation Bar and makes use of the same background fill. To match the style of your app and guarantee readability, the content of the status bar comes in two different styles: dark (black) and light (white).

iOS Status Bar 
It is possible to hide the Status Bar, but think twice before doing so. For example, users might be interested in knowing if they are connected to a WiFi network when the app regularly downloads web content or if Bluetooth is enabled when the app requires a Bluetooth link to third-party hardware. A valid reason to hide the Status Bar is when you want to remove all distractions from a single element, for example, when displaying full screen content such as an image gallery.

Navigation Bar

The navigation bar contains the controls for navigating through the applications views and optionally to manage the content of the current view. It will always appear at the top of the screen, right below the status bar. By default, the background is slightly translucent and blurs content underneath the bar. The background fill of the bar can be set to a solid color, a gradient or a custom bitmap-pattern.

iOS Navigation Bar 
Navigation Bar on iPhone 6 in portrait mode.
iOS Navigation Bar Landscape 
Navigation Bar on iPhone 4S in landscape mode. The height of the bar is reduced by 12pt, except on iPads. It's also a common practice to hide the status bar in landscape mode.
The elements should always following a specific alignment pattern.

Back button should always be aligned to the left side.
Title of the current view should always be centered in the bar.
Action buttons should always be aligned to the right side. If possible, there should never be more than one primary action to avoid missed clicks and to maintain simplicity.
Toolbar

A toolbar contains a set of actions for managing or manipulating the content of the current view. On the iPhone, it will always appear aligned at the bottom edge of the screen, while on the iPad, it can also be displayed aligned at the top of the screen.

Similarly to the navigation bar, the background fill of toolbars can be modified, is translucent and blurs the underlaying content by default.

iOS Toolbar 
Toolbars should be used when a specific view requires more than three primary actions that would hardly fit or would look messy in the navigation bar.

Search Bar

Search bars come in two different styles by default: prominent and minimal. Both versions do have the same functionality.

As long as no text was entered by the user, a placeholder text is shown inside the bar, and, optionally, a bookmarks icon that can be used to access recent or saved searches.
Once a search term is entered, the placeholder disappears, and a clear button to delete the entered value appears on the right edge.
Search bars can make use of a prompt — a short sentence to introduce the functionality in the context of the search. For example, „Enter a city, zip code or airport.“

iOS prominent search bar 
Prominent search bar style, without and with a prompt.
iOS minimal search bar 
Minimal search bar style.
To provide even more control over a search query, it is possible to chain the search Bar with a scope bar. The scope bar will use the same style as the search bar and might be useful when there are clearly defined categories for the search results. For example, in a music app, the search results could be filtered again by interpreters, albums or songs.

Tab Bar

The tab bar is used to allow the user to quickly navigate through the separate views of an application, and it should only be used for this purpose. It always appears at the bottom edge of the screen. By default, its slightly translucent and uses the same system blur for underlaying content as the navigation bar.

iOS Tab Bar 
A tab bar can only contain a fixed maximum number of tabs. Once there are more tabs than the maximum count, the last tab displayed will be replaced by a „More-tab“ that will lead to a list of hidden tabs, with an option to re-order the displayed tabs.

While the maximum amount of tabs displayed is five on iPhones, it’s possible to display up to seven tabs on the iPad while avoiding a more-tab.

To notify users about new information on a view, it sometimes makes sense to apply a badge count to a tab bar button. If a view is temporarily disabled, the related tab button should not be completely hidden; instead, it should be faded out to visually communicate the disabled state.

Table View

Table views are used to display small to large amounts of list style information in a single or multiple columns and with the option to divide several rows into separate sections or to group them.

There are two basic table view types that should be used, depending on the type of data you are presenting.

PLAIN

iOS plain table view 
A plain table contains a number of rows that can have a header on the top and a footer after the last row. It’s possible to display a vertical navigation on the right edge of the screen to navigate through the table, which makes sense when presenting a big data set that could be sorted in some way (e.g., alphabetically descending).

GROUPED

iOS grouped table view
A grouped table allows you to organize rows in groups. Each group can have a header (best used to describe the context for the group) as well as a footer (good for help text, etc.). A grouped table needs to contain at least one group, and each group needs to contain at least one row.

For both table view types, a few styles are available to present the data in a way that allows users to easily scan, read and probably modify it.

DEFAULT

iOS default table view 
A table row in default style has an optional image aligned on the left and a title.

WITH SUBTITLE

iOS subtitle table view
The subtitle table style enables a small subtitle text underneath the row title. It is useful for further explanations or short descriptions.

WITH VALUE

iOS subtitle table view
The value table style allows you to display a specific value that is related to the row title. Similar to the default style, each row can have an image and a title that are both aligned to the left. The title is followed by the right aligned label for the value, which is usually displayed in a slightly more subtle text color than the title.

Modals, Popovers and Alerts

iOS provides various styles of temporary views that can be used to display, edit and manipulate data in a way that fits best in a given situation. While each temporary view exists for a very specific purpose and each one looks different, all temporary views still have one thing in common: When displayed, it’s the highest index layer on the current view (they appear on top of everything else), and content underneath is overlayed by a translucent black background.

ACTIVITY VIEW

An activity view is used to perform specific tasks. These tasks can be default system tasks such as share content via the available options, or they can be completely custom actions. When designing icons for custom task buttons, you should follow the same guidelines as for the active state of bar button icons — solid fill, no effects, on a transparent background.

iOS activity sheet view
ACTIONS

Action Sheets are used to perform one single action from a list of available actions and to force the user of an app to confirm an action or cancel it.

iOS action sheet view 
In portrait mode (and on small landscape screen resolutions), actions are always displayed as a list of buttons sliding in and staying at the bottom edge of the screen. In this case, an action sheet should always have a cancel button to close the view and not perform any of the listed actions.

When there is enough space available (e.g., on iPad screens), action sheets visually transform into popovers. A button to close the view is not required anymore because tapping a target anywhere outside the popover will close it automatically.

ALERTS

The purpose of alerts is to inform the user about critical information and optionally to force the user to make a decision about some action.

An alert view does always contain a title text, which should not be longer than one line and one (for pure informational alerts, e.g., „OK“) or two (for alerts that require a decision, e.g., „Send“ and „Cancel“) buttons.

iOS Alerts 
Also, you can add a message text, if needed, as well as up to two text input fields, one of which can be a masked input field, which is appropriate for sensitive information like passwords or PINs.

EDIT MENU

iOS minimal search bar 
The Edit Menu allows users to perform actions such as Copy, Paste, Cut, etc., when an element is selected (text, images, others). While it is possible to control which operations the user can choose from, the visual appearance of edit menus is set and not configurable unless you build your own completely custom edit menu.

POPOVER

Popovers are useful when a specific action requires multiple user inputs before proceeding. A good example is adding an item, which has a few attributes that need to be set before the item can be created.

In a horizontal environment, popovers reveal underneath the related control (such as a button) with an arrow pointing to that control while opened. The background of a popover uses a slightly reduced opacity and blurs the content underneath, just as many other UI elements have done since iOS 7.

iOS popover view 
A popover is a powerful temporary view that can contain various objects such as its own navigation bar, table views, maps or web views. When a popover grows in size due to the number of contained elements and reaches the bottom edge of the viewport, it is possible to scroll within the popover.

MODALS

Modals are a useful view for tasks that require multiple commands or inputs by the user. They appear on top of everything else, and, while open, block interaction with any other interactive elements underneath.

The typical modal usually provides:

a title to describe the task;
a button to close the modal without saving or performing any other actions;
a button to save or submit any entered information; and
various elements for user input in the modal body.
There are three different modal styles available:

Full screen: covers the entire screen.
Page sheet: In portrait mode, the modal covers the underlaying content only partially, leaving a small portion of the parent view visible underneath the translucent black background. In landscape mode, the page sheet modal acts just like a full screen modal.
Form sheet: In portrait mode, the modal appears in the center of the screen, keeping the surrounding content of the parent view visible underneath the translucent black background. The position of the modal adjusts automatically when a keyboard needs to be displayed. In landscape mode, the page sheet modal acts just like a full screen modal.
Controls

iOS provides a wide range of controls for basically any required input type you can think of. Listed below you will find the most important (commonly used), but for a full list of the available controls, you should look at the iOS Developer Library.

BUTTONS

Probably the most used control overall is the good old button. Since iOS 7, the default button design hasn't really looked like a button anymore, but rather more like a plain text link. The button control is highly customizable and allows you to style everything from text style, drop shadows and color to an icon that is either prepended or centered if there is no text label, as well as fully custom backgrounds.

Keep in mind that a button can have several states, which should be communicated with visual language: default, highlighted, selected and disabled.

PICKERS

Pickers are used to select one value from a list of available values. The web equivalent would be a select box (which the picker control is also used for when touching a select in Safari). An extended version of picker is the datepicker, which allows the user to scroll through a list of dates and times and select values for (configurable) day, month and time.

iOS picker controls
Left: datepicker displayed inside a table view, right: picker as keyboard.
Except for the background color, it is not possible to change the visual style or size (same as keyboard) of a picker control. Most often, they appear at the bottom of the screens, where keyboards appear as well, but it is possible to use them in other positions.

SEGMENT CONTROLS

A segment control contains a set of segments (at least two) that can be used for things like filtering content or to create tabs for clearly categorized content types.

iOS segment controls 
Segment control without and with icons.
Each segment can contain a text label or an image (icon), but never both. In addition, using a mixed set of segment types (text and images) in one segment control is not really recommended. The width of one segment changes automatically based on the number of segments (two segments: 50% of total control width, 5 segments: 20% of total control width).

SLIDERS

The slider control allows the user to choose one specific value from a range of allowed values. Since choosing a value works pretty smoothly and without any steps, sliders are recommended for selecting an estimated, but not exact, value. For example, a slider would be a good control for setting the sound volume, since the user can hear the difference and can see the difference between loud and very loud, but a text input to set an exact dB value would be impractical.

iOS slider controls 
Slider control without and with descriptive icons.
It is possible to set icons for the minimum and the maximum value, which are displayed on the start and end edge of the slider control, thereby allowing you to visually embrace the purpose of the slider.

STEPPER

Steppers should be used when the user should enter an exact value from a limited range of possible values (e.g., 1-10). A stepper always contains two segmented buttons, one for lowering and one for raising the current value.

iOS stepper controls 
Visually, the stepper control is highly customizable:

you can use your own icons for stepper buttons;
when maintaining the native iOS look, you can customize the color of borders, background and icons by using a tint color, which automatically sets the color for each of these elements; and
if you want to go further, you can use completely custom background images for the stepper buttons as well as for the separator.
SWITCH

iOS switch controls 
A switch allows the user to quickly toggle between two possible states: on and off. It’s the checkbox for iOS apps. It is possible to customize the color for the on and off states, but the appearance of the toggle button and size of the switch are set and cannot be changed.

KEYBOARDS

There are various keyboard types available to provide the best possible keyboard for a specific text input. While it is possible to build your own completely custom keyboard, default keyboards cannot be customized in style or size.

Further Reading and Resources

These guidelines only provide basic information to get you started with iOS design. Once you dig deeper, you might be interested in more details. These articles and resources should help you.

GENERAL

iOS Human Interface Guidelines
by Apple
UIKit User Interface Catalog
by Apple
My app design workflow
by Marc Edwards
Learn Mobile App Design
on Treehouse
ANIMATIONS & PROTOTYPING

Principle
$99, highly recommended!
Framer.js
$79.99, trial available
Marvel
Free Prototyping for Everyone
Pixate
Prototype iOS animations
How To Prototype In Xcode Using Storyboard
by Meng To
DEVELOPMENT STARTER GUIDES

Building iOS Apps From Scratch
by Mike Rundle
Cocoa Controls
Open Source, Commercial