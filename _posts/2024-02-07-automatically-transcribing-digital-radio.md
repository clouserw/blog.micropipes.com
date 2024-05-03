---
layout: post
title: Automatically transcribing digital radio
tags:
- software
- radio
---

I've recently been using [DSD FME](https://github.com/lwvmobile/dsd-fme) to
decode Silke Communication's [FleetNet Network](https://www.silkecom.com/fleetnet)
radio traffic around me.  After some configuration effort it's working well,
but I realized one of the things I've really appreciated about the past decade
is the slow migration to asynchronous communications (email, messages, etc.)
instead of voice calls or in-person meetings that interrupt whatever I'm doing.
I don't want to actually listen to the radio traffic, rather, I'd like to skim
it, preferably visually, after-the-fact to see if anything interesting
happened.

Maybe we can automatically transcribe it?

Historically, automatic transcription hasn't been great, even in ideal
environments, let alone something as sketchy as a radio where calls can fade
and a good percentage of the words are jargon.  But this is 2024 and AI rules
the day, right?  Maybe things are better.

DSD FME can be configured to dump every call to a `.wav` file in a directory
which takes care of the source audio.

I wrote a [short python script](https://github.com/clouserw/dsd-fme-transcribe)
which watches a directory for file handles closing (meaning, the call is over)
and sends the files through [OpenAI's Whisper](https://github.com/openai/whisper) library to convert it to text.
Running it while audio files are coming in provides a roughly real-time
transcription.  Example output from this evening while the local school buses
were dropping off students:

> TG Bus Dispatch RID 8703: 237 to central.
>
> TG Bus Dispatch RID 8761: 2-3-7 standby just a moment. 2-3-2 go ahead.
>
> TG Bus Dispatch RID 8784: I just wanted to update you that I'm route complete. Thank you.
>
> TG Bus Dispatch RID 8761: Okay, 10-4. Thank you. Go ahead. Two, three, seven.
>
> TG Bus Dispatch RID 8761: 274 standby just a moment. I got one more route calling in here. 237, I'm ready for you. Go ahead 237.
>
> TG Bus Dispatch RID 8703: So it is closed and I have three stops down there. What do I do?

The system works!  Is it accurate?

Ehh.  I'd say it's about 75% accurate after watching it for a bit.  It gets
most of the messages but does trip up occasionally.  I'm using the [base model](https://github.com/openai/whisper?tab=readme-ov-file#available-models-and-languages)
because my computer isn't very fast but using a larger model may improve the
accuracy.  Even better would be to train a model on radio communications. One
similar example where they did tune their model is [this thesis applying the technique](https://repository.tudelft.nl/islandora/object/uuid:8aa780bf-47b6-4f81-b112-29e23bc06a7d?collection=education)
to air traffic control radio.  They achieved a ~13% error rate with a pretty
challenging data set.


Is this revolutionary?

Not really.  There are [many examples](https://github.com/openai/whisper/discussions/categories/show-and-tell)
of using Whisper to decode audio like this, even in real time.  I wrote this
because all the examples seem too complicated for someone just looking at the
library for the first time and it's fun to start and finish a project in a
couple of hours!
