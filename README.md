# Google Assistant

![Google Assistant logo](images/Google_Assistant_logo_200px.svg)

Having heavily investigated [Amazon Alexa](http://github.com/mramshaw/Alexa-Stuff), it seemed to be time
to take a good look at __Google Assistant__.

## Content

The contents are as follows:

* [Software versus Hardware](#software-versus-hardware)
* [Devices](#devices)
* [Installation](#installation)
* [Voices](#voices)
* [Wake Word](#wake-word)
    * [Smartwatches](#smartwatches)
* [Google Actions](#google-actions)
* [DialogFlow](#dialogflow)
    * [Intents](#intents)
    * [Parameters](#parameters)
    * [Entities](#entities)
    * [Fulfillment](#fulfillment)
    * [Integrations](#integrations)
* [Certification](#certification)
* [Privacy](#privacy)
* [To Do](#to-do)

## Software versus Hardware

__Google Assistant__ is the software part of Google's voice offerings while __Google Home__ devices are
(one of) the hardware components.

## Devices

In addition to Google Home and other Google devices, Google Assistant is available on Android devices
(including [Wear OS](http://wearos.google.com) devices such as smartwatches) and also iOS devices.

## Installation

To enable Google Assistant on your Android phone, navigate to the Google Play store and install it.

Here is the link:

    http://play.google.com/store/apps/details?id=com.google.android.apps.googleassistant

## Voices

Internally, Google Assistant has several voices available. These are colour-coded, with names like "Red"
and "Purple". Additionally, there are voices with names that subtly hint at their origins - these have
names like "British Racing Green" and "Sydney Harbour Blue".

As you would expect, the default voice (Red) is actually the best choice - although being able to choose
a personalized custom voice is a very nice touch.

## Wake Word

To let Google know you want to invoke a Google Action, start with:

    "Hey Google"

As in:

    "Hey Google, Talk to Peanut Allergy Facts"

Here __Peanut Allergy Facts__ is the app to be invoked, and __Hey Google__ is what is known as a ___Wake Word___.

As opposed to Amazon Alexa, which expects verbs such as __Open__, __Launch__ or __Start__, in Google Assistant
the standard way to invoke an app is with __Talk to__ (of course you may still specify Open, Launch or Start
instead).

This breaks down as follows:

Vendor|wake word|verb|app name
------|---------|----|--------
__Amazon__|Alexa,|open|Peanut Allergy Facts
__Google__|Hey Google,|Talk to|Peanut Allergy Facts

This distinction between the normal ___verb___ is probably insignificant, as both vendors allow customization.

[Amazon also allows customization of its [wake word](http://github.com/mramshaw/Alexa-Stuff#wake-word).]

#### Smartwatches

With a [Wear OS](http://wearos.google.com) device, either say "Ok Google" or else press and hold the power button
to get started.

## Google Actions

Individual components for Google Assistant are called ___Actions___ (these are what AWS Alexa calls ___Skills___).

To see available Google Actions, refer to:

    http://assistant.google.com/explore

Note that certain actions may not be available in all languages or all regions.

It is possible to configure Google Assistant so as to trigger multiple actions with a single voice command.

Google Actions offers `Built-in intents`, `Templates` and `Home automation` - any of which may serve your purposes.

For everything else there are `Custom intents` - which will open a [Dialogflow](#dialogflow) console in a new window.

## DialogFlow

While it is possible to create simple actions within the Google Actions console, for more sophisticated
actions there is the aptly-named [DialogFlow](http://dialogflow.com/).

Google originally purchased [API.AI](http://api.ai) which it rebranded as DialogFlow. [API.AI was previously
known as Speaktoit. Note that the API.AI URL redirects to DialogFlow.] Nevertheless, YouTube videos and
the like occasionally still refer to API.AI; any changes are generally minor and cosmetic.

One interesting thing about DialogFlow is that it can interact with multiple backend services, such as
Slack and Alexa (it refers to these as [integrations](#integrations)). It is not limited to Google Actions,
although these are obviously the prime target. However, it does require a Google Project for the frontend
portion.

Dialogflow refers to what Alexa calls skills and Google calls apps as ___Agents___.

Dialogflow offers `Prebuilt agents` as well as `Small Talk` - both of which may serve your purposes and are
well worth a look.

Agents are generally coordinated within a Request/Response format, possibly using ___webhooks___.

Inidividual [intents](#intents) must be established - after which optional [entities](#entities) may be
established and [fulfillment](#fulfillment) or [integrations](#integrations) may take place.

#### Intents

Broadly speaking these are the main concepts of a question or statement.

[I have diagrammed these for the [Wit.ai API](https://github.com/mramshaw/GCP-Slackbot#wit).]

Intents can be individually tested from within DialogFlow.

Follow-up intents are a special case - these can only match if their parents have previously matched.

![Dialogflow Follow-up intents](images/Dialogflow_Follow-up_intents.png)

Read more about Follow-up intents here:

    http://dialogflow.com/docs/contexts/follow-up-intents

#### Parameters

These seem to be _parameters_ of the __Intent__ question or statement, for instance in the phrase:

    "tell me yesterday's weather"

![Dialogflow Parameter](images/Dialogflow_Parameter.png)

In this case `yesterday` constitutes an intent parameter of type 'date' that can be defaulted.

#### Entities

These are the concepts to be established in the dialogue, such as `departure date` or `animals`.

For more information, refer to the documentation:

    http://dialogflow.com/docs/entities

#### Fulfillment

Generally speaking, these operate as extension points to the existing dialogue flow.

Normally these would operate as external API calls.

> Fulfillment is code that's deployed as a webhook

    http://dialogflow.com/docs/fulfillment

[It may also consist of code that is defined in the Inline Editor. It's either/or,
as in EITHER a webhook OR inline code. The inline code will be __javascript__ and
will be deployed to Google Firebase.]

#### Integrations

Generally speaking, integrations will be to Google Assistant - but many other options are possible.

## Certification

While Alexa offers _beta testing_, Google Assistant offers _alpha testing_ __and__ _beta testing_.

Unlike Alexa, Google Assistant will increment a version number as each successive Google Action is certified.

Also unlike Alexa, Google __requires__ a published ___privacy policy___ as a part of its certification
process (it is impossible to get an Action certified without one, even if it captures no data of any
kind).

## Privacy

As noted above, Google has taken steps to be transparent as to the type of data it captures.

Also, each certified Action has a published privacy policy.

If privacy is a concern, it is possible to view (and manage) the personal information that Google tracks:

    http://myactivity.google.com/

[This is very much worth looking at, if simply to see the type of granular detail that Google tracks.]

The following privacy checkup link is worth a look as well:

    http://myaccount.google.com/intro/privacycheckup

Google appears to be fairly responsible in the way that it always asks for consent to capture personal
data (such as voice snippets, or gesture usage, etc). While Google Apps generally require opting-in to
this type of data capture (if only for voice recognition or gesture recognition purposes), permission
can always be revoked at a later stage (and the captured data can also be deleted).

## To Do

- [ ] Continue testing
- [ ] Investigate Firebase integration
- [x] Investigate DialogFlow
- [ ] Investigate DialogFlow fulfillment
- [ ] Investigate DialogFlow integrations (other than Google Actions)
- [ ] Investigate Google Assistant versus Alexa versus Siri
- [ ] Publish a Google Action
