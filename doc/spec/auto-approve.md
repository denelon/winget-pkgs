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

* PackageVersion
* InstallerUrl (filtered by logic for installer URLs on the same domain and path)
* InstallerSha256
* ProductCode
* ReleaseDate
* ReleaseNotesUrl (filtered by logic for URLs on the same domain and path)

## Inspiration

Manual review takes time, and for a subset of packages with rich metadata and only installer/version level metadata is changed. Automation can identify when specific criteria are met, and eliminate the toil of a manual review. This can also reduce the time from when a PR is submitted and it gets approved. This is especially helpful on weekends/holidays and when PRs would normally sit open until the next business day for review.

## Solution Design

This would be implemented in the validation pipelines. If all existing manifest validation checks succeed, the pipeline would check if the package is in the allow list. If it is, the pipeline would check if the PR meets the criteria for auto-approval. PRs meeting the criteria would be automatically approved and merged.

Example PRs that would be auto-approved:

1. [#170290](https://github.com/microsoft/winget-pkgs/pull/170290/files)
    * Update to an existing version manifest ✅
    * Updated fields are: PackageVersion, InstallerSha256, ProductCode ✅

2. [#170388](https://github.com/microsoft/winget-pkgs/pull/170388/files)
    * New version manifest of an existing PackageIdentifier ✅
    * Updated fields from previous manifest are: PackageVersion, InstallerUrl, InstallerSha256, ReleaseDate, ReleaseNotesUrl ✅

### Automated Identification

Evaluate the version for a package to be added. If the version is newer than the latest version of a package in the repository identify which fields have been changed, added, or removed from the previous version.

### Allow List Management

Two moderators are required to add a package to the allow list.
One moderator can remove a package from the allow list.

## UI/UX Design

PRs for new package versions of packages in the allow list will not require manual review if specific criteria are met.
One of the bots will comment on PRs for these packages if criteria are met for auto-approval. If criteria are not met for auto-approval, the bot will comment with the fields that prevent auto-approval for PRs against packages in the allow list.

## Capabilities

This feature enables the validation pipelines to determine if a PR is suitable for merge without manual review.

### Accessibility

No impact expected

### Security

None of the current security controls are expected to be impacted. All security checks associated with the manifest and the package installer will still be in place.

### Reliability

Reliability is not expected to be impacted in a negative way. By decreasing the average time between a valid PR submission and subsequent approval for merge should decrease. This should increase the reliability of the WinGet user experience by making the latest versions of packages submitted by PR available sooner for customers.

### Compatibility

No breaking changes are anticipated.

### Performance, Power, and Efficiency

The average time between PR submission and subsequent approval will be reduced on average.

## Potential Issues

It's possible users may forgo updates to description, release notes, and other optional metadata in order to get a package merged in more quickly. This could lead to additional PRs to update the metadata after the fact which could get forgotten or delayed.

## Future considerations

* The verified publisher feature may require mutual exclusion or modification with this feature.
* For extending allow list to a larger set of packages, validation pipelines would require updates to match ARP manifest fields against their exact registry values.

## Resources

[comment]: # Be sure to add links to references, resources, footnotes, etc.
