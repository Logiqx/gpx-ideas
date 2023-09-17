## GPX Ideas

### Background

GPX is the most commonly supported file format for the exchange of GPS / GNSS related activity data, and grown beyond being only for GPS data. Handheld GNSS receivers, custom devices, smart phones and wearables (sports watches + smart watches) all tend to provide GPX exports + imports.

The existing GPX 1.1 schema lends itself well to the exchange of other spatio-temporal data, especially sensor data which is by its very nature temporal. Several manufacturers already use proprietary GPX extensions to exchange data such as heart rate + cadence, air / water temperature and water depth.

Proprietary GPX extensions can lead to issues when exchanging data between different software providers and although the big players in the fitness market are unlikely to change the way they exchange sensor data such as heart rate, there are wider opportunities available for a number of activities.



### Overview

This project is to capture the thoughts relating to a collection of "standard" GPX extensions for the sensor data relating to fitness, sailing, aviation, and meteorology. Taking a holistic view has identified a lot of commonality, thus lending itself to reusability and avoidance of duplication / redundancy.

Subject to acceptance by the wider GPX community, I believe that a collection of "standard" extensions for GPX 1.1 will provide a solid foundation for the exchange of common GNSS + sensor data between software providers, especially for apps on modern devices such as smart phones and watches.

In addition to a collection of "standard" extensions, several enhancements may also be made to the core GPX schema, essentially GPX 1.2. These enhancements will all be backwards compatible with GPX 1.1, yet provide many of the common suggestions / requests since the release of GPX 1.1.



### Approach

The contents of this project are likely to be quite fluid as it is primarily to capture ideas and thoughts to facilitate community discussion. My general approach is "commit often, perfect later, publish once" so you should regard everything in these pages as WIP, rather than a completed proposal.

In August 2023, I wrote a proposal to add COG, SOG and accuracy estimates to GPX, which I tentatively referred to as GPX 1.1.1. This new project for "GPX Ideas" supersedes the proposal for a GPX 1.1.1, but the August proposal is still [available](proposal/README.md) within this project as background / reference material.

It is envisaged that this project will start off being primarily material for discussion on the GPX developer list and subsequently be converted into actual XSD documents that can be reviewed and tested. 



### Topics

This project covers several independent topics:

1. GPX [Extensions](extensions/README.md) - GPX extension schemas for fitness, nautical, aviation, meteorological, etc
2. GPX [Usage](usage/README.md) - topics relating to general usage such as validation and file compression (gpz)
3. GPX [Core](core/README.md) - improvements to the core GPX schema, essentially GPX 1.2

Each of the topics above will be documented separately, since they are largely independent.

Simply click the links above to access the page(s) for each topic.

