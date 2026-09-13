# Local email dumping

## Context
For systems like e-commerces where users contantly interact with services that might send emails for the user. On real application this involves the user of an **email provider**. The issue is setting up such providers involve the use of sensitive information, which should not be exposed in public repositories, such as github. At the same time, it's important to provide a feature that generates these emails and allows users to access its contents. 

## Options considered
1. Export emails to individual files inside the host's filesystem.
2. Allow anyone who wants to build the project the possibility of registering their own email providers.
3. Expose a configuration for my own email provider.

## Decision
Exporting the emails to a local file is, by far, the best choice. It provides a very simple and intuitive approach to this feature. In the end, emails are used to communicate change or events to users and this is perfectly achievable with this approach while at the same time I can avoid exposing sensitive data from my own email provider and avoid the hassle of setting up a custom email provider, at least for now.

Another benefit of this, although small, is that the emails exported to files always contain the same **sender**, for example `inkwell_company@gmail.com`.

Fortunately this implementation can be easily replaced for another one, more in-line with a real maling system, just by using simple java interfaces.

## Consequences
1. Testing scenarios where an email fails to be sent becomes harder.
2. Any email sent can be easily and quickly read on its folder. 
3. Checking for an specific email on a giant list of files can be messy if the files are not named properly.
