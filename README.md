﻿# Telegram Bot Framework for .NET Core

[![Build Status](https://travis-ci.org/pouladpld/Telegram.Bot.Framework.svg?branch=master)](https://travis-ci.org/pouladpld/Telegram.Bot.Framework)
[![NuGet](https://img.shields.io/nuget/v/Telegram.Bot.Framework.svg)](https://www.nuget.org/packages/Telegram.Bot.Framework)

<img src="./docs/icon.png" alt="Telegram Bot Framework Logo" width=200 height=200 />

Simple framework for building Telegram bots. Ideal for running multiple chat bots inside a single ASP.NET Core app.

See an example in action:

Click [here to open it in Telegram](https://t.me/sample_echoer_bot) or search for `@sample_echoer_bot` there.

[Sample - Echoer bot](https://t.me/sample_echoer_bot)

## Screenshots

--> Add here <--

## Getting Started

### Requirements

- Visual Studio 2017 or [.NET Core 1.1](https://www.microsoft.com/net/download/core#/current).

> Talk to **[BotFather](http://t.me/botfather)** to get a token for your Telegram bot.

### Implementation

Getting your bot to work is very easy with this framework. Following code snippets show that:

#### Bot Type

```c#
class EchoerBot : BotBase<EchoerBot>
{
    ...
}
```

#### Message Handler

```c#
class TextMessageEchoer : UpdateHandlerBase
{
    public override bool CanHandleUpdate(IBot bot, Update update)
    {
        // Can handle it only if the update is a text message
    }

    public override async Task<UpdateHandlingResult> HandleUpdateAsync(IBot bot, Update update)
    {
        // Echo back the text to user
        return UpdateHandlingResult.Handled;
    }
}
```

#### Configure the Bot

```c#
public void ConfigureServices(IServiceCollection services)
{
    services.AddTelegramBot<EchoerBot>(Configuration.GetSection("EchoerBot"))
        .AddUpdateHandler<TextMessageEchoer>()
        .Configure();
}
```

#### Use Webhook Middleware

```c#
public void Configure(IApplicationBuilder app)
{
    app.UseTelegramBotWebhook<EchoerBot>(ensureWebhookEnabled: true);
}
```

## Examples

Have a look at the [Sample app](./src/Telegram.Bot.Sample/) to see some examples.
