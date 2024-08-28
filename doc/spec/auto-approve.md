---
author: <first-name> <last-name> <github-id>/<email>
created on: <yyyy-mm-dd>
last updated: <yyyy-mm-dd>
issue id: <github issue id>
---

# Auto approve new package versions in an allow list

[comment]: # Link to issue: "For [#1](https://github.com/microsoft/winget-pkgs/issues/1)"

## Abstract

This specification defines criteria for auto-approval of PRs for a subset of packages in an allow list. These auto-approvals will be limited to packages in the allow list only when a limited set of properties have been modified. These would include:
*  Package version
*  Package URL (filtered by logic for installer URLs on the same domain and path)
*  Installer SHA256
*  Product Code

Package Version should be an exact match to the values written in the registry for Apps & Features data.
Other Apps And Features entries should also be an exact match.

## Inspiration

Manual review takes time, and for a subset of packages with rich metadata and only installer/version level metadata is changed. Automation can identify when specific criteria are met, and eliminate the toil of a manual review. This can also reduce the time from when a PR is submitted and it gets approved. This is especially helpful on weekends/holidays and when PRs would normally sit open until the next business day for review.

## Solution Design

This would be implemented in the Validation pipelines.

Good example PRs:
TODO: explain what's going to work or not for each...
* https://github.com/microsoft/winget-pkgs/pull/170290/files
* https://github.com/microsoft/winget-pkgs/pull/170388/files

### Automated Identification
Evaluate the version for a package to be added. If the version is newer than the latest version of a package in the repository identify which fields have been changed, added, or removed from the previous version.

### Allow List Management
Two moderators are required to add a package to the allow list.
One moderator can remove a package from the allow list.

## UI/UX Design

PRs for new package versions of packages in the allow list will not require manual review if specific criteria are met.
One of the bots will comment on PRs for these packages if criteria are met for auto-approval. If criteria are not met for auto-approval, the bot will comment with the fields that prevent auto-approval for PRs against packages in the allow list.

## Capabilities

[comment]: # Discuss how the proposed fixes/features impact the following key considerations:

### Accessibility

No impact expected

### Security

[comment]: # How will the proposed change impact security?

### Reliability

[comment]: # Will the proposed change improve reliability? If not, why make the change?

### Compatibility

No breaking changes are anticipated.

### Performance, Power, and Efficiency

The average time between PR submission and subsequent approval will be reduced on average.

## Potential Issues

[comment]: # What are some of the things that might cause problems with the fixes/features proposed? Consider how the user might be negatively impacted.

## Future considerations

The verified publisher feature may require mutual exclusion or modification with this feature.

## Resources

[comment]: # Be sure to add links to references, resources, footnotes, etc.
