[Home](README.md)

## Traffic Management

The recent explosive growth in the popularity of MeshCore has lead to situation where in some areas traffic has reached saturation. Areas densely served by repeaters and/or well connected to the national (and indeed international) mesh are suffering most. The consequence is that messages get lost because of collisions and it can become difficult to send messages and manage nodes.

## Mitigation Strategies

### Reducing Advert Frequency

Since repeater adverts currently make up a very significant proportion of all traffic, reducing their frequency is an obviously beneficial. Setting the maximum allowable values in Advert Intervals would be:

- Auto Advert (Zero Hop): 240 mins
- Auto Advert (Flood): 168 hours

A value of zero disables either one of these.

### Use Of Regions

[Regions](Regions.md) are a way of restricting (scoping) how far [Channel](Channels.md) messages propagate. Other traffic such as Adverts (which form a significant proportion of all traffic) will be unaffected.

### Increasing Path Hash Size

In your companion under Experimental settings (currently) is a Path Hash Size value. It is well described there and so won't repeat that, but increasing the value from 1 byte to 2 or 3 will not only reduce path ambiguity but also limit how far (how many hops) your messages will travel.

- 1 byte: 64 hops
- 2 bytes: 32 hops
- 3 bytes: 21 hops

There is also a repeater CLI setting for [path.hash.mode](https://docs.meshcore.io/cli_commands/#region-management-v110) which similarly affects how far adverts propagate. The following sets the hash mode to 3 bytes (the value is desired size -1):

```
set path.hash.mode 2
```

Note that his is a relatively new setting that requires repeaters with firmware 1.14 or newer. Older repeaters only forward traffic with a hash size of 1. My experience is that around me the majority of repeaters are updated fairly regularly and use of this feature doesn't unduly affect my usage.

### Decreasing flood.max

The flood.max value is a repeater CLI setting that specifies a maximum path length (hops) above which a repeater will drop the message/packet. It defaults to 64 and thus if a packet arrives that has already traversed 64 hops then it will be dropped. This affects both channel messages and adverts.

For example:

```
set flood.max 16
```

The default of 64 is a generous value and can be dropped to reduce traffic. I rarely see traffic with more than 30 hops, and most of it comes in at under 20. Local traffic (South West & South Wales) tends to be 8 or less - but your situation may be very different.

Note that there is obviously a **statistical relationship** between geographic distance and number of hops but it's not absolute. Messages from Scotland or the Netherlands tend to arrive with a higher hop count than those from an adjacent county but this can't be guaranteed and sometimes wild paths will be seen. In Bristol I see Cornish traffic mostly at 6 or less hops but also the occasional 20.

The higher the hop count the less likely you are to receive a message. I've noticed that as conversations become more distant I'm more likely to only get fragments of them anyway which isn't especially useful.

I would suggest initially leaving the value at something safe like the default (64) or perhaps 30 for a while and enabling "Message Settings"/"Show Channel Message Hops". You will get to know what your traffic profile is and what value you can drop this to without losing messages from people you want to hear from.

However, bare in mind that adjusting this value also affects the mesh experience of those around you and perhaps consider this as a last resort when congestion at your local repeater is excessive.

For example I had a hilltop repeater that was repeating pretty much continuously. That traffic was amplified by several repeaters in a valley below and the mesh around me was overloaded to the point where sending was very unreliable. I have now set flood.max to 8 and the amount of mesh traffic is vastly reduced. I receive more local traffic and can once again send reliably. Obviously this impacts remote traffic for other people nearby but their experience of it was poor to begin with, at least now local traffic is more reliable.

If some consensus around a regional value for flood.max emerges, I will update it here.

