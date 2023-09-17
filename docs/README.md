## GPX Ideas

### Background

GPX is the most commonly supported file format for the exchange of GPS / GNSS related activity data, and is useful for more than just GPS data. Handheld GNSS receivers, custom loggers, smart phones and wearables all tend to provide GPX exports + imports for GPS / GNSS and other sensor data.

The existing GPX 1.1 schema already lends itself to the exchange of spatio-temporal data, especially sensor data which is by its very nature temporal. Several manufacturers achieve this with proprietary GPX extensions for data such as heart rate + cadence, air / water temperature and water depth.

However, proprietary GPX extensions can lead to issues when exchanging data between different software. Although the big players in the fitness market are (realistically) unlikely to change the way they exchange sensor data, there remain a large number of opportunities for common data exchange.



### Overview

This project has been created to capture ideas for a collection of "standard" GPX extensions for sensor data relating to fitness, sailing, aviation, and meteorology. Taking a holistic view has identified a lot of commonality, thus lending itself to reusability and avoidance of duplication / redundancy.

Subject to acceptance by the wider GPX community, I firmly believe a collection of "standard" extensions for GPX 1.1 will provide a solid foundation for the exchange of common GNSS + sensor data between software providers, especially for the modern-day apps on smart phones and watches.

In addition to a collection of "standard" extensions, several enhancements may also be made to the core GPX schema, essentially GPX 1.2. These enhancements will all be backwards compatible with GPX 1.1, yet implement many of the common suggestions / requests since the release of GPX 1.1.



### Approach

The contents of this project are likely to be quite fluid as it is primarily to capture ideas and thoughts for discussion within the GPX community. My approach is "commit often, perfect later, publish once" so you should regard everything in these pages as WIP, rather than a polished proposal.

In August 2023, I submitted a proposal for COG, SOG and accuracy estimates in GPX, which nominally referred to as GPX 1.1.1. This new project called "GPX Ideas" supersedes the GPX 1.1.1 proposal, but the original content is still [available](proposal/README.md) within this project as background / reference material.

It is envisaged that this project will start off being a repository for material that can be discussed in the GPX developer list and subsequently be converted into actual XSD documents that can be reviewed and tested.



### Content

The content of the project relates to 3 independent topics:

1. GPX [Extensions](extensions/README.md) - GPX extension schemas for fitness, nautical, aviation, meteorological, etc
2. General [Usage](usage/README.md) - topics relating to general usage of GPX, such as validation and file compression (gpz)
3. GPX [Core](core/README.md) - improvements to the core GPX schema, essentially GPX 1.2

Each of the topics above will be documented separately, since they are largely independent.

Simply click the links above to access the page(s) for each topic.

