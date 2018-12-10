---
title: Status Core Team

---
###### tags: `proposal` `core` `SNIP` `SNIP-core`

# Status Core proposal

## Summary

Status Core is responsible for implementing a decentralized, reliable Ethereum reference client for Mobile on Android and iOS. This client should provide a reliable communication medium and ability to access the open decentralized web.

Core team also sets up the design direction for the mobile app.

Desktop is out of scope, as is protocol research. Whitepaper use case implementation is partly in scope, partly not, depending on specifics and other teams.

Core needs an accountable, passionate get-shit-done mentality and drive, in contrast to the meandering blame-shifting.


## Budget

Headcount-based. 8 people.

The swarm also has a discretionary budget for bounty based development using Gitcoin, in order to parallelize development.

Assuming average organizational compensation, this would be roughly 69k/m. Possibly more based on performance, etc.
A self-imposed ceiling of 100k is proposed for budget bucketing (~10%) for the team as a whole.

Related adjacent activities such as security, devops, marketing, QA, etc will be assumed to be provided and funded by the Gmbh until further notice.

## Core participants

- Adam
- Andrea MP
- Chad (PM)
- DmitryS
- Igor (tech lead)
- Andrei M (Design)
- Pedro
- Roman
- Serhy (QA)

## Scope

See also: [team and responsibilities](https://notes.status.im/k0xVSu6nRvS5p0UAWV__BA?view)

Core should focus on problems/features that require multidisciplinary understanding and influence the application architecture. With the highest priority of making Status a usable application for consumption.

For simplicity, the responsibilities are split into 2 categories:
* **maintenance** - that means this effort is continuous and doesn't have any end date or exit criteria (publishing a mobile release is a good example, we don't stop)
* **project** - something that has a clear exit criteria, with a few iterations, after which the task is considered completed (for instance, when LES option is there and works)


## Process (aka How We Work?)

### Projects

Each project that is currently active should have an umbrella issue that should
link all the other issues. It contains a full description of the project and is
closed when the project is considered "done".

Some high-level discussions might also happen there.

This issue should contain all the other issues grouped into areas if necessary.

Each project should contain **Vision**, **Scope** and **Tradeoffs**.
1. Vision: a high-level goal of the project or a problem we are trying to solve.
2. Scope: limiting conditions that we empose on ourselves when implementing the project (what it is doing and what it is NOT doing).
3. Tradeoffs: a lot of projects can contain tradeoffs that make is feasible to implement. These should be documented there.

See https://github.com/status-im/status-react/issues/6757 as an example of a similar issue.

The projects list should have links to umbrella issues for each projects.

### Meetings & Philosophy

Process can be revisited through retrospective. Probably, the process should go to a github repository as a markdown file and using PRs to update it.

Taking as little of the parallel projects as possible. For example, we have to do maintenance anyway, so adding one other project as a focus area should be okay.

Weekly sync-up calls
- goals for the week
- focus area, progress
- post-meeting report in a Discuss thread

Post-project retrospective with post-mortem
- when the project milestone is done/failed
- when we are deciding to switch to another focus area

[DRIs](https://www.forbes.com/sites/quora/2012/10/02/how-well-does-apples-directly-responsible-individual-dri-model-work-in-practice/#38840682194c) for focus areas / maintenance tasks:
- single point of contact
- focused on one thing (one can be a DRI only to one focus area/maintenance task)

# Core: Maintenance

#### 1. Battery usage

#### 2. Application performance profiling

#### 3. Mobile Releases

- [Mobile release guide](https://notes.status.im/mobile-release-guide)
- [Mobile release notes](https://notes.status.im/mobile-release-notes)
- Upgrade policy
  - *User’s data.* User should be able to successfully upgrade preserving all his/her data from 0.9.19 to any beta release.
  - *Messaging/Transactions.* User should be able to successfully interact (make transactions, chat, etc) with users that have 0.9.20 or later release.

#### 4. Product Analytics

Product analytics provides insight into how Status is being used.  Currently we have 3 key metrics delivering insight:

- App downloads
- Public message
- ENS registrations

The core team is responsible for maintaining the reporting of these metrics at [status.im/analytics](https://status.im/analytics/)

# Core: Projects - Active

#### Message Reliability Improvements

The goal of this project is:
* to make messaging extremely reliable;
* to be able to prove that;
* to be able to show that information to a user (especially it is important to
    communicate if the message isn't delivered).

See more and up-to-date info in the Epic: https://github.com/status-im/status-react/issues/6757

# Core: Projects - Backlog

This backlog is organized in a prioritized way. The higher the project the more important it is.
When promoting the project, it is also important to make it more detailed.

#### "Save Password" on Android

The goal is to achieve feature-parity between iOS and Android in terms of
storing the password.

Epic: https://github.com/status-im/status-react/issues/5793

#### Support LES and ULC

Add an option to use LES and ULC in our application. It should work on Ropsten and Mainnet with working discovery.

Status can host clusters for LES and ULC, for both testing and reliability purposes, but the usage of LES/ULC shouldn't be limited to that.

See more and up-to-date info in the Epic: https://github.com/status-im/status-react/issues/6905

#### Spam filtering & DDoS Protection

We lack the way of protecting our network from spam, especially on the network
layer where a bot can relatively easily spam channels or at least waste users'
traffic.


#### LES/ULC: Economic incentives

> [dmitry] is it about proposal from Jacek?
> [igorm] probably, I'm not sure. it isn't the priority unless LES/ULC is just functional.

#### VipNode support


#### Implement EIP-681

https://eips.ethereum.org/EIPS/eip-681

> A standard way of representing various transactions, especially payment requests in Ethers and ERC #20 tokens as URLs.

#### Reduce unnecessary bandwidth usage

https://github.com/status-im/status-go/issues/1266

Make sure that we identify and fix all the unnecessary bandwidth usage cases. We need to be able to test the usage regressions in the future, so these issues don't happen anymore.

Currently, it looks like our application uses too much bandwidth.

**Why?**

1. We don't have bandwidth tests in place.
2. Mailserver requests seems to be very expensive in bandwidth and we probably receive a lot of duplicate messages.
3. We don't know all the places where networking is used, so we can't measure bandwidth client-side (we have to only rely on iOS/Android settings to check that).

#### Support multi-device experience

We need to be able to see the same message history on multiple devices (desktop + mobile is the common scenario).

#### Improve mechanisms of storing/using sensitive information on mobile

**Problems in this area**

1. Whisper uses the same keypairs as the blockchain, exposing one of them leads to losing funds.
2. It is possible (and it happened before) to leak sensitive data through logs and debugging information.
3. Unsafe defaults in some publicly available builds in the application.
4. Sensitive information is used directly (accessible to most of the app components), whereas the best practices is to provide minimal APIs to do whatever needs to be done w/o exposing data (see Secure Enclave data signing)
5. Only a single protection mechanism for sensitive data (should be at least two).
6. (potentially) Storing sensitive information which we don't have to store.

#### Improved message compatibility with other versions and other clients (using the *current* version of the protocol)

**Problems**
1. It is too easy to change protocol (message format, etc) in a PR w/o necessary oversight.
2. There are no tests to detect that message format or semantics didn't change after PR is merged.
3. We don't have any procedures and best practices on how to introduce changes to the current protocol.
4. We don't have any procedures and best practices on how to handle breaking changes gracefully and coordinate them between the clients.
5. We don't have any procedures, tools and best practices to handle breaking changes in mailservers.
> [pedro] Same thing for mailservers. Just recently there was a change to status-go that made it incompatible with the deployed eth.beta mailservers. We have no way to deal with backward compatibility, and having mailserver pinned makes it especially problematic.
> [igor] added this part too

#### Reduce metadata leakage

#### Audited private group chat and PFS

#### Reproducible builds

**Problems**
1. Right now it's hard to tell exactly which commit of any dependency was used to build a particular release
2. Users don't have guarantees that the release they downloaded matches the official release (i.e. hasn't been tampered with).
3. A user should be able to build the sources on his own machine and obtain exactly the same binaries. 

#### Integrate with `libp2p`

#### Better discovery

1. Support/integrate geth initiatives

#### Better censorship resistance

1. Being able to update bootnodes list if they are blocked


#### Push Notifications v2

https://ideas.status.im/ideas/086-push-notif-v2/README

---

# Outscoped Projects (to other teams)

#### 14. Better CI experience

To DevOps team?

Not sure if the core team responsibility (igorm).
This is one of the problems that everyone depends on. If/when our CI is unstable, essentially, the whole dev team cannot work. 
> [???] Although I agree that this is mission critical, I would like to see this offloaded to a different team, it requires a specific skillset (which we might have in the core-team, but not only) and not many dependencies, also our plate is quite full as it is.
> [igorm] Agree, I just want to make sure it will be prioritized by some team, and asap. 

**Problems**
1. Issues with builds scripts on macOS builders (not isolated)
2. Way too many network requests on each build process (if any of these fails, all the build procedure fails). 
3. No retries of commonly unstable steps (again, when it fails, everything fails).
4. No decent caching/reusing of artifacts (that makes the build process very slow).