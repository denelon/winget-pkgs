---
author: <first-name> <last-name> <github-id>/<email>
created on: <yyyy-mm-dd>
last updated: <yyyy-mm-dd>
issue id: <github issue id>
---

# Spec Title

[comment]: # Link to issue: "For [#1](https://github.com/microsoft/winget-pkgs/issues/1)"

## Abstract

[comment]: # Outline what this spec describes
This specification defines criteria for auto-approval of PRs for a subset of packages in an allow list. These auto-approvals will be limited to packages in the allow list only when a limited set of properties have been modified. These would include package version, package URL (filtered by logic for installer URLs on the same domain and path), and the Installer SHA256.

## Inspiration

[comment]: # What were the drivers/inspiration behind the creation of this spec.
Several packages have rich metadata and when new versions are added, the only changes are the installer portion of the URL, the Installer SHA256 the package version.

## Solution Design

[comment]: # Outline the design of the solution. Feel free to include ASCII-art diagrams, etc.

## UI/UX Design

[comment]: # What will this fix/feature look like? How will it affect the end user?

## Capabilities

[comment]: # Discuss how the proposed fixes/features impact the following key considerations:

### Accessibility

[comment]: # How will the proposed change impact accessibility for users of screen readers, assistive input devices, etc.

### Security

[comment]: # How will the proposed change impact security?

### Reliability

[comment]: # Will the proposed change improve reliability? If not, why make the change?

### Compatibility

[comment]: # Will the proposed change break existing code/behaviors? If so, how, and is the breaking change "worth it"?

### Performance, Power, and Efficiency

## Potential Issues

[comment]: # What are some of the things that might cause problems with the fixes/features proposed? Consider how the user might be negatively impacted.

## Future considerations

[comment]: # What are some of the things that the fixes/features might unlock in the future? Does the implementation of this spec enable scenarios?

## Resources

[comment]: # Be sure to add links to references, resources, footnotes, etc.
