*   [What features do bots have?](#what-features-do-bots-have "What features do bots have?")
*   [Inputs](#inputs)
    *   [Commands](#commands)
    *   [Keyboards](#keyboards)
    *   [Inline Keyboards](#inline-keyboards)
    *   [Menu Button](#menu-button)
    *   [Global Commands](#global-commands)
*   [Chat and User Selection](#chat-and-user-selection)
*   [Interactions](#interactions)
    *   [Inline Requests](#inline-requests)
    *   [Deep Linking](#deep-linking)
    *   [Attachment Menu](#attachment-menu)
*   [Integration](#integration)
*   [Monetization](#monetization)
    *   [Telegram Stars](#telegram-stars)
    *   [Digital Products](#digital-products)
    *   [Paid Media](#paid-media)
    *   [Subscription Plans](#subscription-plans)
    *   [Revenue Sharing from Telegram Ads](#revenue-sharing-from-telegram-ads)
*   [Mini Apps](#mini-apps)
    *   [Seamless Integration With Telegram](#seamless-integration-with-telegram)
    *   [Mini App Previews](#mini-app-previews)
    *   [Mini App Store](#mini-app-store)
    *   [Home Screen Shortcuts](#home-screen-shortcuts)
    *   [Customizable Loading Screens](#customizable-loading-screens)
    *   [Full-Screen Mode](#full-screen-mode)
    *   [Setting Emoji Status](#setting-emoji-status)
    *   [Sharing Media](#sharing-media)
    *   [Sharing from Mini Apps to Stories](#sharing-from-mini-apps-to-stories)
    *   [Geolocation Access](#geolocation-access)
    *   [Device Motion Tracking](#device-motion-tracking)
    *   [Device Hardware Info](#device-hardware-info)
*   [Bots for Business](#bots-for-business)
*   [Payments](#payments)
*   [Web Login](#web-login)
    *   [Widgets](#widgets)
    *   [Inline Login](#inline-login)
*   [HTML5 Games](#html5-games)
*   [Stickers and Custom Emoji](#stickers-and-custom-emoji)
*   [Language Support](#language-support)
*   [Bot Management](#bot-management)
    *   [Privacy Mode](#privacy-mode)
*   [Testing your bot](#testing-your-bot)
    *   [Dedicated test environment](#dedicated-test-environment)
    *   [Creating a bot in the test environment](#creating-a-bot-in-the-test-environment)
    *   [Status alerts](#status-alerts)
    *   [Local Bot API](#local-bot-api)
*   [BotFather](#botfather)
    *   [Creating a new bot](#creating-a-new-bot)
    *   [About text, description and profile media](#about-text-description-and-profile-media)
    *   [Generating an authentication token](#generating-an-authentication-token)
    *   [Transfer ownership](#transfer-ownership)
    *   [BotFather commands](#botfather-commands)
    *   [Edit bots](#edit-bots)
    *   [Edit settings](#edit-settings)
    *   [Manage games](#manage-games)

*   [Telegram Bots](/bots)
*   [Telegram Bot Features](/bots/features)

Telegram Bot Features
=====================

This page describes individual **bot elements** and **features** in detail. See also:

*   [A General Bot Platform Overview](/bots)
*   [Full API Reference for Developers](/bots/api)

### [](#what-features-do-bots-have)What features do bots have?

*   [**Inputs**](#inputs)
    *   [Text](#inputs)
    *   [Commands](#commands)
    *   [Buttons](#keyboards)
    *   [Chat and User Selection](#chat-and-user-selection)
*   [**Interactions**](#interactions)
    *   [Inline](#inline-requests)
    *   [Deep Linking](#deep-linking)
    *   [Attachment Menu](#attachment-menu)
*   [**Integration**](#integration)
    *   [Mini Apps](#mini-apps)
    *   [Bots for Business](#bots-for-business)
    *   [Payments](#payments)
    *   [Web Login](#web-login)
    *   [HTML5 Games](#html5-games)
    *   [Stickers](#stickers-and-custom-emoji)
*   [**Monetization**](#monetization)
*   [**Language Support**](#language-support)
*   [**Bot Management**](#bot-management)
    *   [Privacy Mode](#privacy-mode)
    *   [Testing Your Bot](#testing-your-bot)
    *   [Status Alerts](#status-alerts)
    *   [Local API](#local-bot-api)
*   [**BotFather, creating and managing bots**](#botfather)

* * *

### [](#inputs)Inputs

Users can send **messages of all types** to bots, including text, files, locations, stickers, voice messages and even [dice](/bots/api#dice) if they're feeling lucky. However, Telegram bots offer many other tools for building flexible interfaces tailored to your specific needs:

*   [Commands](#commands) that are highlighted in messages and can be selected from a list after typing `/`.
*   [Keyboards](#keyboards) that replace the user's keyboard with predefined answer options.
*   [Buttons](#inline-keyboards) that are shown next to messages from the bot.

For even more flexibility, [Web Apps](#web-apps) support 100% custom interfaces with JavaScript.

[![](/file/464001858/11318/ahAJjwERIX8.164875/ce1372cbf73e3ea94e)](/file/464001858/11318/ahAJjwERIX8.164875/ce1372cbf73e3ea94e)

> **Note:** Telegram bots can support [multiple languages](#language-support) that adapt to the users' language settings in the app.

#### [](#commands)Commands

A command is a simple `/keyword` that tells the bot what to do. Telegram apps will:

*   **Highlight** commands in messages. When the user taps a highlighted command, that command is immediately sent again.
*   Suggest a **list of supported commands** with descriptions when the user enters a `/` (for this to work, you need to have provided a list of commands to [@BotFather](https://t.me/botfather) or via the [appropriate API method](/bots/api#setmycommands)). Selecting a command from the list immediately sends it.
*   Show a [menu button](#menu-button) containing all or some of a bot’s commands (which you set via [@BotFather](https://t.me/botfather)).

Commands must always start with the `/` symbol and contain **up to 32 characters**. They can use **Latin letters**, **numbers** and **underscores**, though simple lowercase text is recommended for a cleaner look.

Here are a few examples:

*   /next
*   /cancel
*   /newlocation
*   /newrule

Commands should be **as specific as possible** – for example `/newlocation` or `/newrule` **is better** than a `/new` command that then requires an additional parameter from the user like "_location_“ or ”_rule_".

[![](/file/464001775/10227/HCr0XgSUHrg.119089/c17ff5d34fe528361e)](/file/464001775/10227/HCr0XgSUHrg.119089/c17ff5d34fe528361e)

> We require **all developers** to support several [Global Commands](#global-commands) to make sure Telegram bots offer a consistent and user-friendly experience.

##### [](#command-scopes)Command Scopes

Your bot is able to **show different commands** to different users and groups – you can control this using [scopes](/bots/api#botcommandscope). For example, your bot could show additional commands to group admins or translate the list based on the user’s [language\_code](/bots/api#user).

> Keep in mind that Bot API [updates](/bots/api#update) **will not contain any information** about the scope of a command sent by the user – in fact, they may contain commands that don’t exist at all in your bot. Your backend should **always** verify that received commands are valid and that the user was authorized to use them regardless of scope.
> 
> Bots with privacy mode enabled will only receive commands in groups under special conditions, [see here](#privacy-mode).

#### [](#keyboards)Keyboards

Bots are able to interpret free text input from users, but offering **specific suggestions** is often more intuitive – this is where **custom keyboards** can be extremely useful.

Whenever your bot sends a message, it can **display a special keyboard** with predefined reply options (see [ReplyKeyboardMarkup](/bots/api#replykeyboardmarkup)). Telegram apps that receive the message will display your keyboard to the user. Using any of the buttons will immediately send the respective text. This way you can drastically **simplify** and **streamline** user interaction with your bot.

[![](/file/464001950/1191a/2RwpmgU-swU.123554/b50478c124d5914c23)](/file/464001950/1191a/2RwpmgU-swU.123554/b50478c124d5914c23)

> Check out the [one\_time\_keyboard](/bots/api#replykeyboardmarkup) parameter to automatically hide your bot's keyboard as soon as it's been used.

You can also **customize the text placeholder** in the input field by setting the `input_field_placeholder` parameter.

#### [](#inline-keyboards)Inline Keyboards

There are times when you'd prefer to do things **without sending any messages** to the chat – like when a user is changing settings, toggling options or navigating search results. In such cases, you can use [Inline Keyboards](/bots/api#inlinekeyboardmarkup) that are shown directly below their relevant messages.

Unlike with custom reply keyboards, pressing buttons on inline keyboards **doesn't send messages to the chat**. Instead, inline keyboards support buttons that can work behind the scenes or open different interfaces: [callback buttons](/bots/api#inlinekeyboardbutton), [URL buttons](/bots/api#inlinekeyboardbutton), [switch-to-inline buttons](/bots/api#inlinekeyboardbutton), [game buttons](/bots/api#inlinekeyboardbutton) and [payment buttons](/bots/api#inlinekeyboardbutton).

[![](/file/464001863/110f3/I47qTXAD9Z4.120010/e0ea04f66357b640ec)](/file/464001863/110f3/I47qTXAD9Z4.120010/e0ea04f66357b640ec)

> To provide a **better user experience**, consider [editing your keyboard](/bots/api#editmessagereplymarkup) when the user toggles a setting button or navigates to a new page – this is both **faster** and **smoother** than sending a whole new message and deleting the previous one.

#### [](#menu-button)Menu Button

In all bot chats, a menu button appears near the message field. By default, tapping this button **opens a menu** that can hold some or all of a bot's commands, including a short description for each. Users can then **select a command from the menu** without needing to type it out.

You can set different texts of the menu button and its command descriptions for various **individual users** or **groups of users** – for example, showing translated text based on the user’s language, as explained [here](#commands).

The **menu button** can alternatively be used to launch a [Web App](#web-apps).

#### [](#global-commands)Global Commands

To make basic interactions more uniform, we ask all developers to support a few **basic commands**. Telegram apps will have interface shortcuts for these commands.

*   /start - begins the interaction with the user, like sending an introductory message. This command can also be used to pass additional parameters to the bot (see [Deep Linking](#deep-linking)).
*   /help - returns a help message, like a short text about what your bot can do and a list of commands.
*   /settings - (if applicable) shows the bot's settings for this user and suggests commands to edit them.

Users will see a **Start** button the first time they open a chat with your bot. **Help** and **Settings** links will be available in the menu on the bot's profile page if you add them in [@BotFather](https://t.me/botfather).

### [](#chat-and-user-selection)Chat and User Selection

Bots can present the user with a **friendly** and **intuitive** interface that lists any number of groups, channels or other users according to a custom set of **criteria**. Tapping on a chat will send its identifier to the bot in a service message and seamlessly close the interface.

A group management bot is the **perfect example**: an admin could select a chat the bot should manage, and then select a user it should promote – this would happen without ever typing any text.

Here is a **quick start guide** to use this feature:

*   Pick a set of criteria and store them in a [KeyboardButtonRequestChat](https://core.telegram.org/bots/api#keyboardbuttonrequestchat) object (or [KeyboardButtonRequestUser](https://core.telegram.org/bots/api#keyboardbuttonrequestuser) for users).
*   Create a [KeyboardButton](https://core.telegram.org/bots/api#keyboardbutton) and store the criteria under `request_chat` or `request_user` respectively.
*   Send a [ReplyKeyboardMarkup](https://core.telegram.org/bots/api#replykeyboardmarkup) that contains the button you just created.
*   When the user selects a chat, you'll receive its identifier in a `chat_shared` or `user_shared` service message.

link 

> Keep in mind that the bot may not be able to use the identifier it receives if the corresponding chat or user is not already known or accessible by some other means.

* * *

### [](#interactions)Interactions

In addition to sending commands and messages to the chat with the bot, there are several ways of interacting with them without opening any specific chat or group.

*   [**Inline mode**](#inline-requests) allows sending requests to bots right from the input field – from any chat on Telegram.
*   [**Deep linking**](#deep-linking) allows special links that send certain parameters to the bot when opened.
*   [**Attachment menu**](#attachment-menu) integration makes it possible to use bots from the attachment menu in chats.

#### [](#inline-requests)Inline Requests

Users can interact with your bot via **inline queries** straight from the message field **in any chat**. All they need to do is start a message with your bot's _@username_ and enter a keyword.

Having received the query, your bot can return some results. As soon as the user selects one, it is sent to the **relevant chat**. This way, people can request and send content from your bot in any of their chats, groups or channels.

Remember that inline functionality has to be enabled via [@BotFather](https://t.me/botfather), or your bot will not receive inline [Updates](/bots/api#update).

[![](/file/464001466/10e4a/r4FKyQ7gw5g.134366/f2606a53d683374703)](/file/464001466/10e4a/r4FKyQ7gw5g.134366/f2606a53d683374703)

> Examples of inline bots include [@gif](https://gif.t.me), [@bing](https://bing.t.me) and [@wiki](https://wiki.t.me). [Web App](#web-apps) bots can also be used inline – try typing [@durgerkingbot](https://durgerkingbot.t.me) in any chat.

#### [](#deep-linking)Deep Linking

Telegram bots have a deep linking mechanism that allows **additional parameters** to be passed to the bot on startup. It could be a command that launches the bot – or an authentication token to connect the user's Telegram account to their account on another platform.

Each bot has a link that **opens a conversation** with it in Telegram – `https://t.me/<bot_username>`. Parameters can be added directly to this link to let your bot work with additional information on the fly, without any user input.

> A-Z, a-z, 0-9, \_ and - are allowed. We recommend using base64url to encode parameters with binary and other types of content. The parameter can be up to 64 characters long.

**Private Chats**  
In private chats, you can use the `start` parameter to automatically pass any value to your bot whenever a user presses the link. For example, you could use:

    https://t.me/your_bot?start=airplane

When someone opens a chat with your bot via this link, you will receive:

    /start airplane

**Groups**  
In groups, you can add the parameter `startgroup` to this link. For example:

    https://t.me/your_bot?startgroup=spaceship

Following a link with this parameter prompts the user to select a group to add the bot to – the resulting update will contain text in the form:

    /start@your_bot spaceship

> [Web Apps](#web-apps) also support deep linking, for more information check out our [dedicated guide](/bots/webapps#adding-bots-to-the-attachment-menu).

#### [](#attachment-menu)Attachment Menu

Certain bots can be added directly to a user’s **attachment menu** – giving them easy access to the bot in any chat. Currently, this option is restricted to certain [approved bots](/bots/webapps#launching-web-apps-from-the-attachment-menu), but may be expanded later.

> Try adding [@DurgerKingBot](https://t.me/durgerkingbot?startattach) to your attachment menu.

* * *

### [](#integration)Integration

There are various ways of further integrating bots with Telegram and other services.

*   Use [Web Apps](#web-apps) to replace any website.
*   Build tools and integrate [business services](#bots-for-business).
*   Accept [Payments](#payments) via third-party payment providers that support integration with Bots and Mini Apps.
*   Connect to Telegram using the [Web Login](#web-login) functionality.
*   Create gaming bots by integrating [HTML5 Games](#html5-games).
*   Help users create and manage [Telegram Stickers](#stickers-and-custom-emoji).

### [](#monetization)Monetization

Telegram offers a **robust ecosystem** of monetization features, allowing any bot to support its development with **multiple revenue streams**.

#### [](#telegram-stars)Telegram Stars

Telegram Stars power all digital transactions between bots and users. Users can acquire Stars through in-app purchases via Apple and Google or via [@PremiumBot](https://t.me/premiumbot).

Bots can use the Stars they receive to [increase message limits](https://telegram.org/blog/dynamic-video-quality-and-more#increased-message-limits-for-bots), [send gifts](https://core.telegram.org/bots/api#sendgift) to users or [accept rewards](https://telegram.org/blog/monetization-for-channels) in Toncoin.

[![](/file/400780400296/3/gxdJYNSAgsg.335683/d6be0165da6f79d605)](/file/400780400296/3/gxdJYNSAgsg.335683/d6be0165da6f79d605)

#### [](#digital-products)Digital Products

Services can use their bot to sell **digital goods** and **services** – like online courses, commissioned artwork and **items in games**.

#### [](#paid-media)Paid Media

Bots can post **paid photos** and **videos** – and users are only allowed to view the media after paying to unlock it. This functionality is available to **all bots** – including **bot admins** in channels and bots managing [Telegram Business](https://core.telegram.org/bots/features#bots-for-business) accounts.

#### [](#subscription-plans)Subscription Plans

Developers are able to **offer paid subscriptions** to their bot – adding **multiple tiers** of content and features tailored to their audience.

#### [](#revenue-sharing-from-telegram-ads)Revenue Sharing from Telegram Ads

Developers can participate in [revenue sharing](https://telegram.org/blog/monetization-for-channels) from [Telegram Ads](https://telegram.org/blog/monetization-for-channels#ton-based-ads) – receiving **50%** of the revenue from ads that appear in the chat with their bot.

### [](#mini-apps)Mini Apps

[Mini Apps](webapps) allow developers to create infinitely flexible interfaces that can be launched right inside Telegram – integrating seamlessly with the app and replacing **any website**.

If your bot is a mini app, you can add a prominent **Launch app** button as well as demo videos and screenshots to the bot’s profile. To do this, go to [@BotFather](https://t.me/botfather) and set up your bot's [Main Mini App](webapps#launching-the-main-mini-app).

> Mini apps are covered in detail in our [dedicated guide](webapps) – you should read it carefully to learn the wide variety of features they can offer.

If you develop a **mini app**, be sure to follow our [design guidelines](webapps#design-guidelines) – you'll want your custom interface to **seamlessly integrate** into the app to provide users the best possible experience.

#### [](#seamless-integration-with-telegram)Seamless Integration With Telegram

Mini apps integrate **seamlessly** with Telegram – from receiving detailed [theme settings](webapps#themeparams) to using native dialogs for reading [QR codes](webapps#initializing-mini-apps), controlling [biometrics](webapps#biometricmanager), sharing media [directly to stories](webapps#initializing-mini-apps) and more.

When opened from a [direct link](webapps#direct-link-mini-apps) in a group, mini apps can also use the `chat_instance` parameter to track of the current context, supporting **shared usage** by multiple chat members – to create live whiteboards, group orders, multiplayer games and much more.

#### [](#mini-app-previews)Mini App Previews

Developers can **upload screenshots** and **video demos** of their mini app right from the bot's **profile page** – giving users an overview of the app's features and functionality. These media previews will be shown to any user who **views your app** – like in the [Mini App Store](#mini-app-store) or via Search.

[![](/file/400780400954/6/9rSb8AM77Ss.158225/1c635ef877be7a6747)](/file/400780400954/6/9rSb8AM77Ss.158225/1c635ef877be7a6747)

> Previews support **multiple languages** – so you can upload **translated versions** of your previews that will be shown to users based on their **app language**.

#### [](#mini-app-store)Mini App Store

More than **500 million** out of Telegram's [950](https://t.me/durov/337) million users interact with mini apps every month. Successful mini apps have the chance to be **highlighted** in the Telegram Mini App Store – appearing for all users in the _'Apps'_ tab of Search.

Featured mini apps are chosen based on how they **enrich the Telegram ecosystem**. To increase the chances of being featured, you must **enable** the [Main Mini App](https://core.telegram.org/bots/webapps#launching-the-main-mini-app) in [@BotFather](https://t.me/botfather), **upload** high-quality media demos showcasing your app to your bot's profile and **accept payments** in [Telegram Stars](https://telegram.org/blog/telegram-stars).

> Check out our documentation to learn more about [enabling Main Mini Apps](https://core.telegram.org/bots/webapps#launching-the-main-mini-app) and [accepting payments](https://core.telegram.org/bots/payments-stars) in Stars.

#### [](#home-screen-shortcuts)Home Screen Shortcuts

Users can place **direct shortcuts** to specific mini apps on the **home screen** of their devices – accessing their favorite games and services in **one tap**.

#### [](#customizable-loading-screens)Customizable Loading Screens

The loading screen of mini apps can be **customized** in [@Botfather](https://t.me/botfather) – where developers can add **their own icon** and set **specific colors** for both light and dark themes.

> To customize your loading screen, go to [@Botfather](https://t.me/botfather) > `/mybots` > Select bot > _Bot Settings_ > _Configure Mini App_ > _Configure Splash Screen_. You can tap on _Open Splash Screen Preview_ to see the final result.

#### [](#full-screen-mode)Full-Screen Mode

Mini apps are able to use the **entire screen** in portrait or **landscape orientation** – allowing for **immersive games** and media with **expanded gestures** and interfaces.

#### [](#setting-emoji-status)Setting Emoji Status

Users can **set an emoji status** inside mini apps or give an app permission to **update it automatically**.

Developers can also integrate APIs from **other services** or request [geolocation access](https://core.telegram.org/bots/features#geolocation-access) – instantly changing a user's status when they start a game ![🎮](//telegram.org/img/emoji/40/F09F8EAE.png) or leave the office ![💼](//telegram.org/img/emoji/40/F09F92BC.png).

#### [](#sharing-media)Sharing Media

Media generated in mini apps can be shared in **any chat** – letting users effortlessly send **referral codes** and **custom images** to contacts, groups and channels. Alternatively, users can [download it](https://core.telegram.org/bots/webapps#downloadfileparams) with a native popup.

#### [](#sharing-from-mini-apps-to-stories)Sharing from Mini Apps to Stories

Any media created by the mini app, like whiteboard snapshots, leaderboards and AI-generated videos can be opened with the native story editor via the [shareToStory](webapps#initializing-mini-apps) method – for users to share as a [Telegram Story](https://telegram.org/tour/stories) right from the mini app.

> Mini apps also receive a number of **events**, allowing them to **instantly react** to actions by the user. You can learn more about which events are available [here](webapps#events-available-for-mini-apps).

#### [](#geolocation-access)Geolocation Access

Mini apps are able to receive **location permissions** from users – giving developers the ability to make **location-based games** and **interactive maps** for events.

#### [](#device-motion-tracking)Device Motion Tracking

Mini Apps can request [acceleration](https://core.telegram.org/bots/webapps#accelerometer), [orientation](https://core.telegram.org/bots/webapps#deviceorientation) and [rotation](https://core.telegram.org/bots/webapps#gyroscope) data from devices in real time – unlocking support for **motion controls** and **VR experiences**.

#### [](#device-hardware-info)Device Hardware Info

A user's device can send [basic hardware info](https://core.telegram.org/bots/webapps#additional-data-in-user-agent) to mini apps, such as its processing power and memory capacity. Mini apps can then use this to **optimize graphics** and automatically **adjust settings** for the smoothest experience.

### [](#bots-for-business)Bots for Business

Bots can enable **Business Mode**, allowing [Telegram Business](https://telegram.org/blog/telegram-business) subscribers to connect them to their account – streamlining and automating private chat management and interactions with their clients.

The **account owner** can specify which chats your bot can access – within those chats, the bot will receive all updates normally supported by the [Bot API](https://core.telegram.org/bots/api), except messages sent by itself and other bots. Depending on the business connection settings, your bot may also be able to **send messages** and do other actions on behalf of the account owner in chats that were active in the last 24h.

Here is a quick start guide to integrate your bot with Telegram Business:

*   Enable **Business Mode** for your bot in [@BotFather](https://t.me/botfather).
*   Handle incoming [BusinessConnection](https://core.telegram.org/bots/api#businessconnection) updates, signaling that a user has _established_, _edited_ or _ended_ a Business Connection with your bot.
*   Process business messages by handling `business_message`, `edited_business_message` and `deleted_business_messages` updates.
*   Check your bot’s write permissions via `can_reply` in the latest [BusinessConnection](https://core.telegram.org/bots#businessconnection) update.
*   If allowed to, use the `business_connection_id` field in [sendMessage](https://core.telegram.org/bots/api#sendmessage), [sendChatAction](https://core.telegram.org/bots/api#sendchataction) and other send methods to communicate on behalf of the Business user.

Users who **connect your bot** to their account will see a **quick action bar** at the top of each managed chat – tapping on “Manage Bot” will redirect them to your bot, which will receive a deep link message in the format `/start bizChat<user_chat_id>`.

> Please keep in mind that operating bots on Telegram is subject to the [Telegram Bot Developer Terms of Service](https://telegram.org/tos/bot-developers). Specifically, for Telegram Business, make sure you have read and understood [Section 5.4](https://telegram.org/tos/bot-developers#5-4-telegram-business).

### [](#payments)Payments

> If your bot or mini app sells **digital goods and services**, be sure to carry out the payment in [Telegram Stars](https://telegram.org/blog/telegram-stars) by specifying `XTR` as currency. In compliance with third-party store policies, Telegram does not support the sale of digital goods and services using other currencies.

Telegram bots can accept payments with a sleek, streamlined interface that collects all necessary data from the user. Telegram **doesn't collect** any payment data – like the user's credit card information – and sends it directly to one of the supported third-party [payment providers](payments).

Here is a **quick start guide** to implement payments:

*   Pick a [provider](payments) and obtain the [proper token](payments#getting-a-token) as well as a **test token** from the "**Stripe TEST MODE**" provider.
*   Implement payments via the [appropriate API methods](/bots/api#payments).
*   Test your implementation by using your **test token** along with a [test credit card](https://stripe.com/docs/testing#cards).

Then, to issue an **invoice** and process the order flow:

*   [Send an invoice](/bots/api#sendinvoice) to the user for the goods or services you are offering.
*   Validate the order and accept the checkout via [answerPreCheckoutQuery](/bots/api#answerprecheckoutquery).
*   Confirm the payment by checking for a [successful payment service message](/bots/api#successfulpayment).
*   Ship the goods or provide the services.

For more details, feel free to check out our full exhaustive **guides** for selling goods and services on Telegram – they include live checklists, parameters and in-depth method descriptions:

*   [Guide for digital goods and services](/bots/payments-stars)
*   [Guide for physical goods and services](/bots/payments)

[![](/file/464001393/101fc/SB_bFCLR0tg.130549/7ecf91aaa44737e8cb)](/file/464001393/101fc/SB_bFCLR0tg.130549/7ecf91aaa44737e8cb)

> Telegram does not directly process the payments, does not store data about orders and does not collect any fees. Invoices are forwarded directly to the third-party payment provider.  
> For this reason, disputes must be solved between the user, the bot developer and the payment provider. You can read more about this in the [Privacy Policy](https://telegram.org/privacy#7-third-party-payment-services).

### [](#web-login)Web Login

Telegram offers a **flexible**, **lightweight** and **free** framework to authenticate users on any website and app. This can be used to bridge your platform with Telegram, providing a smooth experience to your users. You can also freely rely on this framework to implement a **fast** and **signup-free** login on your site, regardless of its connection to Telegram.

#### [](#widgets)Widgets

The Telegram login widget is a **simple and secure way to authorize users** on your website.

1.  Choose a bot – ideally its name and profile pic **should match** the website title and logo.
2.  Use the `/setdomain` command in [@BotFather](https://t.me/botfather) to pair the bot with your website domain.
3.  Configure your widget using [our dedicated tool](/widgets/login#widget-configuration) and embed it on your website.

#### [](#inline-login)Inline Login

When users open your website via an **inline button**, you can use the [login\_url](/bots/api#loginurl) parameter as an alternative to login widgets. This way, you'll be able to [seamlessly authorize](https://telegram.org/blog/privacy-discussions-web-bots#meet-seamless-web-bots) them on your website or app before the page even loads.

[![](/file/464001287/105ea/23bO4ntH4tc.43741/c9624e36c3462b6540)](/file/464001287/105ea/23bO4ntH4tc.43741/c9624e36c3462b6540)

> Make sure to review our [guide](/widgets/login#checking-authorization) on authenticating the received data as well as our [sample code](https://gist.github.com/anonymous/6516521b1fb3b464534fbc30ea3573c2).

### [](#html5-games)HTML5 Games

Bots can serve as **standalone gaming platforms** – with our [HTML5 Gaming API](/bots/api#games) you can develop multiplayer or single-player games and let your users have fun comparing **ranks**, **scores** and much more.

To get started, follow these simple steps:

*   Send the `/newgame` command to [@BotFather](https://t.me/botfather)
*   Provide a **description text**, an **image** or an **optional gif** to showcase its gameplay
*   Send the game to users via the [sendGame](/bots/api#sendgame) method or via an [inline query](/bots/api#inlinequeryresultgame)
*   When someone wants to play, you'll receive the appropriate `game_short_name` in a [CallbackQuery](/bots/api#callbackquery)
*   To launch the game, provide the **HTML5 Game URL** as the `url` param of [answerCallbackQuery](/bots/api#answercallbackquery)

Then, to handle **highscores**:

*   Use [setGameScore](/bots/api#setgamescore) to post high scores in the chat with the game
*   Use [getGameHighScores](/bots/api#getgamehighscores) to get in-game high score tables

You can also **embed a share button** within your game, play around with **custom inline buttons**, **URL parameters** and much more. To get a better idea, make sure to check out:

*   [HTML5 Games Manual](/bots/games)
*   [HTML5 Games Bot API Docs](/bots/api#games)

[![](/file/464001558/11b92/y_Fu9QQWtj0.141959/dc9db48f66800bf271 "Games")](/file/464001558/11b92/y_Fu9QQWtj0.141959/dc9db48f66800bf271)

> Check out [@GameBot](https://t.me/gamebot) and [@gamee](https://t.me/gamee) for examples of what you can do using our Gaming Platform.

### [](#stickers-and-custom-emoji)Stickers and Custom Emoji

[Stickers](https://core.telegram.org/stickers) and [Custom Emoji](https://telegram.org/blog/custom-emoji) are a distinctive Telegram feature used by millions of users to share artwork every day. Stickers and custom emoji take many forms – ranging from **basic images** to smooth **vector animations** and high-detail **.WEBM videos**.

All these formats are supported by our [Bot API](api#stickers), which allows bots to **create**, **edit**, **delete** and **share** new artwork packs on the fly. Telegram's [Import API](https://core.telegram.org/import-stickers) lets users **migrate packs** from other platforms and sticker apps.

**Creating a new pack**  
To create a **new pack**, simply:

*   **Prepare** your artwork following our [technical requirements](https://core.telegram.org/stickers).
*   **Create** a new sticker pack via [createStickerSet](api#createnewstickerset). Set `sticker_type` to _regular_ to create a sticker pack or to _custom emoji_ to create a pack of custom emoji. Attach the [files](api#file) you wish to include in the pack as an array of [InputSticker](https://core.telegram.org/bots#inputsticker)
*   You can use [addStickerToSet](api#addstickertoset) to add stickers or emoji later on.

**Additional features**  
Regular stickers and custom emoji support **keywords** that users can type to quickly find the respective artwork – this can be useful when a sticker doesn't have obvious ties to a specific emoji. You can use the `keywords` parameter in [InputSticker](https://core.telegram.org/bots#inputsticker) to specify them.

Custom emoji additionally support **adaptive colors** – they will always match the current context (e.g., white on photos, accent color when used as status, etc.); to enable this feature, use the `needs_repainting` parameter in [createStickerSet](api#createnewstickerset).

Once you're done creating and sharing your artwork, don't forget to check out our [remaining sticker methods](api#stickers) to find out how to [edit](api#setstickersetthumb), [delete](api#deletestickerfromset) and even [reorder](api#setstickerpositioninset) your pack.

> Note that these methods will only work on packs **created by the bot that is calling them**.

### [](#language-support)Language Support

Bots can tailor their interfaces to **support multiple languages** – updating inputs and information on the fly. A user’s [language\_code](/bots/api#user) is included in every relevant [update](/bots/api#update) as an [IETF language tag](https://en.wikipedia.org/wiki/IETF_language_tag), allowing bots to adapt accordingly.

We recommend that you follow our guidelines to provide **the best user experience**.

*   Your interfaces, texts and [inline results](/bots/api#answerinlinequery) should adapt seamlessly to the _language\_code_, without user intervention.
*   Connected [WebApps](/bots/webapps) will receive the user's _language\_code_ – your HTML page should account for it.
*   [HTML5 Games](/bots/games) can obtain language information if you specify it as a [URL parameter](/bots/games#using-url-parameters). You can generate this parameter from the _language\_code_ field in the [User](/bots/api#user) object served with the initial game [CallbackQuery](/bots/api#callbackquery).
*   The bot's **Name**, **Description** and **About text** can be natively localized with the respective [methods](https://core.telegram.org/bots/api#setmydescription).
*   Command lists can also be specified for individual languages – more on this [here](#commands).

> The _language\_code_ is an **optional field** – it could be empty.  
> If you target the general public, your code should always fall back to either the last recorded language tag or English (in this order) when the field is missing for a specific user.

* * *

### [](#bot-management)Bot Management

#### [](#privacy-mode)Privacy Mode

Bots are frequently added to groups to perform basic tasks or assist moderators – like automatically posting company announcements or even celebrating birthdays. By default, **all bots** added to groups run in Privacy Mode and only see relevant messages and commands:

*   Commands explicitly meant for them (e.g., `/command@this_bot`).
*   General commands (e.g. `/start`) if the bot was the last bot to send a message to the group.
*   Inline messages sent [via](/bots/api#inline-mode) the bot.
*   Replies to any messages implicitly or explicitly meant for this bot.

All bots will also receive, **regardless of privacy mode**:

*   All service messages.
*   All messages from private chats.
*   All messages from channels where they are a member.

Privacy mode is **enabled by default** for all bots, except bots that were added to a group as admins (bot admins always receive **all messages**). It can be disabled so that the bot receives all messages like an ordinary user (the bot will need to be re-added to the group for this change to take effect). We only recommend doing this in cases where it is **absolutely necessary** for your bot to work. In most cases, using the force reply option for the bot's messages should be more than enough.

[![](/file/464001338/107af/JdbERa0BATg.62371/28977e9a96aed3860a "Privacy Mode")](/file/464001338/107af/JdbERa0BATg.62371/28977e9a96aed3860a)

> This mode not only increases user privacy, but also makes the bot more efficient by reducing the number of inputs it needs to process. Users can always see a bot’s current privacy setting in the list of group members.

### [](#testing-your-bot)Testing your bot

You can quickly test your bot **without interfering** with its users by simply running another instance of your code on a different bot account. To do so, create a _new bot_ via [@BotFather](https://t.me/botfather), obtain its token and use it in the testing instance of your code.

All further testing and debugging can happen privately on the new bot, without affecting the original instance.

> If you need to share file references across bots, note that the `file_id` field is tied to a single bot id, so your test instance cannot use a shared `file_id` database to quickly send media – files must be individually reuploaded.

#### [](#dedicated-test-environment)Dedicated test environment

Telegram also offers a dedicated **test environment** suitable for more advanced testing. Bots and users in this environment generally have more flexible restrictions – for example:

*   When working with the test environment, you may use HTTP links without TLS to test your [Web Apps](https://core.telegram.org/bots/features#web-apps) or [Web Login](https://core.telegram.org/bots/features#web-login).

> **Flood limits** are not raised in the test environment, and may at times be stricter. To minimize how this impacts your bot, you should make sure that it handles errors with retry policies and does not depend on hardcoded limit values.

#### [](#creating-a-bot-in-the-test-environment)Creating a bot in the test environment

The test environment is **completely separate** from the main environment, so you will need to create a new user account and a new bot with [@BotFather](https://t.me/botfather).

To create an account and log in, use either of the following:

*   **iOS**: tap 10 times on the Settings icon > Accounts > Login to another account > Test.
*   **Telegram Desktop**: open ☰ Settings > Shift + Alt + Right click 'Add Account' and select 'Test Server'.
*   **macOS**: click the Settings icon 10 times to open the Debug Menu, ⌘ + click 'Add Account' and log in via phone number.

After logging in, simply [create a new bot](#creating-a-new-bot) following the standard procedure and send your requests to the Test Bot API in this format:

    https://api.telegram.org/bot<token>/test/METHOD_NAME

> When working with the test environment, you may use HTTP links without TLS in the `url` field of both [LoginUrl](/bots/api#loginurl) and [WebAppInfo](/bots/api#webappinfo).

#### [](#status-alerts)Status alerts

Millions choose Telegram for its speed. To best benefit users, your bot also **needs to be responsive**. In order to help developers keep their bots in shape, [@BotFather](https://t.me/botfather) will send **status alerts** if it sees something is wrong.

We check the number of replies and the _request/response_ conversion rate for popular bots (~300 requests per minute, this value may change in the future). If your bot returns an **abnormally low number**, you will receive a notification from [@BotFather](https://t.me/botfather).

##### [](#responding-to-alerts)Responding to alerts

By default, **you will only get one alert per bot per hour**.

Each alert has the following buttons:

*   **Fixed** - Use this if you found an issue with your bot and fixed it. If you press the fix button, we will resume sending alerts in the regular way so that you can see if your fix worked within 5-10 minutes instead of having to wait for an hour.
*   **Support** - Use this to open a chat with [@BotSupport](https://t.me/botsupport) if you don't see any issues with your bot or if you think the problem is on our side.
*   **Mute for 8h/1w** - Use this if you can't fix your bot at the moment. This will disable all alerts for the bot in question for the specified period of time. **We do not recommend** using this option since your users may migrate to a more stable bot. You can unmute alerts in your bot's settings via [@BotFather](https://t.me/botfather).

##### [](#monitored-issues)Monitored issues

We currently notify you about the following issues:

*   **Too few private messages are sent.** Value: **{value}** - Your bot is sending far fewer messages than it did in previous weeks. This is useful for newsletter-style bots that send messages without prompts from users. The larger the value, the more significant the difference.
    
*   **Too few replies to incoming private messages**. Conversion rate: **{value}** - Your bot is not replying to all messages that are being sent to it (the request/response conversion rate for your bot was too low for at least two of the last three 5-minute periods).
    

> To provide a good user experience, please respond to all messages that are sent to your bot. Respond to message updates by calling send… methods (e.g. [sendMessage](/bots/api#sendmessage)).

*   **Too few answers to inline queries**. Conversion rate: **{value}** - Your bot is not replying to all inline queries that are being sent to it, calculated in the same way as above. Respond to `inline_query` updates by calling [answerInlineQuery](/bots/api#answerinlinequery).

*   **Too few answers to callback queries**. Conversion rate: **{value}**
*   **Too few answers to callback game queries**. Conversion rate: **{value}** - Your bot is not replying to all callback queries that are being sent to it (with or without games), calculated in the same way as above. Respond to `callback_query` updates by calling [answerCallbackQuery](/bots/api#answercallbackquery).

#### [](#local-bot-api)Local Bot API

You can host and work with **your own instance** of our open-source [Bot API](/bots/api).  
The **source code** is available [here](https://github.com/tdlib/telegram-bot-api), along with a quick [installation guide](https://github.com/tdlib/telegram-bot-api#installation).

After **installing the server**, remember to use the [logOut](/bots/api#logout) method before **redirecting requests** to your new local API URL.

> Your local instance runs on port `8081` by default and will only accept HTTP requests, so a TLS termination proxy has to be used to handle remote HTTPS requests.

By hosting our API locally you'll gain access to **some upgrades**, including:

API

Max File Download

Max File Upload

WHook URL

WHook Port

WHook Max Connections

[Official](/bots/api#making-requests)

20MB

50MB

HTTPS

443,80,88,8443

1-100

[Local](/bots/api#using-a-local-bot-api-server)

Unlimited

2000MB

HTTP

Any port

1-100000

> You can find an exhaustive list [here](/bots/api#using-a-local-bot-api-server).  
> All limits may be subject to change in the future, so make sure to follow [@BotNews](https://t.me/botnews).

* * *

### [](#botfather)BotFather

Below is a detailed guide to using [@BotFather](https://t.me/botfather), Telegram’s tool for **creating** and **managing** bots.

#### [](#creating-a-new-bot)Creating a new bot

Use the `/newbot` command to create a new bot. [@BotFather](https://t.me/botfather) will ask you for a name and username, then generate an authentication token for your new bot.

*   The **name** of your bot is displayed in contact details and elsewhere.
    
*   The **username** is a short name, used in search, mentions and t.me links. Usernames are 5-32 characters long and not case sensitive – but may only include Latin characters, numbers, and underscores. Your bot's username must end in 'bot’, like 'tetris\_bot' or 'TetrisBot'.
    
*   The **token** is a string, like `110201543:AAHdqTcvCH1vGWJxfSeofSAs0K5PALDsaw`, which is required to authorize the bot and send requests to the Bot API. Keep your token secure and store it safely, it can be used by anyone to control your bot.
    

> Unlike the bot’s name, the username cannot be changed later – so choose it carefully.  
> When sending a request to api.telegram.org, remember to prefix the word ‘bot’ to your token.

#### [](#about-text-description-and-profile-media)About text, description and profile media

When new users open your bot, they will be met with a helpful description in a box titled “What can this bot do?”.

Properly [setting this field](#edit-bots) in [@BotFather](https://t.me/botfather) allows everyone to immediately get an idea of what your bot can do – your description should be **brief**, **to the point** and **on topic**.

> You can also add a photo or video to this field with `Edit Description Picture` in [@BotFather](https://t.me/botfather).

Additionally, just like normal users, bots also come with a **short bio** available on their profile. If you didn't specify this field while first creating your bot, you can set it at any time with the `/setabouttext` command in [@BotFather](https://t.me/botfather). Users can interact with many bots and they won't have access to their description after starting them – having a quick reminder of the bot's purpose can be very useful.

> Note that both the **Description** and the **About text** can be [natively localized](https://core.telegram.org/bots/api#setmydescription) – each user will automatically see the correct translation for their language.

Bots can also have a **profile picture** – you should pick something unique and original so that users can find it in their chat list at a glance.

> Starting from April 21, 2023 ([Telegram 9.6](https://telegram.org/blog/shareable-folders-custom-wallpapers)), you can edit your bot directly from its profile page – including setting a custom **profile video**.

#### [](#generating-an-authentication-token)Generating an authentication token

If your existing token is **compromised** or **you lost it** for some reason, use the `/token` command to generate a new one.

#### [](#transfer-ownership)Transfer ownership

You can transfer ownership of your bot **to another user**.  
To do this, send `/mybots`, select your bot, then _transfer ownership_.  
You can only transfer a bot to users who have interacted with it at least once.

> Transferring ownership will give full control of the bot to another user – they will be able to access the bot’s messages and even delete it. The transfer is permanent, so please consider it carefully.

#### [](#botfather-commands)BotFather commands

The remaining commands are pretty self-explanatory:

*   /mybots – returns a list of your bots with handy controls to edit their settings.
*   /mygames – does the same for your games.

#### [](#edit-bots)Edit bots

To edit your bot, you have two options.

You can use the available commands:

*   /setname – change your bot's **name**.
*   /setdescription – change the bot's **description** (short text up to 512 characters). Users will see this text at the beginning of the conversation with the bot, titled '_What can this bot do?_'.
*   /setabouttext – change the bot's **about info**, a shorter text up to 120 characters. Users will see this text on the bot's profile page. When they share your bot with someone, this text is sent together with the link.
*   /setuserpic – change the bot's **profile picture**.
*   /setcommands – change the list of **commands** supported by your bot. Users will see these commands as suggestions when they type `/` in the chat with your bot. See [commands](#commands) for more info.
*   /setdomain – link a **website domain** to your bot. See the [login widget](#login-widget) section.
*   /deletebot – delete your bot and **free its username**. Cannot be undone.

Or you can use the `/mybots` command, tap on your bot and use the modern inline interface to edit it.

> Starting from April 21, 2023 ([Telegram 9.6](https://telegram.org/blog/shareable-folders-custom-wallpapers)), you can edit your bot's public-facing info directly from its profile page – including setting a custom **profile video**.

#### [](#edit-settings)Edit settings

*   /setinline – toggle **inline mode** for your bot.
*   /setinlinegeo – request **location data** to provide location-based inline results.
*   /setjoingroups – toggle whether your bot can be **added to groups** or not. All bots must be able to process direct messages, but if your bot was not designed to work in groups, you can disable this.
*   /setinlinefeedback – toggle whether the API should **send updates about the results** chosen by users. See an in-depth explanation [here](/bots/inline#collecting-feedback).
*   /setprivacy – set which messages your bot will receive when added to a group. See [privacy-mode](#privacy-mode) for more info.

#### [](#manage-games)Manage games

*   /newgame – create a new game.
*   /listgames – see a list of your games.
*   /editgame – edit a game.
*   /deletegame – delete an existing game.

> Please note that it may take a few minutes for changes to take effect.

* * *

With this information, you are ready to proceed to our [Full API Reference for Developers](/bots/api).

*   If you have any questions, check out our [Bot FAQ](/bots/faq).
*   If you're experiencing issues with our API, please contact [@BotSupport](https://t.me/botsupport) on Telegram.