## UK South Wales and South West Channel and Scope Strategy

This document is an attempt at centralising and documenting the evolving strategy for this regional area's use of channels and region scopes.

It's not an attempt to dictate what we do but rather document what we are doing. It's also not intended as comprehensive documentation of the all relevant features, that's better done by the official documentation on the main [MeshCore site](https://meshcore.co.uk) 

## Comments and Suggestions Are Welcome

To suggest changes/additions => TBD

## Current Local Channels

See later for explanations of what hash channels and scopes are and how to manage them.

| Hash Channel Name        | Regional Scopes |
| ------------------------ | --------------- |
| ```#walesandwest-chat``` |                 |
| ```#walesandwest```      | ```#swsw```     |

## Public Hash Channels

These are relatively straight forward concept, and one need only know what they're called in order to add them via your MeshCore app and see any messages posted to the channel.

## Regional Scopes

### Regional Scopes 101

Regional scopes are a feature designed to limit the propagation of messages to regions to reduce unnecessary traffic across the wider mesh.

A repeater is typically configured to re-broadcast channel flood messages that either have no region scope or messages that match one or more specific region scopes. By default a repeater currently rebroadcasts everything irrespective of scope.

Thus a channel can be assigned scope(s) by an individual user such that anything they post in that channel will have the scope assigned. Consequently its flood transmission will be limited to local repeaters that accept that region, and will be dropped by more distant repeaters that only support other regions .

To successfully use scopes both the local repeaters must be configured to forward messages with the local region scopes and users channel configurations must be assigned appropriate supported scopes.

This is clearly a complex area and further information for that can be found below:

- [Repeater CLI: Region Management](https://github.com/meshcore-dev/MeshCore/blob/main/docs/cli_commands.md#region-management-v110)
- [Region Filtering](https://buymeacoffee.com/ripplebiz/region-filtering)

### Issues With Scopes

We are in a period of transition at the moment where regional scope is only supported by more recent repeater firmware and app versions. There is no central management in place or even a suggested strategy. Until scopes are properly understood and configured by the majority of repeaters in our region there is the chance that:

- Un-scoped messages intended for a region will be unnecessarily broadcast across the entire mesh.
- People visiting a scoped channel from outside the region will not see all/any of the messages as they've been dropped by repeaters on the path that are configured for other regions. Similarly people travelling outside their region will not be able to post to a scoped channel and have the messages reach the intended recipients.
- While a region contains a mix of repeaters with and without scope configuration and and a mix of versions where the feature is or is not implemented, scoped message propagation will be somewhat haphazard.

### Basic Scope Management

There are two aspects to scopes, configuring the companion to send any channel messages with a scope, and configuring a repeater to re-broadcast messages with a scope.

#### Companion Channel Configuration

Setting scopes for a channel can be done via the "..." menu at the top of a channel.
Once successfully done it will be visible at the top of the channel:

![[viewing-scope.png]]

#### Repeater Configuration

A repeater is typically configured to re-broadcast flood messages that either have no region scope or messages that match one of the configured either everything or just those messages
Below are examples of setting the ```#swsw``` scope.

This can be done with the Repeater CLI:

```
region put #swsw
region allowf #swsw
region save
```

It can also be done with **Manage Regions** in the Repeater Admin screen:

![](setting-scope.jpeg)