*   [Recent changes](#recent-changes)
    *   [November 17, 2024](#november-17-2024)
    *   [September 6, 2024](#september-6-2024)
    *   [July 31, 2024](#july-31-2024)
    *   [July 7, 2024](#july-7-2024)
    *   [July 1, 2024](#july-1-2024)
    *   [March 31, 2024](#march-31-2024)
    *   [December 29, 2023](#december-29-2023)
    *   [September 22, 2023](#september-22-2023)
    *   [April 21, 2023](#april-21-2023)
    *   [December 30, 2022](#december-30-2022)
    *   [August 12, 2022](#august-12-2022)
    *   [June 20, 2022](#june-20-2022)
*   [Designing Mini Apps](#designing-mini-apps)
    *   [Color Schemes](#color-schemes)
    *   [Design Guidelines](#design-guidelines)
*   [Implementing Mini Apps](#implementing-mini-apps "Implementing Mini Apps")
    *   [Keyboard Button Mini Apps](#keyboard-button-mini-apps)
    *   [Inline Button Mini Apps](#inline-button-mini-apps)
    *   [Launching Mini Apps from the Menu Button](#launching-mini-apps-from-the-menu-button "Launching Mini Apps from the Menu Button")
    *   [Launching the main Mini App](#launching-the-main-mini-app)
    *   [Inline Mode Mini Apps](#inline-mode-mini-apps)
    *   [Direct Link Mini Apps](#direct-link-mini-apps)
    *   [Launching Mini Apps from the Attachment Menu](#launching-mini-apps-from-the-attachment-menu)
*   [Initializing Mini Apps](#initializing-mini-apps)
    *   [ThemeParams](#themeparams)
    *   [StoryShareParams](#storyshareparams)
    *   [StoryWidgetLink](#storywidgetlink)
    *   [ScanQrPopupParams](#scanqrpopupparams)
    *   [PopupParams](#popupparams)
    *   [PopupButton](#popupbutton)
    *   [EmojiStatusParams](#emojistatusparams)
    *   [DownloadFileParams](#downloadfileparams)
    *   [SafeAreaInset](#safeareainset)
    *   [ContentSafeAreaInset](#contentsafeareainset)
    *   [BackButton](#backbutton)
    *   [BottomButton](#bottombutton)
    *   [SettingsButton](#settingsbutton)
    *   [HapticFeedback](#hapticfeedback)
    *   [CloudStorage](#cloudstorage)
    *   [BiometricManager](#biometricmanager)
    *   [BiometricRequestAccessParams](#biometricrequestaccessparams)
    *   [BiometricAuthenticateParams](#biometricauthenticateparams)
    *   [Accelerometer](#accelerometer)
    *   [AccelerometerStartParams](#accelerometerstartparams)
    *   [DeviceOrientation](#deviceorientation)
    *   [DeviceOrientationStartParams](#deviceorientationstartparams)
    *   [Gyroscope](#gyroscope)
    *   [GyroscopeStartParams](#gyroscopestartparams)
    *   [LocationManager](#locationmanager)
    *   [LocationData](#locationdata)
    *   [WebAppInitData](#webappinitdata)
    *   [WebAppUser](#webappuser)
    *   [WebAppChat](#webappchat)
    *   [Validating data received via the Mini App](#validating-data-received-via-the-mini-app)
    *   [Validating data for Third-Party Use](#validating-data-for-third-party-use)
    *   [Events Available for Mini Apps](#events-available-for-mini-apps)
    *   [Adding Bots to the Attachment Menu](#adding-bots-to-the-attachment-menu)
    *   [Additional Data in User-Agent](#additional-data-in-user-agent)
*   [Testing Mini Apps](#testing-mini-apps)
    *   [Using bots in the test environment](#using-bots-in-the-test-environment)
    *   [Debug Mode for Mini Apps](#debug-mode-for-mini-apps)

*   [Bots](/bots)
*   [Telegram Mini Apps](/bots/webapps)

Telegram Mini Apps
==================

With **Mini Apps** developers can use _JavaScript_ to create **infinitely flexible interfaces** that can be launched right inside Telegram — and can completely replace **any website**.

Like bots, **Mini Apps** support [seamless authorization](https://telegram.org/blog/privacy-discussions-web-bots#meet-seamless-web-bots), payments via third-party [payment providers](/bots/payments) (with _Google Pay_ and _Apple Pay_ out of the box), delivering tailored push notifications to users, and [much more](/bots).

> To see a **Mini App** in action, try our sample [@DurgerKingBot](https://t.me/durgerkingbot).

* * *

### [](#recent-changes)Recent changes

#### [](#november-17-2024)November 17, 2024

**Bot API 8.0**

> This is the **largest update** in the history of Telegram mini apps – adding more than **10 new features** and monetization options for developers. To read more about all these changes, check out this [dedicated blog post](https://telegram.org/blog/fullscreen-miniapps-and-more).

**Full-screen Mode**

*   Mini Apps are now able to [become full-screen](https://telegram.org/blog/fullscreen-miniapps-and-more#full-screen-mode) in both portrait and **landscape mode** – allowing them to host **more games**, play **widescreen media** and support **immersive** user experiences.
*   Added the methods _requestFullscreen_ and _exitFullscreen_ to toggle full-screen mode.
*   Added the fields _safeAreaInset_ and _contentSafeAreaInset_, allowing Mini Apps to ensure that their content properly respects the device's safe area margins.
*   Further added the fields _isActive_ and _isFullscreen_ to the class [WebApp](#initializing-mini-apps).
*   Added the [events](#events-available-for-mini-apps) _activated_, _deactivated_, _safeAreaChanged_, _contentSafeAreaChanged_, _fullscreenChanged_ and _fullscreenFailed_.

**Homescreen Shortcuts**

*   Mini Apps can now be accessed via [direct shortcuts](https://telegram.org/blog/fullscreen-miniapps-and-more#home-screen-shortcuts) added to the **home screen** of mobile devices.
*   Added the method _addToHomeScreen_ to create a shortcut for users to add to their home screens.
*   Added the method _checkHomeScreenStatus_ to determine the status and support of the home screen shortcut for the Mini App on the current device.
*   Added the [events](#events-available-for-mini-apps) _homeScreenAdded_ and _homeScreenChecked_.

**Emoji Status**

*   Mini Apps can now prompt users to set their [emoji status](https://telegram.org/blog/fullscreen-miniapps-and-more#emoji-statuses-from-apps) – or request access to later sync it automatically with in-game badges, third-party APIs and more.
*   Added the method _setEmojiStatus_ to let users manually confirm a custom emoji as their new status via a native dialog.
*   Added the method _requestEmojiStatusAccess_ for obtaining permission to later update a user's emoji status via the Bot API method [setUserEmojiStatus](/bots/api#setuseremojistatus).
*   Added the [events](#events-available-for-mini-apps) _emojiStatusSet_, _emojiStatusFailed_ and _emojiStatusAccessRequested_.

**Media Sharing and File Downloads**

*   Users can now [share media](https://telegram.org/blog/fullscreen-miniapps-and-more#media-sharing) directly from Mini Apps – sending **referral codes**, custom memes, artwork and more to **any chat** or posting them [as a story](https://telegram.org/blog/w3-browser-mini-app-store#sharing-from-mini-apps-to-stories).
*   Added the method _shareMessage_ to share media from Mini Apps to Telegram chats. Also see [PreparedInlineMessage](/bots/api#preparedinlinemessage).
*   Added the method _downloadFile_, introducing support for a **native popup** that prompts users to download files from the Mini App.
*   Added the [events](#events-available-for-mini-apps) _shareMessageSent_, _shareMessageFailed_ and _fileDownloadRequested_.

**Geolocation Access**

*   Mini Apps can now request [geolocation access](https://telegram.org/blog/fullscreen-miniapps-and-more#geolocation-access) to users, allowing them to build virtually any location-based service, from **games** with dynamic points of interest to **interactive maps** for events.
*   Added the field _LocationManager_ to the class [WebApp](#initializing-mini-apps).
*   Added the [events](#events-available-for-mini-apps) _locationManagerUpdated_ and _locationRequested_.

**Device Motion Tracking**

*   Mini Apps can now track detailed [device motion data](https://telegram.org/blog/fullscreen-miniapps-and-more#device-motion-tracking), allowing them to implement better productivity tools, immersive **VR experiences** and more.
*   Added the fields _isOrientationLocked_, _Accelerometer_, _DeviceOrientation_ and _Gyroscope_ to the class [WebApp](#initializing-mini-apps).
*   Added the methods _lockOrientation_ and _unlockOrientation_ to control the screen orientation.
*   Added the [events](#events-available-for-mini-apps) _accelerometerStarted_, _accelerometerStopped_, _accelerometerChanged_, _accelerometerFailed_, _deviceOrientationStarted_, _deviceOrientationStopped_, _deviceOrientationChanged_, _deviceOrientationFailed_, _gyroscopeStarted_, _gyroscopeStopped_, _gyroscopeChanged_, _gyroscopeFailed_.

**Subscription Plans and Gifts for Telegram Stars**

*   Mini Apps now support **paid subscriptions** powered by [Telegram Stars](https://telegram.org/blog/telegram-stars) – **monetizing their efforts** with multiple tiers of content and features.
*   Mini Apps can use their balance of [Telegram Stars](https://telegram.org/blog/telegram-stars) to **send gifts** to their users.
*   You can read more on implementing Paid Subscriptions and Gifts in our [Bot API documentation](/bots/api-changelog#november-17-2024).

**Loading Screen Customization**

*   Mini Apps can customize their loading screen, adding **their own icon** and **specific colors** for light and dark themes.
*   You can access these customization settings in [@BotFather](https://t.me/botfather) via _/mybots > Select Bot > Bot Settings > Configure Mini App > Enable Mini App_

**Hardware-specific Optimizations**

*   Mini Apps running on Android can now receive [basic information](#additional-data-in-user-agent) about a device's processing hardware, allowing them to **optimize user experience** based on the device's capabilities.
*   This information includes the OS, App and SDK's respective versions as well as the device's model and performance class.

**General**

*   The field _photo\_url_ in the class [WebAppUser](#webappuser) is now available to all Mini Apps, allowing them to access a user's profile photo if their privacy settings allow for it.
*   Third parties (e.g., Mini App builders, external SDKs etc.) that receive or process data on behalf of Mini Apps are now able to [validate it](#validating-data-for-third-party-use) without knowing the App's [bot token](/bots/tutorial#obtain-your-bot-token).
*   Debugging [options](#debug-mode-for-mini-apps) have been expanded to include full support for **iOS devices**. You can use these tools to find app-specific issues in your Mini App.

#### [](#september-6-2024)September 6, 2024

**Bot API 7.10**

*   Added the field _SecondaryButton_ to the class [WebApp](#initializing-mini-apps).
*   Added the event _secondaryButtonClicked_.
*   Renamed the class _MainButton_ to the class [BottomButton](#bottombutton).
*   Added the field _bottomBarColor_ and the method _setBottomBarColor_ to the class [WebApp](#initializing-mini-apps).
*   Added the field _bottom\_bar\_bg\_color_ to the class [ThemeParams](#themeparams).

#### [](#july-31-2024)July 31, 2024

**Bot API 7.8**

*   Added the option for bots to set a [Main Mini App](#launching-the-main-mini-app), which can be previewed and launched directly from a button in the bot's profile or a link.
*   Added the method _shareToStory_ to the class [WebApp](#initializing-mini-apps).

#### [](#july-7-2024)July 7, 2024

**Bot API 7.7**

*   Added the field _isVerticalSwipesEnabled_ and the methods _enableVerticalSwipes_, _disableVerticalSwipes_ to the class [WebApp](#initializing-mini-apps).
*   Added the event _scanQrPopupClosed_.

#### [](#july-1-2024)July 1, 2024

**Bot API 7.6**

*   Added the field _section\_separator\_color_ to the class [ThemeParams](#themeparams).
*   Changed the default opening mode for [Direct Link Mini Apps](#direct-link-mini-apps).

#### [](#march-31-2024)March 31, 2024

**Bot API 7.2**

*   Added the field _BiometricManager_ to the class [WebApp](#initializing-mini-apps).

#### [](#december-29-2023)December 29, 2023

**Bot API 7.0**

*   Added the field _SettingsButton_ to the class [WebApp](#initializing-mini-apps).
*   Added the fields _header\_bg\_color_, _accent\_text\_color_, _section\_bg\_color_, _section\_header\_text\_color_, _subtitle\_text\_color_, _destructive\_text\_color_ to the class [ThemeParams](#themeparams).
*   Mini Apps no longer close when the method _WebApp.openTelegramLink_ is called.

#### [](#september-22-2023)September 22, 2023

**Bot API 6.9**

*   Added the field _CloudStorage_ to the class [WebApp](#initializing-mini-apps).
*   Added the methods _requestWriteAccess_ and _requestContact_ to the class [WebApp](#initializing-mini-apps).
*   Added the fields _added\_to\_attachment\_menu_ and _allows\_write\_to\_pm_ to the class [WebAppUser](#webappuser).
*   Added the events _writeAccessRequested_ and _contactRequested_.
*   Added the ability to set any header color using the _setHeaderColor_ method.

#### [](#april-21-2023)April 21, 2023

**Bot API 6.7**

*   Added support for launching Mini Apps from inline query results and from a direct link.
*   Added the method _switchInlineQuery_ to the class [WebApp](#initializing-mini-apps).

#### [](#december-30-2022)December 30, 2022

**Bot API 6.4**

*   Added the field _platform_, the optional parameter _options_ to the method _openLink_ and the methods _showScanQrPopup_, _closeScanQrPopup_, _readTextFromClipboard_ to the class [WebApp](#initializing-mini-apps).
*   Added the events _qrTextReceived_, _clipboardTextReceived_.

#### [](#august-12-2022)August 12, 2022

**Bot API 6.2**

*   Added the field _isClosingConfirmationEnabled_ and the methods _enableClosingConfirmation_, _disableClosingConfirmation_, _showPopup_, _showAlert_, _showConfirm_ to the class [WebApp](#initializing-mini-apps).
*   Added the field _is\_premium_ to the class [WebAppUser](#webappuser).
*   Added the event _popupClosed_.

#### [](#june-20-2022)June 20, 2022

**Bot API 6.1**

*   Added the ability to use bots added to the attachment menu in group, supergroup and channel chats.
*   Added support for [t.me links](#adding-bots-to-the-attachment-menu) that can be used to select the chat in which the attachment menu with the bot will be opened.
*   Added the fields _version_, _headerColor_, _backgroundColor_, _BackButton_, _HapticFeedback_ and the methods _isVersionAtLeast_, _setHeaderColor_, _setBackgroundColor_, _openLink_, _openTelegramLink_, _openInvoice_ to the class [WebApp](#initializing-mini-apps).
*   Added the field _secondary\_bg\_color_ to the class [ThemeParams](#themeparams).
*   Added the method _offClick_ to the class [MainButton](#mainbutton).
*   Added the fields _chat_, _can\_send\_after_ to the class [WebAppInitData](#webappinitdata).
*   Added the [events](#events-available-for-mini-apps) _backButtonClicked_, _settingsButtonClicked_, _invoiceClosed_.

* * *

### [](#designing-mini-apps)Designing Mini Apps

#### [](#color-schemes)Color Schemes

Mini Apps always receive data about the user's current **color theme** in real time, so you can adjust the appearance of your interfaces to match it. For example, when users switch between **Day and Night** modes or use various [custom themes](https://telegram.org/blog/protected-content-delete-by-date-and-more#global-chat-themes-on-android).

> [Jump to technical information](#themeparams)

#### [](#design-guidelines)Design Guidelines

Telegram apps are known for being snappy, smooth and following a consistent cross-platform design. Your Mini App should ideally reflect these principles.

*   All elements should be responsive and designed with a mobile-first approach.
*   Interactive elements should mimic the style, behavior, and intent of UI components that already exist.
*   All included animations should be smooth, ideally 60fps.
*   All inputs and images should contain labels for accessibility purposes.
*   The app should deliver a seamless experience by monitoring the [dynamic theme-based colors](#color-schemes) provided by the API and using them accordingly.
*   Ensure that the app’s interface respects the [safe area](#safeareainset) and [content safe area](#contentsafeareainset) to avoid overlapping with control elements, especially when using fullscreen mode.
*   For Android devices, consider the additional information in the User-Agent (see [User-Agent details](#additional-data-in-user-agent)) and adjust for the device’s performance class, minimizing animations and visual effects on low-performance devices to ensure smooth performance.

* * *

### [](#implementing-mini-apps)Implementing Mini Apps

Telegram currently supports seven different ways of launching Mini Apps: the main Mini App from a [profile button](#launching-the-main-mini-app), from a [keyboard button](#keyboard-button-mini-apps), from an [inline button](#inline-button-mini-apps), from the [bot menu button](#launching-mini-apps-from-the-menu-button), via [inline mode](#inline-mode-mini-apps), from a [direct link](#direct-link-mini-apps) – and even from the [attachment menu](#launching-mini-apps-from-the-attachment-menu).

[![Types of buttons](/file/464001388/10b1a/IYpn0wWfggw.1156850/fd9a32baa81dcecbe4)](/file/464001388/10b1a/IYpn0wWfggw.1156850/fd9a32baa81dcecbe4)

#### [](#keyboard-button-mini-apps)Keyboard Button Mini Apps

> **TL;DR:** Mini Apps launched from a **web\_app** type [keyboard button](/bots/api#keyboardbutton) can send data back to the bot in a _service message_ using [Telegram.WebApp.sendData](#initializing-mini-apps). This makes it possible for the bot to produce a response without communicating with any external servers.

Users can interact with bots using [custom keyboards](/bots#keyboards), [buttons under bot messages](/bots#inline-keyboards-and-on-the-fly-updating), as well as by sending freeform **text messages** or any of the **attachment types** supported by Telegram: photos and videos, files, locations, contacts and polls. For even more flexibility, bots can utilize the full power of **HTML5** to create user-friendly input interfaces.

You can send a **web\_app** type [KeyboardButton](/bots/api#keyboardbutton) that opens a Mini App from the specified URL.

To transmit data from the user back to the bot, the Mini App can call the [Telegram.WebApp.sendData](#initializing-mini-apps) method. Data will be transmitted to the bot as a String in a service message. The bot can continue communicating with the user after receiving it.

**Good for:**

*   **Сustom data input interfaces** (a personalized calendar for selecting dates; selecting data from a list with advanced search options; a randomizer that lets the user “spin a wheel” and chooses one of the available options, etc.)
*   **Reusable components** that do not depend on a particular bot.

#### [](#inline-button-mini-apps)Inline Button Mini Apps

> **TL;DR:** For more interactive Mini Apps like [@DurgerKingBot](https://t.me/durgerkingbot), use a **web\_app** type [Inline KeyboardButton](/bots/api#inlinekeyboardbutton), which gets basic user information and can be used to send a message on behalf of the user to the chat with the bot.

If receiving text data alone is insufficient or you need a more advanced and personalized interface, you can open a Mini App using a **web\_app** type [Inline KeyboardButton](/bots/api#inlinekeyboardbutton).

From the button, a Mini App will open with the URL specified in the button. In addition to the user's [theme settings](#color-schemes), it will receive basic user information (`ID`, `name`, `username`, `language_code`) and a unique identifier for the session, **query\_id**, which allows messages on behalf of the user to be sent back to the bot.

The bot can call the Bot API method [answerWebAppQuery](/bots/api#answerwebappquery) to send an inline message from the user back to the bot and close the Mini App. After receiving the message, the bot can continue communicating with the user.

**Good for:**

*   Fully-fledged web services and integrations of any kind.
*   The use cases are effectively **unlimited**.

#### [](#launching-mini-apps-from-the-menu-button)Launching Mini Apps from the Menu Button

> **TL;DR:** Mini Apps can be launched from a customized menu button. This simply offers a quicker way to access the app and is otherwise **identical** to [launching a mini app from an inline button](#inline-button-mini-apps).

By default, chats with bots always show a convenient **menu button** that provides quick access to all listed [commands](/bots#commands). With [Bot API 6.0](/bots/api-changelog#april-16-2022), this button can be used to **launch a Mini App** instead.

To configure the menu button, you must specify the text it should show and the Mini App URL. There are two ways to set these parameters:

*   To customize the button for **all users**, use [@BotFather](https://t.me/botfather) (the `/setmenubutton` command or _Bot Settings > Menu Button_).
*   To customize the button for both **all users** and **specific users**, use the [setChatMenuButton](/bots/api#setchatmenubutton) method in the Bot API. For example, change the button text according to the user's language, or show links to different Mini Apps based on a user's settings in your bot.

Apart from this, Mini Apps opened via the menu button work in the exact same way as when [using inline buttons](#inline-button-mini-apps).

> [@DurgerKingBot](https://t.me/durgerkingbot) allows launching its Mini App both from an inline button and from the menu button.

#### [](#launching-the-main-mini-app)Launching the main Mini App

> **TL;DR:** If your bot is a mini app, you can add a prominent **Launch app** button as well as high-quality demo videos and screenshots to the bot’s profile. To do this, go to [@BotFather](https://t.me/botfather) and set up your bot's **Main Mini App**.

If your bot is a mini app, you can unlock a number of features that streamline and simplify the way in which users view and interact with it. To do this, go to [@BotFather](https://t.me/botfather) and set up your bot's **Main Mini App**.

After setting a main mini app, you'll be able to upload detailed **media preview demos** to publicly highlight your app's key features on its profile. A **Launch app** button will also appear, allowing users to open your app directly from its profile. Bots that enabled a main mini app will be displayed in the _Apps_ tab of the search for users who have launched them.

> Media previews support [multiple languages](/bots/features#mini-app-previews) – so you can upload **translated versions** of your previews that will be shown to users based on their **app language**.

A bot's **main Mini App** can also be opened in the current chat by direct link in the format `https://t.me/botusername?startapp`. If a non-empty _startapp_ parameter is included in the link, it will be passed to the Mini App in the _start\_param_ field and in the GET parameter _tgWebAppStartParam_.

**Examples**

`https://t.me/botusername?startapp`  
`https://t.me/botusername?startapp=command`  
`https://t.me/botusername?startapp=command&mode=compact`

In this mode, Mini Apps can use the _chat\_type_ and _chat\_instance_ parameters to keep track of the current chat context. This introduces support for **concurrent** and **shared** usage by multiple chat members – to create live whiteboards, group orders, multiplayer games and similar apps.

By default, the main Mini App opens to full-screen height, and users cannot reduce them to half-height. However, you can change this behavior via [@BotFather](https://t.me/botfather) or by including the parameter `mode=compact` in the link to the Mini App, in which case it will open to half-screen height by default.

**Good for:**

*   Fully-fledged web services and integrations that any user can open in one tap.
*   Cooperative, multiplayer or teamwork-oriented services within a chat context.
*   The use cases are effectively **unlimited**.

> Successful bots which **enable** a main Mini App and **accept payments** in [Telegram Stars](/bots/payments-stars) may be featured in the Telegram [Mini App Store](https://t.me/BotNews/99). To increase the chances of being featured, we recommend uploading high-quality media showcasing your app on your bot's profile and following our [design guidelines](#design-guidelines).

#### [](#inline-mode-mini-apps)Inline Mode Mini Apps

> **TL;DR:** Mini Apps launched via **web\_app** type [InlineQueryResultsButton](/bots/api#inlinequeryresultsbutton) can be used anywhere in inline mode. Users can create content in a web interface and then seamlessly send it to the current chat via inline mode.

You can use the _button_ parameter in the [answerInlineQuery](/bots/api#answerinlinequery) method to display a special 'Switch to Mini App' button either above or in place of the inline results. This button will **open a Mini App** from the specified URL. Once done, you can call the [Telegram.WebApp.switchInlineQuery](#initializing-mini-apps) method to send the user back to inline mode.

Inline Mini Apps have **no access** to the chat – they can't read messages or send new ones on behalf of the user. To send messages, the user must be redirected to **inline mode** and actively pick a result.

**Good for:**

*   Fully-fledged web services and integrations in inline mode.

#### [](#direct-link-mini-apps)Direct Link Mini Apps

> **TL;DR:** Mini App Bots can be launched from a direct link in any chat. They support a _startapp_ parameter and are aware of the current chat context.

You can use direct links to **open a Mini App** directly in the current chat. If a non-empty _startapp_ parameter is included in the link, it will be passed to the Mini App in the _start\_param_ field and in the GET parameter _tgWebAppStartParam_.

In this mode, Mini Apps can use the _chat\_type_ and _chat\_instance_ parameters to keep track of the current chat context. This introduces support for **concurrent** and **shared** usage by multiple chat members – to create live whiteboards, group orders, multiplayer games and similar apps.

Mini Apps opened from a direct link have **no access** to the chat – they can't read messages or send new ones on behalf of the user. To send messages, the user must be redirected to **inline mode** and actively pick a result.

Starting from Bot API 7.6, by default, Mini Apps of this type open to full-screen height, and users cannot reduce them to half-height. However, you can change this behavior by including the parameter `mode=compact` in the link to the Mini App, in which case it will open to half-screen height by default.

**Examples**

`https://t.me/botusername/appname`  
`https://t.me/botusername/appname?startapp=command`  
`https://t.me/botusername/appname?startapp=command&mode=compact`

**Good for:**

*   Fully-fledged web services and integrations that any user can open in one tap.
*   Cooperative, multiplayer or teamwork-oriented services within a chat context.
*   The use cases are effectively **unlimited**.

#### [](#launching-mini-apps-from-the-attachment-menu)Launching Mini Apps from the Attachment Menu

> **TL;DR:** Mini App Bots can request to be added directly to a user's attachment menu, allowing them to be quickly launched from any chat. To try this mode, open this [attachment menu link](https://t.me/durgerkingbot?startattach) for _@DurgerKingBot_, then use the ![Attach](/file/464001085/2/E4hNXSNQimQ.2503/bf6ffcab3cb3afd43d) menu in **any type of chat**.

Mini App Bots can request to be added directly to a user's attachment menu, allowing them to be quickly launched from **any type of chat**. You can configure in which types of chats your mini app can be started from the attachment menu (private, groups, supergroups or channels).

Attachment menu integration is currently only available for major advertisers on the [Telegram Ad Platform](https://promote.telegram.org/basics). However, **all bots** can use it in the [test server environment](#using-bots-in-the-test-environment).

To enable this feature for your bot, open [@BotFather](https://t.me/botfather) [from an account on the test server](#using-bots-in-the-test-environment) and send the `/setattach` command – or go to _Bot Settings > Configure Attachment Menu_. Then specify the URL that will be opened to launch the bot's Mini App via its icon in the attachment menu.

You can add a 'Settings' item to the context menu of your Mini App using [@BotFather](https://t.me/botfather). When users select this option from the menu, your bot will receive a `settingsButtonClicked` event.

In addition to the user's [theme settings](#color-schemes), the bot will receive basic user information (`ID`, `name`, `username`, `language_code`, `photo`), as well as public info about the chat partner (`ID`, `name`, `username`, `photo`) or the chat info (`ID`, `type`, `title`, `username`, `photo`) and a unique identifier for the web view session **query\_id**, which allows messages of any type to be sent to the chat on behalf of the user that opened the bot.

The bot can call the Bot API method [answerWebAppQuery](/bots/api#answerwebappquery), which sends an inline message from the user via the bot to the chat where it was launched and closes the Mini App.

> You can read more about adding bots to the attachment menu [here](#adding-bots-to-the-attachment-menu).

* * *

### [](#initializing-mini-apps)Initializing Mini Apps

To connect your Mini App to the Telegram client, place the script [telegram-web-app.js](https://telegram.org/js/telegram-web-app.js?56) in the `<head>` tag before any other scripts, using this code:

    <script src="https://telegram.org/js/telegram-web-app.js?56"></script>

Once the script is connected, a `window.Telegram.WebApp` object will become available with the following fields:

Field

Type

Description

initData

String

A string with raw data transferred to the Mini App, convenient for [validating data](#validating-data-received-via-the-mini-app).  
**WARNING:** [Validate data](#validating-data-received-via-the-mini-app) from this field before using it on the bot's server.

initDataUnsafe

[WebAppInitData](#webappinitdata)

An object with input data transferred to the Mini App.  
**WARNING:** Data from this field should not be trusted. You should only use data from _initData_ on the bot's server and only after it has been [validated](#validating-data-received-via-the-mini-app).

version

String

The version of the Bot API available in the user's Telegram app.

platform

String

The name of the platform of the user's Telegram app.

colorScheme

String

The color scheme currently used in the Telegram app. Either “light” or “dark”.  
Also available as the CSS variable `var(--tg-color-scheme)`.

themeParams

[ThemeParams](#themeparams)

An object containing the current theme settings used in the Telegram app.

isActive NEW

Boolean

Bot API 8.0+ _True_, if the Mini App is currently active. _False_, if the Mini App is minimized.

isExpanded

Boolean

_True_, if the Mini App is expanded to the maximum available height. False, if the Mini App occupies part of the screen and can be expanded to the full height using the **expand()** method.

viewportHeight

Float

The current height of the visible area of the Mini App. Also available in CSS as the variable `var(--tg-viewport-height)`.  
  
The application can display just the top part of the Mini App, with its lower part remaining outside the screen area. From this position, the user can “pull” the Mini App to its maximum height, while the bot can do the same by calling the **expand()** method. As the position of the Mini App changes, the current height value of the visible area will be updated in real time.  
  
Please note that the refresh rate of this value is not sufficient to smoothly follow the lower border of the window. It should not be used to pin interface elements to the bottom of the visible area. It's more appropriate to use the value of the `viewportStableHeight` field for this purpose.

viewportStableHeight

Float

The height of the visible area of the Mini App in its last stable state. Also available in CSS as a variable `var(--tg-viewport-stable-height)`.  
  
The application can display just the top part of the Mini App, with its lower part remaining outside the screen area. From this position, the user can “pull” the Mini App to its maximum height, while the bot can do the same by calling the **expand()** method. Unlike the value of `viewportHeight`, the value of `viewportStableHeight` does not change as the position of the Mini App changes with user gestures or during animations. The value of `viewportStableHeight` will be updated after all gestures and animations are completed and the Mini App reaches its final size.  
  
_Note the [event](#events-available-for-mini-apps) `viewportChanged` with the passed parameter `isStateStable=true`, which will allow you to track when the stable state of the height of the visible area changes._

headerColor

String

Current header color in the `#RRGGBB` format.

backgroundColor

String

Current background color in the `#RRGGBB` format.

bottomBarColor

String

Current bottom bar color in the `#RRGGBB` format.

isClosingConfirmationEnabled

Boolean

_True_, if the confirmation dialog is enabled while the user is trying to close the Mini App. _False_, if the confirmation dialog is disabled.

isVerticalSwipesEnabled

Boolean

_True_, if vertical swipes to close or minimize the Mini App are enabled. _False_, if vertical swipes to close or minimize the Mini App are disabled. In any case, the user will still be able to minimize and close the Mini App by swiping the Mini App's header.

isFullscreen NEW

Boolean

_True_, if the Mini App is currently being displayed in fullscreen mode.

isOrientationLocked NEW

Boolean

_True_, if the Mini App’s orientation is currently locked. _False_, if orientation changes freely based on the device’s rotation.

safeAreaInset NEW

[SafeAreaInset](#safeareainset)

An object representing the device's safe area insets, accounting for system UI elements like notches or navigation bars.

contentSafeAreaInset NEW

[ContentSafeAreaInset](#contentsafeareainset)

An object representing the safe area for displaying content within the app, free from overlapping Telegram UI elements.

BackButton

[BackButton](#backbutton)

An object for controlling the back button which can be displayed in the header of the Mini App in the Telegram interface.

MainButton

[BottomButton](#bottombutton)

An object for controlling the main button, which is displayed at the bottom of the Mini App in the Telegram interface.

SecondaryButton

[BottomButton](#bottombutton)

An object for controlling the secondary button, which is displayed at the bottom of the Mini App in the Telegram interface.

SettingsButton

[SettingsButton](#settingsbutton)

An object for controlling the Settings item in the context menu of the Mini App in the Telegram interface.

HapticFeedback

[HapticFeedback](#hapticfeedback)

An object for controlling haptic feedback.

CloudStorage

[CloudStorage](#cloudstorage)

An object for controlling cloud storage.

BiometricManager

[BiometricManager](#biometricmanager)

An object for controlling biometrics on the device.

Accelerometer NEW

[Accelerometer](#accelerometer)

An object for accessing accelerometer data on the device.

DeviceOrientation NEW

[DeviceOrientation](#deviceorientation)

An object for accessing device orientation data on the device.

Gyroscope NEW

[Gyroscope](#gyroscope)

An object for accessing gyroscope data on the device.

LocationManager NEW

[LocationManager](#locationmanager)

An object for controlling location on the device.

isVersionAtLeast(version)

Function

Returns true if the user's app supports a version of the Bot API that is equal to or higher than the version passed as the parameter.

setHeaderColor(color)

Function

Bot API 6.1+ A method that sets the app header color in the `#RRGGBB` format. You can also use keywords _bg\_color_ and _secondary\_bg\_color_.  
  
Up to Bot API 6.9 You can only pass _Telegram.WebApp.themeParams.bg\_color_ or _Telegram.WebApp.themeParams.secondary\_bg\_color_ as a color or _bg\_color_, _secondary\_bg\_color_ keywords.

setBackgroundColor(color)

Function

Bot API 6.1+ A method that sets the app background color in the `#RRGGBB` format. You can also use keywords _bg\_color_ and _secondary\_bg\_color_.

setBottomBarColor(color)

Function

Bot API 7.10+ A method that sets the app's bottom bar color in the `#RRGGBB` format. You can also use the keywords _bg\_color_, _secondary\_bg\_color_, and _bottom\_bar\_bg\_color_. This color is also applied to the navigation bar on Android.

enableClosingConfirmation()

Function

Bot API 6.2+ A method that enables a confirmation dialog while the user is trying to close the Mini App.

disableClosingConfirmation()

Function

Bot API 6.2+ A method that disables the confirmation dialog while the user is trying to close the Mini App.

enableVerticalSwipes()

Function

Bot API 7.7+ A method that enables vertical swipes to close or minimize the Mini App. For user convenience, it is recommended to always enable swipes unless they conflict with the Mini App's own gestures.

disableVerticalSwipes()

Function

Bot API 7.7+ A method that disables vertical swipes to close or minimize the Mini App. This method is useful if your Mini App uses swipe gestures that may conflict with the gestures for minimizing and closing the app.

requestFullscreen() NEW

Function

Bot API 8.0+ A method that requests opening the Mini App in fullscreen mode. Although the header is transparent in fullscreen mode, it is recommended that the Mini App sets the header color using the _setHeaderColor_ method. This color helps determine a contrasting color for the status bar and other UI controls.

exitFullscreen() NEW

Function

Bot API 8.0+ A method that requests exiting fullscreen mode.

lockOrientation() NEW

Function

Bot API 8.0+ A method that locks the Mini App’s orientation to its current mode (either portrait or landscape). Once locked, the orientation remains fixed, regardless of device rotation. This is useful if a stable orientation is needed during specific interactions.

unlockOrientation() NEW

Function

Bot API 8.0+ A method that unlocks the Mini App’s orientation, allowing it to follow the device's rotation freely. Use this to restore automatic orientation adjustments based on the device orientation.

addToHomeScreen() NEW

Function

Bot API 8.0+ A method that prompts the user to add the Mini App to the home screen. After successfully adding the icon, the `homeScreenAdded` event will be triggered if supported by the device. Note that if the device cannot determine the installation status, the event may not be received even if the icon has been added.

checkHomeScreenStatus(\[callback\]) NEW

Function

Bot API 8.0+ A method that checks if adding to the home screen is supported and if the Mini App has already been added. If an optional _callback_ parameter is provided, the _callback_ function will be called with a single argument _status_, which is a string indicating the home screen status. Possible values for _status_ are:  
\- **unsupported** – the feature is not supported, and it is not possible to add the icon to the home screen,  
\- **unknown** – the feature is supported, and the icon can be added, but it is not possible to determine if the icon has already been added,  
\- **added** – the icon has already been added to the home screen,  
\- **missed** – the icon has not been added to the home screen.

onEvent(eventType, eventHandler)

Function

A method that sets the app event handler. Check [the list of available events](#events-available-for-mini-apps).

offEvent(eventType, eventHandler)

Function

A method that deletes a previously set event handler.

sendData(data)

Function

A method used to send data to the bot. When this method is called, a service message is sent to the bot containing the data _data_ of the length up to 4096 bytes, and the Mini App is closed. See the field _web\_app\_data_ in the class [Message](/bots/api#message).  
  
_This method is only available for Mini Apps launched via a [Keyboard button](#keyboard-button-mini-apps)._

switchInlineQuery(query\[, choose\_chat\_types\])

Function

Bot API 6.7+ A method that inserts the bot's username and the specified inline _query_ in the current chat's input field. Query may be empty, in which case only the bot's username will be inserted. If an optional _choose\_chat\_types_ parameter was passed, the client prompts the user to choose a specific chat, then opens that chat and inserts the bot's username and the specified inline query in the input field. You can specify which types of chats the user will be able to choose from. It can be one or more of the following types: _users_, _bots_, _groups_, _channels_.

openLink(url\[, options\])

Function

A method that opens a link in an external browser. The Mini App will _not_ be closed.  
Bot API 6.4+ If the optional _options_ parameter is passed with the field _try\_instant\_view=true_, the link will be opened in [Instant View](https://instantview.telegram.org/) mode if possible.  
  
_Note that this method can be called only in response to user interaction with the Mini App interface (e.g. a click inside the Mini App or on the main button)_

openTelegramLink(url)

Function

A method that opens a telegram link inside the Telegram app. The Mini App will _not_ be closed after this method is called.  
  
Up to Bot API 7.0 The Mini App _will_ be closed after this method is called.

openInvoice(url\[, callback\])

Function

Bot API 6.1+ A method that opens an invoice using the link _url_. The Mini App will receive the [event](#events-available-for-mini-apps) _invoiceClosed_ when the invoice is closed. If an optional _callback_ parameter was passed, the _callback_ function will be called and the invoice status will be passed as the first argument.

shareToStory(media\_url\[, params\])

Function

Bot API 7.8+ A method that opens the native story editor with the media specified in the _media\_url_ parameter as an HTTPS URL. An optional _params_ argument of the type [StoryShareParams](#storyshareparams) describes additional sharing settings.

shareMessage(msg\_id\[, callback\]) NEW

Function

Bot API 8.0+ A method that opens a dialog allowing the user to share a message provided by the bot. If an optional _callback_ parameter is provided, the _callback_ function will be called with a boolean as the first argument, indicating whether the message was successfully sent. The message id passed to this method must belong to a [PreparedInlineMessage](/bots/api#preparedinlinemessage) previously obtained via the Bot API method [savePreparedInlineMessage](/bots/api#savepreparedinlinemessage).

setEmojiStatus(custom\_emoji\_id\[, params, callback\])

Function

Bot API 8.0+ A method that opens a dialog allowing the user to set the specified custom emoji as their status. An optional _params_ argument of type [EmojiStatusParams](#emojistatusparams) specifies additional settings, such as duration. If an optional _callback_ parameter is provided, the _callback_ function will be called with a boolean as the first argument, indicating whether the status was set.  
  
_Note: this method opens a native dialog and cannot be used to set the emoji status without manual user interaction. For fully programmatic changes, you should instead use the Bot API method [setUserEmojiStatus](bots/api#setuseremojistatus) after obtaining authorization to do so via the Mini App method requestEmojiStatusAccess._

requestEmojiStatusAccess(\[callback\]) NEW

Function

Bot API 8.0+ A method that shows a native popup requesting permission for the bot to manage user's emoji status. If an optional _callback_ parameter was passed, the _callback_ function will be called when the popup is closed and the first argument will be a boolean indicating whether the user granted this access.

downloadFile(params\[, callback\]) NEW

Function

Bot API 8.0+ A method that displays a native popup prompting the user to download a file specified by the _params_ argument of type [DownloadFileParams](#downloadfileparams). If an optional _callback_ parameter is provided, the _callback_ function will be called when the popup is closed, with the first argument as a boolean indicating whether the user accepted the download request.

showPopup(params\[, callback\])

Function

Bot API 6.2+ A method that shows a native popup described by the _params_ argument of the type [PopupParams](#popupparams). The Mini App will receive the [event](#events-available-for-mini-apps) _popupClosed_ when the popup is closed. If an optional _callback_ parameter was passed, the _callback_ function will be called and the field _id_ of the pressed button will be passed as the first argument.

showAlert(message\[, callback\])

Function

Bot API 6.2+ A method that shows _message_ in a simple alert with a 'Close' button. If an optional _callback_ parameter was passed, the _callback_ function will be called when the popup is closed.

showConfirm(message\[, callback\])

Function

Bot API 6.2+ A method that shows _message_ in a simple confirmation window with 'OK' and 'Cancel' buttons. If an optional _callback_ parameter was passed, the _callback_ function will be called when the popup is closed and the first argument will be a boolean indicating whether the user pressed the 'OK' button.

showScanQrPopup(params\[, callback\])

Function

Bot API 6.4+ A method that shows a native popup for scanning a QR code described by the _params_ argument of the type [ScanQrPopupParams](#scanqrpopupparams). The Mini App will receive the [event](#events-available-for-mini-apps) _qrTextReceived_ every time the scanner catches a code with text data. If an optional _callback_ parameter was passed, the _callback_ function will be called and the text from the QR code will be passed as the first argument. Returning _true_ inside this callback function causes the popup to be closed. Starting from Bot API 7.7, the Mini App will receive the _scanQrPopupClosed_ event if the user closes the native popup for scanning a QR code.

closeScanQrPopup()

Function

Bot API 6.4+ A method that closes the native popup for scanning a QR code opened with the _showScanQrPopup_ method. Run it if you received valid data in the [event](#events-available-for-mini-apps) _qrTextReceived_.

readTextFromClipboard(\[callback\])

Function

Bot API 6.4+ A method that requests text from the clipboard. The Mini App will receive the [event](#events-available-for-mini-apps) _clipboardTextReceived_. If an optional _callback_ parameter was passed, the _callback_ function will be called and the text from the clipboard will be passed as the first argument.  
  
_Note: this method can be called only for Mini Apps launched from the attachment menu and only in response to a user interaction with the Mini App interface (e.g. a click inside the Mini App or on the main button)._

requestWriteAccess(\[callback\])

Function

Bot API 6.9+ A method that shows a native popup requesting permission for the bot to send messages to the user. If an optional _callback_ parameter was passed, the _callback_ function will be called when the popup is closed and the first argument will be a boolean indicating whether the user granted this access.

requestContact(\[callback\])

Function

Bot API 6.9+ A method that shows a native popup prompting the user for their phone number. If an optional _callback_ parameter was passed, the _callback_ function will be called when the popup is closed and the first argument will be a boolean indicating whether the user shared its phone number.

ready()

Function

A method that informs the Telegram app that the Mini App is ready to be displayed.  
It is recommended to call this method as early as possible, as soon as all essential interface elements are loaded. Once this method is called, the loading placeholder is hidden and the Mini App is shown.  
If the method is not called, the placeholder will be hidden only when the page is fully loaded.

expand()

Function

A method that expands the Mini App to the maximum available height. To find out if the Mini App is expanded to the maximum height, refer to the value of the _Telegram.WebApp.isExpanded_ parameter

close()

Function

A method that closes the Mini App.

#### [](#themeparams)ThemeParams

Mini Apps can [adjust the appearance](#color-schemes) of the interface to match the Telegram user's app in real time. This object contains the user's current theme settings:

Field

Type

Description

bg\_color

String

_Optional_. Background color in the `#RRGGBB` format.  
Also available as the CSS variable `var(--tg-theme-bg-color)`.

text\_color

String

_Optional_. Main text color in the `#RRGGBB` format.  
Also available as the CSS variable `var(--tg-theme-text-color)`.

hint\_color

String

_Optional_. Hint text color in the `#RRGGBB` format.  
Also available as the CSS variable `var(--tg-theme-hint-color)`.

link\_color

String

_Optional_. Link color in the `#RRGGBB` format.  
Also available as the CSS variable `var(--tg-theme-link-color)`.

button\_color

String

_Optional_. Button color in the `#RRGGBB` format.  
Also available as the CSS variable `var(--tg-theme-button-color)`.

button\_text\_color

String

_Optional_. Button text color in the `#RRGGBB` format.  
Also available as the CSS variable `var(--tg-theme-button-text-color)`.

secondary\_bg\_color

String

_Optional_. Bot API 6.1+ Secondary background color in the `#RRGGBB` format.  
Also available as the CSS variable `var(--tg-theme-secondary-bg-color)`.

header\_bg\_color

String

_Optional_. Bot API 7.0+ Header background color in the `#RRGGBB` format.  
Also available as the CSS variable `var(--tg-theme-header-bg-color)`.

bottom\_bar\_bg\_color

String

_Optional_. Bot API 7.10+ Bottom background color in the `#RRGGBB` format.  
Also available as the CSS variable `var(--tg-theme-bottom-bar-bg-color)`.

accent\_text\_color

String

_Optional_. Bot API 7.0+ Accent text color in the `#RRGGBB` format.  
Also available as the CSS variable `var(--tg-theme-accent-text-color)`.

section\_bg\_color

String

_Optional_. Bot API 7.0+ Background color for the section in the `#RRGGBB` format. It is recommended to use this in conjunction with _secondary\_bg\_color_.  
Also available as the CSS variable `var(--tg-theme-section-bg-color)`.

section\_header\_text\_color

String

_Optional_. Bot API 7.0+ Header text color for the section in the `#RRGGBB` format.  
Also available as the CSS variable `var(--tg-theme-section-header-text-color)`.

section\_separator\_color

String

_Optional_. Bot API 7.6+ Section separator color in the `#RRGGBB` format.  
Also available as the CSS variable `var(--tg-theme-section-separator-color)`.

subtitle\_text\_color

String

_Optional_. Bot API 7.0+ Subtitle text color in the `#RRGGBB` format.  
Also available as the CSS variable `var(--tg-theme-subtitle-text-color)`.

destructive\_text\_color

String

_Optional_. Bot API 7.0+ Text color for destructive actions in the `#RRGGBB` format.  
Also available as the CSS variable `var(--tg-theme-destructive-text-color)`.

[![](/file/400780400851/2/6GwDkk6T-aY.416569/b591d589108b487d63 "WebViewColors explained")](/file/400780400851/2/6GwDkk6T-aY.416569/b591d589108b487d63)

#### [](#storyshareparams)StoryShareParams

This object describes additional sharing settings for the native story editor.

Field

Type

Description

text

String

_Optional_. The caption to be added to the media, 0-200 characters for regular users and 0-2048 characters for [premium](https://telegram.org/faq_premium#telegram-premium) subscribers.

widget\_link

[StoryWidgetLink](#storywidgetlink)

_Optional_. An object that describes a widget link to be included in the story. Note that only [premium](https://telegram.org/faq_premium#telegram-premium) subscribers can post stories with links.

#### [](#storywidgetlink)StoryWidgetLink

This object describes a widget link to be included in the story.

Field

Type

Description

url

String

The URL to be included in the story.

name

String

_Optional_. The name to be displayed for the widget link, 0-48 characters.

#### [](#scanqrpopupparams)ScanQrPopupParams

This object describes the native popup for scanning QR codes.

Field

Type

Description

text

String

_Optional_. The text to be displayed under the 'Scan QR' heading, 0-64 characters.

#### [](#popupparams)PopupParams

This object describes the native popup.

Field

Type

Description

title

String

_Optional_. The text to be displayed in the popup title, 0-64 characters.

message

String

The message to be displayed in the body of the popup, 1-256 characters.

buttons

Array of [PopupButton](#popupbutton)

_Optional_. List of buttons to be displayed in the popup, 1-3 buttons. Set to _\[{“type”:“close”}\]_ by default.

#### [](#popupbutton)PopupButton

This object describes the native popup button.

Field

Type

Description

id

String

_Optional_. Identifier of the button, 0-64 characters. Set to empty string by default.  
If the button is pressed, its _id_ is returned in the callback and the _popupClosed_ event.

type

String

_Optional_. Type of the button. Set to _default_ by default.  
Can be one of these values:  
\- _default_, a button with the default style,  
\- _ok_, a button with the localized text “OK”,  
\- _close_, a button with the localized text “Close”,  
\- _cancel_, a button with the localized text “Cancel”,  
\- _destructive_, a button with a style that indicates a destructive action (e.g. “Remove”, “Delete”, etc.).

text

String

_Optional_. The text to be displayed on the button, 0-64 characters. Required if _type_ is _default_ or _destructive_. Irrelevant for other types.

#### [](#emojistatusparams)EmojiStatusParams

This object describes additional settings for setting an emoji status.

Field

Type

Description

duration

Integer

_Optional_. The duration for which the status will remain set, in seconds.

#### [](#downloadfileparams)DownloadFileParams

This object describes the parameters for the file download request.

> **Note:** To ensure consistent file download behavior across platforms, it is recommended to include the HTTP header `Content-Disposition: attachment; filename="<file_name>"` in the server response. This header helps prompt the download action and suggests a file name for the downloaded file, especially on web platforms where forced downloads cannot always be guaranteed.

Field

Type

Description

url

String

The HTTPS URL of the file to be downloaded.

file\_name

String

The suggested name for the downloaded file.

#### [](#safeareainset)SafeAreaInset

This object represents the system-defined safe area insets, providing padding values to ensure content remains within visible boundaries, avoiding overlap with system UI elements like notches or navigation bars.

Field

Type

Description

top

Integer

The top inset in pixels, representing the space to avoid at the top of the screen. Also available as the CSS variable `var(--tg-safe-area-inset-top)`.

bottom

Integer

The bottom inset in pixels, representing the space to avoid at the bottom of the screen. Also available as the CSS variable `var(--tg-safe-area-inset-bottom)`.

left

Integer

The left inset in pixels, representing the space to avoid on the left side of the screen. Also available as the CSS variable `var(--tg-safe-area-inset-left)`.

right

Integer

The right inset in pixels, representing the space to avoid on the right side of the screen. Also available as the CSS variable `var(--tg-safe-area-inset-right)`.

[![](/file/400780400066/1/tTFDI7OC8tE.1374724/9e496dd312c7706a38 "SafeAreaInset explained")](/file/400780400066/1/tTFDI7OC8tE.1374724/9e496dd312c7706a38)

#### [](#contentsafeareainset)ContentSafeAreaInset

This object represents the content-defined safe area insets, providing padding values to ensure content remains within visible boundaries, avoiding overlap with Telegram UI elements.

Field

Type

Description

top

Integer

The top inset in pixels, representing the space to avoid at the top of the content area. Also available as the CSS variable `var(--tg-content-safe-area-inset-top)`.

bottom

Integer

The bottom inset in pixels, representing the space to avoid at the bottom of the content area. Also available as the CSS variable `var(--tg-content-safe-area-inset-bottom)`.

left

Integer

The left inset in pixels, representing the space to avoid on the left side of the content area. Also available as the CSS variable `var(--tg-content-safe-area-inset-left)`.

right

Integer

The right inset in pixels, representing the space to avoid on the right side of the content area. Also available as the CSS variable `var(--tg-content-safe-area-inset-right)`.

[![](/file/400780400676/2/8VT7jCQvpsk.1386608/d249aa072662450345 "ContentSafeAreaInset explained")](/file/400780400676/2/8VT7jCQvpsk.1386608/d249aa072662450345)

#### [](#backbutton)BackButton

This object controls the **back** button, which can be displayed in the header of the Mini App in the Telegram interface.

Field

Type

Description

isVisible

Boolean

Shows whether the button is visible. Set to _false_ by default.

onClick(callback)

Function

Bot API 6.1+ A method that sets the button press event handler. An alias for `Telegram.WebApp.onEvent('backButtonClicked', callback)`

offClick(callback)

Function

Bot API 6.1+ A method that removes the button press event handler. An alias for `Telegram.WebApp.offEvent('backButtonClicked', callback)`

show()

Function

Bot API 6.1+ A method to make the button active and visible.

hide()

Function

Bot API 6.1+ A method to hide the button.

All these methods return the BackButton object so they can be chained.

#### [](#bottombutton)BottomButton

This object controls the button that is displayed at the bottom of the Mini App in the Telegram interface.

Field

Type

Description

type

String

_Readonly._ Type of the button. It can be either _main_ for the main button or _secondary_ for the secondary button.

text

String

Current button text. Set to _Continue_ for the main button and _Cancel_ for the secondary button by default.

color

String

Current button color. Set to _themeParams.button\_color_ for the main button and _themeParams.bottom\_bar\_bg\_color_ for the secondary button by default.

textColor

String

Current button text color. Set to _themeParams.button\_text\_color_ for the main button and _themeParams.button\_color_ for the secondary button by default.

isVisible

Boolean

Shows whether the button is visible. Set to _false_ by default.

isActive

Boolean

Shows whether the button is active. Set to _true_ by default.

hasShineEffect

Boolean

Bot API 7.10+ Shows whether the button has a shine effect. Set to _false_ by default.

position

String

Bot API 7.10+ Position of the secondary button. Not defined for the main button. It applies only if both the main and secondary buttons are visible. Set to _left_ by default.  
Supported values:  
\- _left_, displayed to the left of the main button,  
\- _right_, displayed to the right of the main button,  
\- _top_, displayed above the main button,  
\- _bottom_, displayed below the main button.

isProgressVisible

Boolean

_Readonly._ Shows whether the button is displaying a loading indicator.

setText(text)

Function

A method to set the button text.

onClick(callback)

Function

A method that sets the button's press event handler. An alias for `Telegram.WebApp.onEvent('mainButtonClicked', callback)`

offClick(callback)

Function

A method that removes the button's press event handler. An alias for `Telegram.WebApp.offEvent('mainButtonClicked', callback)`

show()

Function

A method to make the button visible.  
_Note that opening the Mini App from the [attachment menu](#launching-mini-apps-from-the-attachment-menu) hides the main button until the user interacts with the Mini App interface._

hide()

Function

A method to hide the button.

enable()

Function

A method to enable the button.

disable()

Function

A method to disable the button.

showProgress(leaveActive)

Function

A method to show a loading indicator on the button.  
It is recommended to display loading progress if the action tied to the button may take a long time. By default, the button is disabled while the action is in progress. If the parameter `leaveActive=true` is passed, the button remains enabled.

hideProgress()

Function

A method to hide the loading indicator.

setParams(params)

Function

A method to set the button parameters. The _params_ parameter is an object containing one or several fields that need to be changed:  
**text** - button text;  
**color** - button color;  
**text\_color** - button text color;  
**has\_shine\_effect** - Bot API 7.10+ enable shine effect;  
**position** - position of the secondary button;  
**is\_active** - enable the button;  
**is\_visible** - show the button.

All these methods return the BottomButton object so they can be chained.

#### [](#settingsbutton)SettingsButton

This object controls the **Settings** item in the context menu of the Mini App in the Telegram interface.

Field

Type

Description

isVisible

Boolean

Shows whether the context menu item is visible. Set to _false_ by default.

onClick(callback)

Function

Bot API 7.0+ A method that sets the press event handler for the Settings item in the context menu. An alias for `Telegram.WebApp.onEvent('settingsButtonClicked', callback)`

offClick(callback)

Function

Bot API 7.0+ A method that removes the press event handler from the Settings item in the context menu. An alias for `Telegram.WebApp.offEvent('settingsButtonClicked', callback)`

show()

Function

Bot API 7.0+ A method to make the Settings item in the context menu visible.

hide()

Function

Bot API 7.0+ A method to hide the Settings item in the context menu.

All these methods return the [SettingsButton](#settingsbutton) object so they can be chained.

#### [](#hapticfeedback)HapticFeedback

This object controls haptic feedback.

Field

Type

Description

impactOccurred(style)

Function

Bot API 6.1+ A method tells that an impact occurred. The Telegram app may play the appropriate haptics based on style value passed. Style can be one of these values:  
\- _light_, indicates a collision between small or lightweight UI objects,  
\- _medium_, indicates a collision between medium-sized or medium-weight UI objects,  
\- _heavy_, indicates a collision between large or heavyweight UI objects,  
\- _rigid_, indicates a collision between hard or inflexible UI objects,  
\- _soft_, indicates a collision between soft or flexible UI objects.

notificationOccurred(type)

Function

Bot API 6.1+ A method tells that a task or action has succeeded, failed, or produced a warning. The Telegram app may play the appropriate haptics based on type value passed. Type can be one of these values:  
\- _error_, indicates that a task or action has failed,  
\- _success_, indicates that a task or action has completed successfully,  
\- _warning_, indicates that a task or action produced a warning.

selectionChanged()

Function

Bot API 6.1+ A method tells that the user has changed a selection. The Telegram app may play the appropriate haptics.  
  
_Do not use this feedback when the user makes or confirms a selection; use it only when the selection changes._

All these methods return the HapticFeedback object so they can be chained.

#### [](#cloudstorage)CloudStorage

This object controls the cloud storage. Each bot can store up to 1024 items per user in the cloud storage.

Field

Type

Description

setItem(key, value\[, callback\])

Function

Bot API 6.9+ A method that stores a value in the cloud storage using the specified key. The key should contain 1-128 characters, only `A-Z`, `a-z`, `0-9`, `_` and `-` are allowed. The value should contain 0-4096 characters. You can store up to 1024 keys in the cloud storage. If an optional _callback_ parameter was passed, the _callback_ function will be called. In case of an error, the first argument will contain the error. In case of success, the first argument will be _null_ and the second argument will be a boolean indicating whether the value was stored.

getItem(key, callback)

Function

Bot API 6.9+ A method that receives a value from the cloud storage using the specified key. The key should contain 1-128 characters, only `A-Z`, `a-z`, `0-9`, `_` and `-` are allowed. In case of an error, the _callback_ function will be called and the first argument will contain the error. In case of success, the first argument will be _null_ and the value will be passed as the second argument.

getItems(keys, callback)

Function

Bot API 6.9+ A method that receives values from the cloud storage using the specified keys. The keys should contain 1-128 characters, only `A-Z`, `a-z`, `0-9`, `_` and `-` are allowed. In case of an error, the _callback_ function will be called and the first argument will contain the error. In case of success, the first argument will be _null_ and the values will be passed as the second argument.

removeItem(key\[, callback\])

Function

Bot API 6.9+ A method that removes a value from the cloud storage using the specified key. The key should contain 1-128 characters, only `A-Z`, `a-z`, `0-9`, `_` and `-` are allowed. If an optional _callback_ parameter was passed, the _callback_ function will be called. In case of an error, the first argument will contain the error. In case of success, the first argument will be _null_ and the second argument will be a boolean indicating whether the value was removed.

removeItems(keys\[, callback\])

Function

Bot API 6.9+ A method that removes values from the cloud storage using the specified keys. The keys should contain 1-128 characters, only `A-Z`, `a-z`, `0-9`, `_` and `-` are allowed. If an optional _callback_ parameter was passed, the _callback_ function will be called. In case of an error, the first argument will contain the error. In case of success, the first argument will be _null_ and the second argument will be a boolean indicating whether the values were removed.

getKeys(callback)

Function

Bot API 6.9+ A method that receives the list of all keys stored in the cloud storage. In case of an error, the _callback_ function will be called and the first argument will contain the error. In case of success, the first argument will be _null_ and the list of keys will be passed as the second argument.

All these methods return the [CloudStorage](#cloudstorage) object, so they can be chained.

#### [](#biometricmanager)BiometricManager

This object controls biometrics on the device. Before the first use of this object, it needs to be initialized using the _init_ method.

Field

Type

Description

isInited

Boolean

Shows whether biometrics object is initialized.

isBiometricAvailable

Boolean

Shows whether biometrics is available on the current device.

biometricType

String

The type of biometrics currently available on the device. Can be one of these values:  
\- _finger_, fingerprint-based biometrics,  
\- _face_, face-based biometrics,  
\- _unknown_, biometrics of an unknown type.

isAccessRequested

Boolean

Shows whether permission to use biometrics has been requested.

isAccessGranted

Boolean

Shows whether permission to use biometrics has been granted.

isBiometricTokenSaved

Boolean

Shows whether the token is saved in secure storage on the device.

deviceId

String

A unique device identifier that can be used to match the token to the device.

init(\[callback\])

Function

Bot API 7.2+ A method that initializes the BiometricManager object. It should be called before the object's first use. If an optional _callback_ parameter was passed, the _callback_ function will be called when the object is initialized.

requestAccess(params\[, callback\])

Function

Bot API 7.2+ A method that requests permission to use biometrics according to the _params_ argument of type [BiometricRequestAccessParams](#biometricrequestaccessparams). If an optional _callback_ parameter was passed, the _callback_ function will be called and the first argument will be a boolean indicating whether the user granted access.

authenticate(params\[, callback\])

Function

Bot API 7.2+ A method that authenticates the user using biometrics according to the _params_ argument of type [BiometricAuthenticateParams](#biometricauthenticateparams). If an optional _callback_ parameter was passed, the _callback_ function will be called and the first argument will be a boolean indicating whether the user authenticated successfully. If so, the second argument will be a biometric token.

updateBiometricToken(token, \[callback\])

Function

Bot API 7.2+ A method that updates the biometric token in secure storage on the device. To remove the token, pass an empty string. If an optional _callback_ parameter was passed, the _callback_ function will be called and the first argument will be a boolean indicating whether the token was updated.

openSettings()

Function

Bot API 7.2+ A method that opens the biometric access settings for bots. Useful when you need to request biometrics access to users who haven't granted it yet.  
  
_Note that this method can be called only in response to user interaction with the Mini App interface (e.g. a click inside the Mini App or on the main button)_

All these methods return the [BiometricManager](#biometricmanager) object so they can be chained.

#### [](#biometricrequestaccessparams)BiometricRequestAccessParams

This object describes the native popup for requesting permission to use biometrics.

Field

Type

Description

reason

String

_Optional_. The text to be displayed to a user in the popup describing why the bot needs access to biometrics, 0-128 characters.

#### [](#biometricauthenticateparams)BiometricAuthenticateParams

This object describes the native popup for authenticating the user using biometrics.

Field

Type

Description

reason

String

_Optional_. The text to be displayed to a user in the popup describing why you are asking them to authenticate and what action you will be taking based on that authentication, 0-128 characters.

#### [](#accelerometer)Accelerometer

This object provides access to accelerometer data on the device.

Field

Type

Description

isStarted

Boolean

Indicates whether accelerometer tracking is currently active.

x

Float

The current acceleration in the X-axis, measured in m/s².

y

Float

The current acceleration in the Y-axis, measured in m/s².

z

Float

The current acceleration in the Z-axis, measured in m/s².

start(params\[, callback\])

Function

Bot API 8.0+ Starts tracking accelerometer data using _params_ of type [AccelerometerStartParams](#accelerometerstartparams). If an optional _callback_ parameter is provided, the _callback_ function will be called with a boolean indicating whether tracking was successfully started.

stop(\[callback\])

Function

Bot API 8.0+ Stops tracking accelerometer data. If an optional _callback_ parameter is provided, the _callback_ function will be called with a boolean indicating whether tracking was successfully stopped.

All these methods return the [Accelerometer](#accelerometer) object so they can be chained.

[![](/file/400780400808/3/4R4bxuff6H0.529743/2a9f6212eaed26d194 "Accelerometer")](/file/400780400808/3/4R4bxuff6H0.529743/2a9f6212eaed26d194)

#### [](#accelerometerstartparams)AccelerometerStartParams

This object defines the parameters for starting accelerometer tracking.

Field

Type

Description

refresh\_rate

Integer

_Optional._ The refresh rate in milliseconds, with acceptable values ranging from 20 to 1000. Set to _1000_ by default. Note that _refresh\_rate_ may not be supported on all platforms, so the actual tracking frequency may differ from the specified value.

#### [](#deviceorientation)DeviceOrientation

This object provides access to orientation data on the device.

Field

Type

Description

isStarted

Boolean

Indicates whether device orientation tracking is currently active.

absolute

Boolean

A boolean that indicates whether or not the device is providing orientation data in absolute values.

alpha

Float

The rotation around the Z-axis, measured in radians.

beta

Float

The rotation around the X-axis, measured in radians.

gamma

Float

The rotation around the Y-axis, measured in radians.

start(params\[, callback\])

Function

Bot API 8.0+ Starts tracking device orientation data using _params_ of type [DeviceOrientationStartParams](#deviceorientationstartparams). If an optional _callback_ parameter is provided, the _callback_ function will be called with a boolean indicating whether tracking was successfully started.

stop(\[callback\])

Function

Bot API 8.0+ Stops tracking device orientation data. If an optional _callback_ parameter is provided, the _callback_ function will be called with a boolean indicating whether tracking was successfully stopped.

All these methods return the [DeviceOrientation](#deviceorientation) object so they can be chained.

[![](/file/400780400662/2/6ziukR8E4pc.4269149/aa2ec0a86b39709a92 "DeviceOrientation")](/file/400780400662/2/6ziukR8E4pc.4269149/aa2ec0a86b39709a92)

#### [](#deviceorientationstartparams)DeviceOrientationStartParams

This object defines the parameters for starting device orientation tracking.

Field

Type

Description

refresh\_rate

Integer

_Optional._ The refresh rate in milliseconds, with acceptable values ranging from 20 to 1000. Set to _1000_ by default. Note that _refresh\_rate_ may not be supported on all platforms, so the actual tracking frequency may differ from the specified value.

need\_absolute

Boolean

_Optional._ Pass _true_ to receive absolute orientation data, allowing you to determine the device's attitude relative to magnetic north. Use this option if implementing features like a compass in your app. If relative data is sufficient, pass _false_. Set to _false_ by default.  
  
**Note:** Keep in mind that some devices may not support absolute orientation data. In such cases, you will receive relative data even if _need\_absolute=true_ is passed. Check the _DeviceOrientation.absolute_ parameter to determine whether the data provided is absolute or relative.

#### [](#gyroscope)Gyroscope

This object provides access to gyroscope data on the device.

Field

Type

Description

isStarted

Boolean

Indicates whether gyroscope tracking is currently active.

x

Float

The current rotation rate around the X-axis, measured in rad/s.

y

Float

The current rotation rate around the Y-axis, measured in rad/s.

z

Float

The current rotation rate around the Z-axis, measured in rad/s.

start(params\[, callback\])

Function

Bot API 8.0+ Starts tracking gyroscope data using _params_ of type [GyroscopeStartParams](#gyroscopestartparams). If an optional _callback_ parameter is provided, the _callback_ function will be called with a boolean indicating whether tracking was successfully started.

stop(\[callback\])

Function

Bot API 8.0+ Stops tracking gyroscope data. If an optional _callback_ parameter is provided, the _callback_ function will be called with a boolean indicating whether tracking was successfully stopped.

All these methods return the [Gyroscope](#gyroscope) object so they can be chained.

[![](/file/400780400892/5/GDxCwbAAG7U.579631/7895611bc90a998a13 "Gyroscope")](/file/400780400892/5/GDxCwbAAG7U.579631/7895611bc90a998a13)

#### [](#gyroscopestartparams)GyroscopeStartParams

This object defines the parameters for starting gyroscope tracking.

Field

Type

Description

refresh\_rate

Integer

_Optional._ The refresh rate in milliseconds, with acceptable values ranging from 20 to 1000. Set to _1000_ by default. Note that _refresh\_rate_ may not be supported on all platforms, so the actual tracking frequency may differ from the specified value.

#### [](#locationmanager)LocationManager

This object controls location access on the device. Before the first use of this object, it needs to be initialized using the _init_ method.

Field

Type

Description

isInited

Boolean

Shows whether the LocationManager object has been initialized.

isLocationAvailable

Boolean

Shows whether location services are available on the current device.

isAccessRequested

Boolean

Shows whether permission to use location has been requested.

isAccessGranted

Boolean

Shows whether permission to use location has been granted.

init(\[callback\])

Function

Bot API 8.0+ A method that initializes the LocationManager object. It should be called before the object's first use. If an optional _callback_ parameter is provided, the _callback_ function will be called when the object is initialized.

getLocation(callback)

Function

Bot API 8.0+ A method that requests location data. The _callback_ function will be called with _null_ as the first argument if access to location was not granted, or an object of type [LocationData](#locationdata) as the first argument if access was successful.

openSettings()

Function

Bot API 8.0+ A method that opens the location access settings for bots. Useful when you need to request location access from users who haven't granted it yet.  
  
_Note that this method can be called only in response to user interaction with the Mini App interface (e.g., a click inside the Mini App or on the main button)._

All these methods return the [LocationManager](#locationmanager) object so they can be chained.

#### [](#locationdata)LocationData

This object contains data about the current location.

Field

Type

Description

latitude

Float

Latitude in degrees.

longitude

Float

Longitude in degrees.

altitude

Float

Altitude above sea level in meters. _null_ if altitude data is not available on the device.

course

Float

The direction the device is moving in degrees (0 = North, 90 = East, 180 = South, 270 = West). _null_ if course data is not available on the device.

speed

Float

The speed of the device in m/s. _null_ if speed data is not available on the device.

horizontal\_accuracy

Float

Accuracy of the latitude and longitude values in meters. _null_ if horizontal accuracy data is not available on the device.

vertical\_accuracy

Float

Accuracy of the altitude value in meters. _null_ if vertical accuracy data is not available on the device.

course\_accuracy

Float

Accuracy of the course value in degrees. _null_ if course accuracy data is not available on the device.

speed\_accuracy

Float

Accuracy of the speed value in m/s. _null_ if speed accuracy data is not available on the device.

#### [](#webappinitdata)WebAppInitData

This object contains data that is transferred to the Mini App when it is opened. It is empty if the Mini App was launched from a [keyboard button](#keyboard-button-mini-apps) or from [inline mode](#inline-mode-mini-apps).

Field

Type

Description

query\_id

String

_Optional._ A unique identifier for the Mini App session, required for sending messages via the [answerWebAppQuery](/bots/api#answerwebappquery) method.

user

[WebAppUser](#webappuser)

_Optional._ An object containing data about the current user.

receiver

[WebAppUser](#webappuser)

_Optional._ An object containing data about the chat partner of the current user in the chat where the bot was launched via the attachment menu. Returned only for private chats and only for Mini Apps launched via the attachment menu.

chat

[WebAppChat](#webappchat)

_Optional._ An object containing data about the chat where the bot was launched via the attachment menu. Returned for supergroups, channels and group chats – only for Mini Apps launched via the attachment menu.

chat\_type

String

_Optional._ Type of the chat from which the Mini App was opened. Can be either “sender” for a private chat with the user opening the link, “private”, “group”, “supergroup”, or “channel”. Returned only for Mini Apps launched from direct links.

chat\_instance

String

_Optional._ Global identifier, uniquely corresponding to the chat from which the Mini App was opened. Returned only for Mini Apps launched from a direct link.

start\_param

String

_Optional._ The value of the _startattach_ parameter, passed [via link](#adding-bots-to-the-attachment-menu). Only returned for Mini Apps when launched from the attachment menu via link.  
  
The value of the `start_param` parameter will also be passed in the GET-parameter `tgWebAppStartParam`, so the Mini App can load the correct interface right away.

can\_send\_after

Integer

_Optional._ Time in seconds, after which a message can be sent via the [answerWebAppQuery](/bots/api#answerwebappquery) method.

auth\_date

Integer

Unix time when the form was opened.

hash

String

A hash of all passed parameters, which the bot server can use to [check their validity](#validating-data-received-via-the-mini-app).

signature NEW

String

A signature of all passed parameters (except _hash_), which the third party can use to [check their validity](#validating-data-for-third-party-use).

#### [](#webappuser)WebAppUser

This object contains the data of the Mini App user.

Field

Type

Description

id

Integer

A unique identifier for the user or bot. This number may have more than 32 significant bits and some programming languages may have difficulty/silent defects in interpreting it. It has at most 52 significant bits, so a 64-bit integer or a double-precision float type is safe for storing this identifier.

is\_bot

Boolean

_Optional_. _True_, if this user is a bot. Returns in the [receiver](#webappinitdata) field only.

first\_name

String

First name of the user or bot.

last\_name

String

_Optional_. Last name of the user or bot.

username

String

_Optional_. Username of the user or bot.

language\_code

String

_Optional_. [IETF language tag](https://en.wikipedia.org/wiki/IETF_language_tag) of the user's language. Returns in _user_ field only.

is\_premium

True

_Optional_. _True_, if this user is a Telegram Premium user.

added\_to\_attachment\_menu

True

_Optional_. _True_, if this user added the bot to the attachment menu.

allows\_write\_to\_pm

True

_Optional_. _True_, if this user allowed the bot to message them.

photo\_url

String

_Optional_. URL of the user’s profile photo. The photo can be in .jpeg or .svg formats.

#### [](#webappchat)WebAppChat

This object represents a chat.

Field

Type

Description

id

Integer

Unique identifier for this chat. This number may have more than 32 significant bits and some programming languages may have difficulty/silent defects in interpreting it. But it has at most 52 significant bits, so a signed 64-bit integer or double-precision float type are safe for storing this identifier.

type

String

Type of chat, can be either “group”, “supergroup” or “channel”

title

String

Title of the chat

username

String

_Optional_. Username of the chat

photo\_url

String

_Optional_. URL of the chat’s photo. The photo can be in .jpeg or .svg formats. Only returned for Mini Apps launched from the attachment menu.

#### [](#validating-data-received-via-the-mini-app)Validating data received via the Mini App

To validate data received via the Mini App, one should send the data from the _Telegram.WebApp.initData_ field to the bot's backend. The data is a query string, which is composed of a series of field-value pairs.

You can verify the integrity of the data received by comparing the received _hash_ parameter with the hexadecimal representation of the [HMAC-SHA-256](https://en.wikipedia.org/wiki/Hash-based_message_authentication_code) signature of the **data-check-string** with the secret key, which is the [HMAC-SHA-256](https://en.wikipedia.org/wiki/Hash-based_message_authentication_code) signature of the [bot's token](/bots/tutorial#obtain-your-bot-token) with the constant string `WebAppData` used as a key.

**Data-check-string** is a chain of all received fields, sorted alphabetically, in the format `key=<value>` with a [line feed](https://en.wikipedia.org/wiki/Newline) character ('\\n', 0x0A) used as separator – e.g., `'auth_date=<auth_date>\nquery_id=<query_id>\nuser=<user>'`.

The full check might look like:

    data_check_string = ...
    secret_key = HMAC_SHA256(<bot_token>, "WebAppData")
    if (hex(HMAC_SHA256(data_check_string, secret_key)) == hash) {
      // data is from Telegram
    }

To prevent the use of outdated data, you can additionally check the _auth\_date_ field, which contains a Unix timestamp of when it was received by the Mini App.

Once validated, the data may be used on your server. Complex data types are represented as JSON-serialized objects.

#### [](#validating-data-for-third-party-use)Validating data for Third-Party Use

NEW If you need to share the data with a third party, they can validate the data without requiring access to your [bot's token](/bots/tutorial#obtain-your-bot-token). Simply provide them with the data from the _Telegram.WebApp.initData_ field and your _bot\_id_.

The integrity of the data can be verified by validating the received _signature_ parameter, which is the base64url-encoded representation of the [Ed25519](https://en.wikipedia.org/wiki/EdDSA) signature of the **data-check-string**. The verification is performed using the public key provided by Telegram.

**Data-check-string** is constructed as follows:  
1\. Prepend the _bot\_id_, followed by `:` and the constant string `WebAppData`.  
2\. Add a [line feed](https://en.wikipedia.org/wiki/Newline) character (`'\n'`, 0x0A).  
3\. Append all received fields (except _hash_ and _signature_), sorted alphabetically, in the format `key=<value>`.  
4\. Separate each key-value pair with a line feed character (`'\n'`, 0x0A).

**Example:**  
`'12345678:WebAppData\nauth_date=<auth_date>\nquery_id=<query_id>\nuser=<user>'`

The verification process might look like this:

    data_check_string = ...
    public_key = "<Telegram_public_key>"
    if (Ed25519_verify(public_key, data_check_string, signature)) {
      // data is valid and originated from Telegram
    }

> Telegram provides the following [Ed25519](https://en.wikipedia.org/wiki/EdDSA) public keys for signature verification:
> 
> **Test environment:** `40055058a4ee38156a06562e52eece92a771bcd8346a8c4615cb7376eddf72ec` (hex)  
> **Production:** `e7bf03a2fa4602af4580703d88dda5bb59f32ed8b02a56c187fe7d34caed242d` (hex)

To prevent the use of outdated data, the third party should additionally validate the _auth\_date_ field. This field contains a Unix timestamp indicating when the data was received by the Mini App.

Once validated, the data may be used. Complex data types are represented as JSON-serialized objects.

#### [](#events-available-for-mini-apps)Events Available for Mini Apps

The Mini App can receive events from the Telegram app, onto which a handler can be attached using the `Telegram.WebApp.onEvent(eventType, eventHandler)` method. Inside `eventHandler` the _this_ object refers to _Telegram.WebApp_, the set of parameters sent to the handler depends on the event type. Below is a list of possible events:

eventType

Description

`activated` NEW

Bot API 8.0+ Occurs when the Mini App becomes active (e.g., opened from minimized state or selected among tabs).  
_eventHandler_ receives no parameters.

`deactivated` NEW

Bot API 8.0+ Occurs when the Mini App becomes inactive (e.g., minimized or moved to an inactive tab).  
_eventHandler_ receives no parameters.

`themeChanged`

Occurs whenever theme settings are changed in the user's Telegram app (including switching to night mode).  
_eventHandler_ receives no parameters, new theme settings and color scheme can be received via _this.themeParams_ and _this.colorScheme_ respectively.

`viewportChanged`

Occurs when the visible section of the Mini App is changed.  
_eventHandler_ receives an object with the single field _isStateStable_. If _isStateStable_ is true, the resizing of the Mini App is finished. If it is false, the resizing is ongoing (the user is expanding or collapsing the Mini App or an animated object is playing). The current value of the visible section’s height is available in _this.viewportHeight_.

`safeAreaChanged` NEW

Bot API 8.0+ Occurs when the device's safe area insets change (e.g., due to orientation change or screen adjustments).  
_eventHandler_ receives no parameters. The current inset values can be accessed via _this.safeAreaInset_.

`contentSafeAreaChanged` NEW

Bot API 8.0+ Occurs when the safe area for content changes (e.g., due to orientation change or screen adjustments).  
_eventHandler_ receives no parameters. The current inset values can be accessed via _this.contentSafeAreaInset_.

`mainButtonClicked`

Occurs when the [main button](#bottombutton) is pressed.  
_eventHandler_ receives no parameters.

`secondaryButtonClicked`

Bot API 7.10+ Occurs when the [secondary button](#bottombutton) is pressed.  
_eventHandler_ receives no parameters.

`backButtonClicked`

Bot API 6.1+ Occurrs when the [back button](#backbutton) is pressed.  
_eventHandler_ receives no parameters.

`settingsButtonClicked`

Bot API 6.1+ Occurrs when the Settings item in context menu is pressed.  
_eventHandler_ receives no parameters.

`invoiceClosed`

Bot API 6.1+ Occurrs when the opened invoice is closed.  
_eventHandler_ receives an object with the two fields: _url_ – invoice link provided and _status_ – one of the invoice statuses:  
\- **paid** – invoice was paid successfully,  
\- **cancelled** – user closed this invoice without paying,  
\- **failed** – user tried to pay, but the payment was failed,  
\- **pending** – the payment is still processing. The bot will receive a service message about a [successful payment](/bots/api#successfulpayment) when the payment is successfully paid.

`popupClosed`

Bot API 6.2+ Occurrs when the opened popup is closed.  
_eventHandler_ receives an object with the single field _button\_id_ – the value of the field _id_ of the pressed button. If no buttons were pressed, the field _button\_id_ will be _null_.

`qrTextReceived`

Bot API 6.4+ Occurs when the QR code scanner catches a code with text data.  
_eventHandler_ receives an object with the single field _data_ containing text data from the QR code.

`scanQrPopupClosed`

Bot API 7.7+ Occurs when the QR code scanner popup is closed by the user.  
_eventHandler_ receives no parameters.

`clipboardTextReceived`

Bot API 6.4+ Occurrs when the `readTextFromClipboard` method is called.  
_eventHandler_ receives an object with the single field _data_ containing text data from the clipboard. If the clipboard contains non-text data, the field _data_ will be an empty string. If the Mini App has no access to the clipboard, the field _data_ will be _null_.

`writeAccessRequested`

Bot API 6.9+ Occurs when the write permission was requested.  
_eventHandler_ receives an object with the single field _status_ containing one of the statuses:  
\- **allowed** – user granted write permission to the bot,  
\- **cancelled** – user declined this request.

`contactRequested`

Bot API 6.9+ Occurrs when the user's phone number was requested.  
_eventHandler_ receives an object with the single field _status_ containing one of the statuses:  
\- **sent** – user shared their phone number with the bot,  
\- **cancelled** – user declined this request.

`biometricManagerUpdated`

Bot API 7.2+ Occurs whenever BiometricManager object is changed.  
_eventHandler_ receives no parameters.

`biometricAuthRequested`

Bot API 7.2+ Occurs whenever biometric authentication was requested.  
_eventHandler_ receives an object with the field _isAuthenticated_ containing a boolean indicating whether the user was authenticated successfully. If _isAuthenticated_ is true, the field _biometricToken_ will contain the biometric token stored in secure storage on the device.

`biometricTokenUpdated`

Bot API 7.2+ Occurs whenever the biometric token was updated.  
_eventHandler_ receives an object with the single field _isUpdated_, containing a boolean indicating whether the token was updated.

`fullscreenChanged` NEW

Bot API 8.0+ Occurs whenever the Mini App enters or exits fullscreen mode.  
_eventHandler_ receives no parameters. The current fullscreen state can be checked via _this.isFullscreen_.

`fullscreenFailed` NEW

Bot API 8.0+ Occurs if a request to enter fullscreen mode fails.  
_eventHandler_ receives an object with the single field _error_, describing the reason for the failure. Possible values for _error_ are:  
**UNSUPPORTED** – Fullscreen mode is not supported on this device or platform.  
**ALREADY\_FULLSCREEN** – The Mini App is already in fullscreen mode.

`homeScreenAdded` NEW

Bot API 8.0+ Occurs when the Mini App is successfully added to the home screen.  
_eventHandler_ receives no parameters.

`homeScreenChecked` NEW

Bot API 8.0+ Occurs after checking the home screen status.  
_eventHandler_ receives an object with the field _status_, which is a string indicating the current home screen status. Possible values for _status_ are:  
\- **unsupported** – the feature is not supported, and it is not possible to add the icon to the home screen,  
\- **unknown** – the feature is supported, and the icon can be added, but it is not possible to determine if the icon has already been added,  
\- **added** – the icon has already been added to the home screen,  
\- **missed** – the icon has not been added to the home screen.

`accelerometerStarted` NEW

Bot API 8.0+ Occurs when accelerometer tracking has started successfully.  
_eventHandler_ receives no parameters.

`accelerometerStopped` NEW

Bot API 8.0+ Occurs when accelerometer tracking has stopped.  
_eventHandler_ receives no parameters.

`accelerometerChanged` NEW

Bot API 8.0+ Occurs with the specified frequency after calling the `start` method, sending the current accelerometer data.  
_eventHandler_ receives no parameters, the current acceleration values can be received via _this.x_, _this.y_ and _this.z_ respectively.

`accelerometerFailed` NEW

Bot API 8.0+ Occurs if a request to start accelerometer tracking fails.  
_eventHandler_ receives an object with the single field _error_, describing the reason for the failure. Possible values for _error_ are:  
**UNSUPPORTED** – Accelerometer tracking is not supported on this device or platform.

`deviceOrientationStarted` NEW

Bot API 8.0+ Occurs when device orientation tracking has started successfully.  
_eventHandler_ receives no parameters.

`deviceOrientationStopped` NEW

Bot API 8.0+ Occurs when device orientation tracking has stopped.  
_eventHandler_ receives no parameters.

`deviceOrientationChanged` NEW

Bot API 8.0+ Occurs with the specified frequency after calling the `start` method, sending the current orientation data.  
_eventHandler_ receives no parameters, the current device orientation values can be received via _this.alpha_, _this.beta_ and _this.gamma_ respectively.

`deviceOrientationFailed` NEW

Bot API 8.0+ Occurs if a request to start device orientation tracking fails.  
_eventHandler_ receives an object with the single field _error_, describing the reason for the failure. Possible values for _error_ are:  
**UNSUPPORTED** – Device orientation tracking is not supported on this device or platform.

`gyroscopeStarted` NEW

Bot API 8.0+ Occurs when gyroscope tracking has started successfully.  
_eventHandler_ receives no parameters.

`gyroscopeStopped` NEW

Bot API 8.0+ Occurs when gyroscope tracking has stopped.  
_eventHandler_ receives no parameters.

`gyroscopeChanged` NEW

Bot API 8.0+ Occurs with the specified frequency after calling the `start` method, sending the current gyroscope data.  
_eventHandler_ receives no parameters, the current rotation rates can be received via _this.x_, _this.y_ and _this.z_ respectively.

`gyroscopeFailed` NEW

Bot API 8.0+ Occurs if a request to start gyroscope tracking fails.  
_eventHandler_ receives an object with the single field _error_, describing the reason for the failure. Possible values for _error_ are:  
**UNSUPPORTED** – Gyroscope tracking is not supported on this device or platform.

`locationManagerUpdated` NEW

Bot API 8.0+ Occurs whenever LocationManager object is changed.  
_eventHandler_ receives no parameters.

`locationRequested` NEW

Bot API 8.0+ Occurs when location data is requested.  
_eventHandler_ receives an object with the single field _locationData_ of type [LocationData](#locationdata), containing the current location information.

`shareMessageSent` NEW

Bot API 8.0+ Occurs when the message is successfully shared by the user.  
_eventHandler_ receives no parameters.

`shareMessageFailed` NEW

Bot API 8.0+ Occurs if sharing the message fails.  
_eventHandler_ receives an object with the single field _error_, describing the reason for the failure. Possible values for _error_ are:  
**UNSUPPORTED** – The feature is not supported by the client.  
**MESSAGE\_EXPIRED** – The message could not be retrieved because it has expired.  
**MESSAGE\_SEND\_FAILED** – An error occurred while attempting to send the message.  
**USER\_DECLINED** – The user closed the dialog without sharing the message.  
**UNKNOWN\_ERROR** – An unknown error occurred.

`emojiStatusSet` NEW

Bot API 8.0+ Occurs when the emoji status is successfully set.  
_eventHandler_ receives no parameters.

`emojiStatusFailed` NEW

Bot API 8.0+ Occurs if setting the emoji status fails.  
_eventHandler_ receives an object with the single field _error_, describing the reason for the failure. Possible values for _error_ are:  
**UNSUPPORTED** – The feature is not supported by the client.  
**SUGGESTED\_EMOJI\_INVALID** – One or more emoji identifiers are invalid.  
**DURATION\_INVALID** – The specified duration is invalid.  
**USER\_DECLINED** – The user closed the dialog without setting a status.  
**SERVER\_ERROR** – A server error occurred when attempting to set the status.  
**UNKNOWN\_ERROR** – An unknown error occurred.

`emojiStatusAccessRequested` NEW

Bot API 8.0+ Occurs when the write permission was requested.  
_eventHandler_ receives an object with the single field _status_ containing one of the statuses:  
\- **allowed** – user granted emoji status permission to the bot,  
\- **cancelled** – user declined this request.

`fileDownloadRequested` NEW

Bot API 8.0+ Occurs when the user responds to the file download request.  
_eventHandler_ receives an object with the single field _status_ containing one of the statuses:  
\- **downloading** – the file download has started,  
\- **cancelled** – user declined this request.

#### [](#adding-bots-to-the-attachment-menu)Adding Bots to the Attachment Menu

Attachment menu integration is currently only available for major advertisers on the [Telegram Ad Platform](https://promote.telegram.org/basics). However, **all bots** can use it in the [test server environment](#using-bots-in-the-test-environment). Talk to Botfather on the test server to [set up the integration](#using-bots-in-the-test-environment).

A special link is used to add bots to the attachment menu:

`https://t.me/botusername?startattach`  
or  
`https://t.me/botusername?startattach=command`

> For example, open this [attachment menu link](https://t.me/durgerkingbot?startattach) for _@DurgerKingBot_, then use the ![Attach](/file/464001085/2/E4hNXSNQimQ.2503/bf6ffcab3cb3afd43d) menu in any **private chat**.

Opening the link prompts the user to add the bot to their attachment menu. If the bot has already been added, the attachment menu will open in the current chat and redirect to the bot there (if the link is opened from a 1-on-1 chat). If a non-empty _startattach_ parameter was included in the link, it will be passed to the Mini App in the _start\_param_ field and in the GET parameter _tgWebAppStartParam_.

The following link formats are also supported:

`https://t.me/username?attach=botusername`  
`https://t.me/username?attach=botusername&startattach=command`  
`https://t.me/+1234567890?attach=botusername`  
`https://t.me/+1234567890?attach=botusername&startattach=command`

These links open the Mini App in the attachment menu in the chat with a specific user. If the bot wasn't already added to the attachment menu, the user will be prompted to do so. If a non-empty _startattach_ parameter was included in the link, it will be passed to the Mini App in the _start\_param_ field and in the GET parameter _tgWebAppStartParam_.

Bot API 6.1+ supports a new link format:

`https://t.me/botusername?startattach&choose=users+bots`  
`https://t.me/botusername?startattach=command&choose=groups+channels`

Opening such a link prompts the user to choose a specific chat and opens the attachment menu in that chat. If the bot wasn't already added to the attachment menu, the user will be prompted to do so. You can specify which types of chats the user will be able to choose from. It can be one or more of the following types: _users_, _bots_, _groups_, _channels_ separated by a `+` sign. If a non-empty _startattach_ parameter was included in the link, it will be passed to the Mini App in the _start\_param_ field and in the GET parameter _tgWebAppStartParam_.

#### [](#additional-data-in-user-agent)Additional Data in User-Agent

When the Mini App is running on Android, additional information is appended to the User-Agent string to provide more context about the app environment. This information includes the app version, device model, Android version, SDK version, and device performance class, formatted as follows:

    Telegram-Android/{app_version} ({manufacturer} {model}; Android {android_version}; SDK {sdk_version}; {performance_class})

where:

*   **{app\_version}** is the version of the Telegram app (e.g., `11.3.3`),
*   **{manufacturer} {model}** represents the device’s manufacturer and model (e.g., `Google sdk_gphone64_arm64`),
*   **{android\_version}** is the Android OS version running on the device (e.g., `14`),
*   **{sdk\_version}** indicates the Android SDK version (e.g., `34`),
*   **{performance\_class}** specifies the device performance class as `LOW`, `AVERAGE`, or `HIGH`, indicating the device's performance capacity.

> **Example**  
> `Mozilla/5.0 (Linux; Android 14; K) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/113.0.5672.136 Mobile Safari/537.36 Telegram-Android/11.3.3 (Google sdk_gphone64_arm64; Android 14; SDK 34; LOW)`

We recommend using this information to optimize your Mini App based on the device's capabilities. For instance, you can adjust animations and visual effects in games on low-performance devices to ensure a smooth experience for all users, regardless of device specifications.

### [](#testing-mini-apps)Testing Mini Apps

#### [](#using-bots-in-the-test-environment)Using bots in the test environment

To log in to the test environment, use either of the following:

*   **iOS:** tap 10 times on the Settings icon > Accounts > Login to another account > Test.
*   **Telegram Desktop:** open ☰ Settings > Shift + Alt + Right click ‘Add Account’ and select ‘Test Server’.
*   **macOS:** click the Settings icon 10 times to open the Debug Menu, ⌘ + click ‘Add Account’ and log in via phone number.

The test environment is completely separate from the main environment, so you will need to create a **new user account** and a **new bot** with @BotFather.

After receiving your bot token, you can send requests to the Bot API in this format:

    https://api.telegram.org/bot<token>/test/METHOD_NAME

> **Note:** When working with the test environment, you may use HTTP links without TLS to test your Mini App.

#### [](#debug-mode-for-mini-apps)Debug Mode for Mini Apps

Use these tools to find app-specific issues in your Mini App:

**iOS**

*   In Telegram tap 10 times on the Settings icon and toggle on _Allow Web View Inspection_.
*   Connect your phone to your computer using a USB cable.
*   Open Safari on your Mac, then go to _Develop > \[Your Device Name\]_ in the menu bar.
*   Launch your Mini App on the iOS device – it will appear in the _Develop_ menu under your device.

**Android**

*   [Enable USB-Debugging](https://developer.chrome.com/docs/devtools/remote-debugging/) on your device.
*   In Telegram Settings, scroll all the way down, press and hold on the **version number** two times.
*   Choose _Enable WebView Debug_ in the Debug Settings.
*   Connect your phone to your computer and open `chrome://inspect/#devices` in Chrome – you will see your Mini App there when you launch it on your phone.

**Telegram Desktop on Windows and Linux**

*   Download and launch the [Beta Version](https://desktop.telegram.org/changelog#beta-version) of Telegram Desktop on **Windows** or **Linux** (not supported on Telegram Desktop for macOS yet).
*   Go to _Settings > Advanced > Experimental settings > Enable webview inspection_.
*   Right click in the WebView and choose _Inspect_.

**Telegram macOS**

*   Download and launch the [Beta Version](https://telegram.org/dl/macos/beta) of Telegram macOS.
*   Quickly click 5 times on the Settings icon to open the debug menu and enable “Debug Mini Apps”.
*   Right click in the Mini App and choose _Inspect Element_.