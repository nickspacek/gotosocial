# HTTP Signature Tester

This document proposes software for validating/debugging **HTTP Signatures**.

## What's the problem?

One of the pain points of writing fediverse software is implementing **HTTP Signatures**, which are widely used to authenticate and apply ACLs to ActivityPub messages.

Current (28/10/22) fediverse implementations like Mastodon, Pixelfed, GNU Social, Pleroma, GoToSocial, etc use the `cavage` HTTP Signature standard [[RFC](https://datatracker.ietf.org/doc/draft-cavage-http-signatures/12/)], mostly because Mastodon implemented it first, and it has proven to be 'good enough' for passing fediverse messages around with reasonable safety. (The `cavage` standard has since been overtaken by the `httpbis` version [[RFC](https://httpwg.org/http-extensions/draft-ietf-httpbis-message-signatures.html)], but almost all fediverse implementations have kept the previous standard, presumably for the purposes of backwards-compatibility.)

In the current fedi ecosystem, implementations are usually expected to HTTP sign outgoing `POST` requests to the inboxes of other instances + actors. If `POST` requests are not HTTP signed, then generally speaking the `POST` of the activity will be rejected with a 401 error code or similar, since it cannot be verified as originating from the actor it claims to have been created by.

Some implementations -- like Secure Mode Mastodon and GoToSocial -- also sign `GET` requests to remote resources, and require incoming `GET` requests to also be signed, so that ACLs can be applied. As with `POST` requests, if a `GET` to Secure Mode Mastodon or to GoToSocial is not signed, the instance will return a 401 error code. This extra layer of security helps to prevent scraping by bots and by blocked domains.

Unfortunately, while http signatures are useful as a layer of security, http signature errors are a frequent cause of federation issues, since the standard is not very simple. While there are http signature libraries available for most major programming languages, these implementations vary in terms of completeness, usability, and maintenance. Furthermore, many fedi softwares simply 'roll their own' http signature code, which is not necessarily conformant to the standard.

This situation presents a high barrier of entry to people wanting to write their own fedi servers, since they will necessarily have to spend a lot of time debugging why they are receiving 401s when trying to interact with other softwares. Moreover, the error text returned alongside most implementations' 401 errors is usually curt, to avoid leaking any sensitive security information. That is to say, while it's clear from the 401 error code that signature authentication failed, looking at the error text usually doesn't reveal anything about *why* it failed.

In the long term, the difficulty + frustration of debugging http signature issues will likely put new developers off working on a fediverse software, which will lead to a smaller and more constrained ecosystem. Bummer!

## Proposal

[todo: general outline of http signature debugger component]

## Architecture

[todo: architecture for http signature debugger component]

## API

[todo: api for http signature debugger component]

## Links

[todo: links to useful documents]
