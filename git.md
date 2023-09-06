## Repository Creation

### Background

This initiative started as a proposal for some additional position / velocity / time additions to GPX 1.1.

It was essentially a proposal for a GPX 1.1.1 schema, essentially adding course + speed + accuracy estimates.

The initiative quickly grew in scope so rather than have it clutter up the gps-wizard project, it is now standalone.



### Filtering git

A clone of the gps-wizard repository was stripped down using git-filter-repo:

```sh
> du -sh .git
135M    .git

> $HOME/.local/bin/git-filter-repo --path docs/gpx/proposal/ --path docs/xmlschemas/ --path docs/gpx/extensions.md --path docs/apis

> du -sh .git
1.9M    .git
```
