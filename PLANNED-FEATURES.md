# GoreeCloud Cast — Planned Features

> **Authority:** Repository-native planned-feature record. This file preserves the complete former Drive planning specification; Google Drive is retired as a feature-state source after verified migration.
> **Lifecycle boundary:** Planned / proposed content below does not establish implementation, release, deployment, or Stable status.

---
title: "GoreeCloud Cast — Planned Features and Capabilities"
product: "GoreeCloud Cast"
document_type: "Feature and Capability Roadmap"
status: "Proposed / Planned"
version: "v0.5"
classification: "Internal"
authoritative_record: repository
implementation_status: "Not established by this specification"
primary_interface: "Glaze UI"
design_principle: "Transfer experiences between devices, not merely pixels."
last_updated: "2026-09-16"
---

## Migrated planning specification
 
## Document Status
 
**Product:** GoreeCloud Cast  
**Category:** Cross-device media, display, audio, and session-transfer service  
**Status:** Proposed / Planned  
**Implementation status:** Not established by this specification  
**Primary interface:** Glaze UI  
**Design principle:** Transfer experiences between devices, not merely pixels.
  
# 1. Overview
 
GoreeCloud Cast is a proposed GoreeCloud platform service for securely discovering nearby devices and transferring media, audio, applications, displays, playback sessions, and interactive experiences between them.
 
GoreeCloud Cast should serve as shared infrastructure rather than forcing every GoreeCloud application to independently implement device discovery, pairing, remote playback control, synchronization, receiver management, permissions, and session recovery.
 
The service should support phones, tablets, computers, televisions, speakers, embedded receivers, browsers, dedicated media devices, and future GoreeCloud device categories.
 
The preferred behavior is **session handoff**.
 
When possible, the receiving device should independently play or render the requested content while the originating device becomes a controller. Continuous screen or media forwarding should only be used when independent receiver-side playback is unavailable or inappropriate.
 
GoreeCloud Cast should therefore support four fundamental models:
 
1. **Handoff** — transfer the experience to another device.
 
2. **Remote playback** — instruct another device to independently retrieve and play content.
 
3. **Media streaming** — send media data directly to another device.
 
4. **Mirroring** — reproduce a display, application, or audio output in real time.
 
# 2. Product Goals
 
GoreeCloud Cast should provide:
 
- Simple device discovery.
- Fast and understandable connection flows.
- Secure device pairing.
- Explicit trust relationships.
- Fine-grained permissions.
- Local-first operation.
- Media playback handoff.
- Cross-device playback continuity.
- Remote playback controls.
- Queue synchronization.
- Application casting.
- Screen mirroring.
- Audio casting.
- Multi-device playback.
- Multi-room audio.
- Receiver groups.
- Controller migration.
- Multiple simultaneous controllers.
- Guest casting.
- Persistent Cast sessions.
- Reliable reconnection.
- Strong privacy indicators.
- Accessible controls.
- Adaptive Glaze UI interfaces.
- Common developer APIs.
- Centralized Cast policy and administration.
- Extensibility for future GoreeCloud devices.
 
# 3. Core Design Principles
 
## 3.1 Local First
 
Normal casting between devices on the same trusted network should not depend on a remote service.
 
Local device discovery, pairing, playback control, media transfer, and session management should continue functioning when external connectivity is unavailable whenever the underlying content is locally accessible.
 
Remote infrastructure should enhance GoreeCloud Cast rather than become a requirement for basic operation.
 
## 3.2 Receiver-First Playback
 
When a receiver is capable of independently obtaining and playing the requested content, GoreeCloud Cast should transfer the playback instructions and state rather than continuously transmitting the media through the controller.
 
This reduces:
 
- controller battery usage;
- network duplication;
- unnecessary latency;
- interruption when the controller application closes;
- dependence on the original device.
 
The originating device can then function primarily as a remote controller.
 
## 3.3 Mirroring as a Fallback
 
Display mirroring should be available but should not be the default architecture for ordinary media playback.
 
Preferred order:
 
**Native receiver playback → direct media transfer → application streaming → display mirroring**
 
Applications should be able to influence this decision when their content or security requirements require a particular mode.
 
## 3.4 Explicit Trust
 
Discovery does not imply authorization.
 
A device that can see another device should not automatically be able to:
 
- play content on it;
- control its volume;
- display notifications;
- mirror a screen;
- capture an application;
- administer it.
 
Trust and permissions should remain separate.
 
## 3.5 Minimum Required Access
 
Each Cast session should receive only the capabilities required to perform that session.
 
A music application casting a song should not automatically receive permission to mirror the device display.
 
A trusted remote controller should not automatically become an administrator.
 
## 3.6 Continuity
 
Temporary network changes, application restarts, screen locking, controller sleep, or controller switching should not unnecessarily destroy a Cast session.
 
Where technically possible, the session should survive independently of the original user interface that created it.
 
## 3.7 Visible State
 
Users should always be able to determine:
 
- whether casting is active;
- what is being cast;
- which device is receiving it;
- which device initiated it;
- who can control it;
- whether the session is local or remote;
- whether the controller may disconnect;
- whether a screen, application, camera, microphone, or other sensitive source is being shared.
 
# 4. Major Casting Modes
 
## 4.1 Media Cast
 
Send an individual media item to a compatible receiver.
 
Supported media categories should eventually include:
 
- video;
- music;
- podcasts;
- audiobooks;
- live media;
- photographs;
- image galleries;
- presentations;
- compatible documents;
- other application-defined media.
 
Metadata should travel with the session where appropriate.
 
## 4.2 Playback Handoff
 
Move an active playback experience from one device to another.
 
Handoff should preserve as much state as possible, including:
 
- playback position;
- play/pause state;
- queue;
- repeat state;
- shuffle state;
- selected audio track;
- selected subtitle track;
- playback speed;
- chapters;
- current item;
- next item;
- session metadata;
- application-defined playback state.
 
Handoff should feel like the same session moved to another device rather than a second unrelated playback attempt.
 
## 4.3 Continue On
 
GoreeCloud applications should be able to expose a consistent **Continue on…** action.
 
Example flow:
 
**Current Device → Continue on… → Select Receiver → Session transfers → Current Device becomes controller**
 
Users should also be able to return the session:
 
**Receiver → Continue here**
 
## 4.4 Direct Media Streaming
 
If the receiver cannot independently access the original media source, the controller or another authorized local source can stream the media directly.
 
The Cast service should negotiate:
 
- available formats;
- receiver performance;
- resolution;
- bitrate;
- audio capabilities;
- subtitle support;
- network conditions;
- latency requirements.
 
## 4.5 Application Casting
 
Users should be able to share only one application rather than their entire display.
 
Application casting should prevent unrelated applications, notifications, and private content from appearing on the receiver.
 
Applications may optionally expose enhanced application-casting support for better quality or lower latency.
 
## 4.6 Window Casting
 
Desktop-style environments should support sharing an individual window.
 
A window selection surface should clearly distinguish:
 
- active window;
- application;
- full display;
- virtual display.
 
## 4.7 Display Mirroring
 
Full-display mirroring should provide low-latency representation of the transmitting device.
 
Users must receive persistent mirroring indicators.
 
Sensitive system surfaces should be capable of:
 
- blocking capture;
- appearing blank;
- appearing obscured;
- requiring explicit confirmation.
 
## 4.8 Virtual Display Mode
 
Applications should be able to create a dedicated virtual display for the receiver.
 
This allows:
 
- presentation mode;
- speaker notes;
- extended workspaces;
- dashboards;
- media controls separate from media output;
- gaming controls separate from rendered output;
- television-specific layouts.
 
The transmitted interface therefore does not have to be identical to the originating display.
 
# 5. Audio Casting
 
GoreeCloud Cast should provide dedicated audio-routing capabilities independently from video.
 
Possible sources include:
 
- media playback;
- individual applications;
- entire device audio;
- microphone input where explicitly permitted;
- accessibility audio;
- notification audio where appropriate.
 
Users should be able to select:
 
**This device → Receiver**
 
or:
 
**Application audio → Receiver**
 
without changing unrelated audio routes.
 
# 6. Multi-Room Audio
 
A later GoreeCloud Cast release should support synchronized playback across multiple receivers.
 
Users should be able to create groups such as:
 
- Living Area
- Upstairs
- Entire Home
- Office
- Outdoor
- Custom Group
 
Group membership should be dynamically adjustable.
 
## 6.1 Synchronization Engine
 
The synchronization subsystem should continuously account for:
 
- receiver processing delay;
- network latency;
- clock differences;
- buffering;
- temporary packet loss;
- device performance differences.
 
Receivers should maintain a common presentation timeline.
 
The system should periodically correct drift without introducing distracting playback jumps.
 
## 6.2 Per-Receiver Delay Calibration
 
Advanced settings should allow receiver-specific delay adjustment.
 
Automatic calibration should be preferred where possible.
 
Manual correction should remain available for unusual hardware configurations.
 
## 6.3 Independent Volume
 
Grouped receivers should support:
 
- group master volume;
- individual receiver volume;
- mute per receiver;
- temporary receiver removal;
- room balance.
 
# 7. Multi-Display Casting
 
Receiver groups should eventually extend beyond audio.
 
Possible uses include:
 
- synchronized video walls;
- digital signage;
- presentations;
- dashboards;
- classroom displays;
- shared viewing;
- event displays;
- monitoring environments.
 
Multi-display operation should remain separate from ordinary household casting permissions because it introduces significantly broader control.
 
# 8. Device Discovery
 
## 8.1 Discovery Service
 
A system-level **GoreeCloud Cast Discovery Service** should discover compatible receivers available through authorized networks and proximity mechanisms.
 
Discovery should produce a normalized device description rather than exposing transport-specific implementation details to applications.
 
## 8.2 Device Information
 
A receiver may advertise:
 
- device identifier;
- user-visible name;
- device category;
- receiver capabilities;
- supported Cast modes;
- supported media characteristics;
- display characteristics;
- audio characteristics;
- current availability;
- trust status;
- ownership relationship;
- room or group;
- authorization requirements;
- whether confirmation is required;
- whether guest casting is available.
 
Sensitive information should not be unnecessarily broadcast during unauthenticated discovery.
 
## 8.3 Discovery Scope
 
Users should be able to control whether a receiver is:
 
- invisible;
- visible only to trusted devices;
- visible to household devices;
- visible to authorized network members;
- temporarily visible to guests.
 
## 8.4 Device Naming
 
Receiver names should be user-friendly.
 
Examples:
 
**Living Room Display**  
**Kitchen Speaker**  
**Office Computer**  
**Bedroom Display**
 
Technical identifiers should not be the primary names shown to ordinary users.
 
# 9. Capability Negotiation
 
Before a Cast session starts, the controller and receiver should negotiate capabilities.
 
The negotiation layer should determine:
 
- Cast mode;
- supported media format;
- supported resolution;
- supported frame rate;
- audio channel capabilities;
- subtitle capabilities;
- interactive control support;
- queue support;
- seek support;
- playback speed support;
- synchronization support;
- remote-control support;
- application receiver support;
- mirroring support;
- secure-content requirements.
 
Applications should receive a simplified capability model rather than manually negotiating network details.
 
# 10. Automatic Cast Mode Selection
 
GoreeCloud Cast should automatically determine the preferred Cast method.
 
A proposed decision sequence:
 
**Can receiver independently play the item?**
 
If yes:
 
→ hand off playback.
 
If no:
 
**Can the media be directly streamed?**
 
If yes:
 
→ direct media stream.
 
If no:
 
**Can the application expose a Cast-specific render surface?**
 
If yes:
 
→ application casting.
 
Otherwise:
 
→ offer display mirroring when permitted.
 
Users should still be able to override the automatic choice when multiple modes are appropriate.
 
# 11. GoreeCloud Cast Architecture
 
## 11.1 High-Level Architecture
 
```text
┌──────────────────────────────────────────────┐
│              GoreeCloud Applications        │
└──────────────────────┬───────────────────────┘
                       │
             GoreeCloud Cast API
                       │
┌──────────────────────▼───────────────────────┐
│            GoreeCloud Cast Service           │
│                                              │
│  Discovery                                   │
│  Capability Negotiation                      │
│  Session Management                          │
│  Trust and Permissions                       │
│  Playback State                              │
│  Queue Management                            │
│  Synchronization                             │
│  Transport Selection                         │
│  Receiver Management                         │
│  Diagnostics                                 │
└───────────┬─────────────────────┬────────────┘
            │                     │
    Local Transport        Optional Remote
            │                     │
┌───────────▼─────────────────────▼────────────┐
│           GoreeCloud Cast Receiver           │
│                                              │
│  Media Playback                              │
│  Audio Output                                │
│  Display Rendering                           │
│  Remote Controls                             │
│  Application Receiver                       │
│  Receiver UI                                 │
└──────────────────────────────────────────────┘
```
 
# 12. Cast Discovery Service
 
The Discovery Service should:
 
- advertise receiver availability;
- discover nearby receivers;
- deduplicate receiver identities;
- maintain device presence;
- monitor reachability;
- expose capability summaries;
- apply visibility policies;
- distinguish trusted and untrusted receivers;
- provide application-safe discovery results.
 
Applications should never need to implement their own network-scanning behavior for ordinary GoreeCloud Cast use.
 
# 13. Cast Session Manager
 
The **Cast Session Manager** should be the authoritative local coordinator for active sessions.
 
It should manage:
 
- session creation;
- session identifiers;
- participants;
- controllers;
- receivers;
- authentication;
- permissions;
- media metadata;
- playback state;
- queues;
- synchronization;
- reconnect tokens;
- controller migration;
- state persistence;
- graceful session termination.
 
# 14. Session Model
 
A Cast session should conceptually contain:
 
```text
CastSession
├── Session Identity
├── Initiating Application
├── Initiating User
├── Controller Devices
├── Receiver Devices
├── Cast Mode
├── Permissions
├── Media / Display Source
├── Playback State
├── Queue
├── Timeline
├── Capabilities
├── Security Context
├── Network Context
└── Recovery State
```
 
The session should exist independently enough that the original application interface can temporarily disappear without immediately destroying playback.
 
# 15. Cast Transport Layer
 
The Cast Transport Layer should abstract the underlying method used to deliver content.
 
Applications should request an experience:
 
**Cast this media item**
 
rather than:
 
**Open this network connection using this transport and encode it this way.**
 
The platform should choose the most suitable transport according to:
 
- content characteristics;
- receiver capability;
- latency requirements;
- network availability;
- security policy;
- quality preference;
- power constraints.
 
# 16. Adaptive Quality
 
GoreeCloud Cast should adapt to changing network conditions.
 
Possible adjustments include:
 
- resolution;
- frame rate;
- bitrate;
- buffer size;
- retransmission behavior;
- compression level;
- latency target.
 
The system should favor stable playback over continuously attempting unsustainable quality levels.
 
Users may optionally choose profiles such as:
 
- Automatic
- Prefer Quality
- Balanced
- Prefer Responsiveness
- Data Saver
 
Applications should normally use **Automatic**.
 
# 17. Session Persistence and Recovery
 
GoreeCloud Cast should tolerate temporary interruptions.
 
Recoverable events may include:
 
- controller application restart;
- controller screen lock;
- receiver interface restart;
- temporary network loss;
- receiver roaming;
- controller roaming;
- short power-management suspension.
 
A reconnecting participant should be able to securely rejoin the existing session where policy allows.
 
# 18. Controller Migration
 
A Cast session should not permanently belong to one controller.
 
Authorized users should be able to transfer control:
 
**Phone → Tablet**
 
or:
 
**Computer → Phone**
 
without restarting playback.
 
The receiver remains the active playback endpoint while the controlling interface changes.
 
# 19. Multiple Controllers
 
GoreeCloud Cast should support multiple authorized controllers for appropriate sessions.
 
Example:
 
A household media session may allow several trusted devices to:
 
- pause;
- resume;
- seek;
- skip;
- adjust volume;
- add queue items.
 
Permissions should determine whether every controller receives identical authority.
 
# 20. Collaborative Queues
 
Optional collaborative queues could allow multiple authorized participants to:
 
- add media;
- reorder entries;
- remove their entries;
- suggest content;
- vote on upcoming items;
- see who added an item.
 
The session owner should be able to disable collaboration.
 
# 21. Cast History
 
Cast history should be privacy-controlled.
 
Possible records:
 
- receiver used;
- application;
- media category;
- timestamp;
- duration;
- session outcome.
 
Media titles should not necessarily be stored unless required for a user-facing history feature.
 
Users should be able to:
 
- disable history;
- clear history;
- limit retention;
- exclude individual applications;
- exclude guest sessions.
 
# 22. Glaze UI Experience
 
GoreeCloud Cast should use Glaze UI as a core part of its identity.
 
The Cast interface should be visually polished while remaining immediately understandable.
 
Its visual hierarchy should emphasize:
 
**Content → Surface → Cast Controls**
 
Solid or softly tinted surfaces should carry content.
 
Translucent Glaze materials should primarily appear on:
 
- Cast selectors;
- floating controllers;
- menus;
- contextual controls;
- status surfaces;
- temporary prompts.
 
Transparency should never reduce readability.
 
# 23. Cast Symbol
 
A consistent Cast symbol should appear across GoreeCloud applications.
 
Its states should communicate:
 
- available;
- connecting;
- connected;
- actively casting;
- attention required;
- error.
 
State should never be indicated using color alone.
 
The symbol can combine:
 
- shape;
- emphasis;
- animation;
- semantic color;
- accessible text.
 
# 24. Cast Device Picker
 
Selecting the Cast control should open a Glaze device picker.
 
Proposed structure:
 
```text
╭────────────────────────────────────╮
│ Cast                               │
│                                    │
│ This Device                        │
│                                    │
│ Nearby                             │
│  Living Room Display         Ready │
│  Kitchen Speaker             Ready │
│  Office Display              Ready │
│                                    │
│ Groups                             │
│  Entire Home                 4     │
│                                    │
│ Manage Cast Devices               │
╰────────────────────────────────────╯
```
 
Each device should expose relevant state without overwhelming the user.
 
# 25. Device State Indicators
 
Possible states include:
 
- Ready
- Playing
- In Use
- Connecting
- Reconnecting
- Permission Required
- Confirmation Required
- Unavailable
- Unsupported
- Offline
- Limited Connection
 
Icons, text, and shape should reinforce the meaning.
 
# 26. Context-Aware Device Picker
 
The device picker should understand what the user is attempting to cast.
 
If casting audio, it should prioritize audio receivers.
 
If casting a video, display-capable receivers should appear first.
 
If mirroring, only compatible displays should be selectable.
 
Incompatible devices may be hidden or shown separately with a clear explanation.
 
# 27. Now Casting Surface
 
Once connected, the Cast control should expand into a persistent **Now Casting** surface.
 
Possible information:
 
```text
╭────────────────────────────────────╮
│ Living Room Display                │
│                                    │
│     [Artwork / Preview]            │
│                                    │
│ Current Media                      │
│ Application                        │
│                                    │
│      ◀      ▶/Ⅱ      ▶             │
│                                    │
│ ━━━━━━━━━●━━━━━━━━━━━━━━━━━━━━     │
│ 18:24                       52:10  │
│                                    │
│ Volume                             │
│ Queue                              │
│ Continue on…                       │
│ Stop Casting                       │
╰────────────────────────────────────╯
```
 
Controls should adapt to the media type and capabilities.
 
# 28. Persistent Cast Chip
 
Active Cast sessions should remain visible even after leaving the originating application.
 
A compact Glaze Cast chip may show:
 
**Living Room • Playing**
 
Selecting it should return to the system Cast controller.
 
The chip should be available through appropriate system surfaces without obstructing normal work.
 
# 29. Phone Interface
 
On smaller touch devices, frequently used controls should remain within comfortable reach.
 
Primary controls should favor the lower portion of the screen.
 
The device selector should preferably use a bottom-oriented Glaze surface rather than forcing important actions into difficult-to-reach top corners.
 
# 30. Tablet and Desktop Interface
 
Larger interfaces may expose:
 
- device sidebar;
- active session workspace;
- receiver inspector;
- queue;
- advanced playback controls;
- diagnostics where appropriate.
 
Multiple simultaneous Cast sessions should be easier to manage from larger displays.
 
# 31. Television and Large-Screen Interface
 
Large-screen receivers should use:
 
- oversized readable text;
- strong focus indicators;
- comfortable spacing;
- directional navigation;
- clear confirmation prompts;
- minimal required text entry;
- reduced visual clutter.
 
Critical actions must remain usable from viewing distance.
 
# 32. Motion
 
Glaze UI motion should reinforce Cast state transitions.
 
Examples:
 
- Cast icon transitions into an active state.
- Device row gently emphasizes when connection begins.
- Artwork visually transitions from controller to receiver representation during handoff.
- The controller condenses after the receiver becomes authoritative.
- Reconnection uses a subtle activity state instead of aggressive flashing.
 
Reduced-motion preferences must be respected.
 
# 33. Semantic Color
 
Cast status can use semantic color to distinguish:
 
- connected;
- active;
- warning;
- error;
- privacy-sensitive sharing.
 
Large surfaces should not become saturated simply because casting is active.
 
Color should primarily appear in:
 
- indicators;
- highlights;
- selected states;
- progress;
- status chips;
- focus rings;
- subtle ambient tint.
 
# 34. Accessibility
 
Accessibility is a requirement of GoreeCloud Cast, not an optional mode.
 
The interface should support:
 
- screen readers;
- keyboard navigation;
- directional remote navigation;
- touch;
- pointer input;
- switch-style input;
- scalable text;
- sufficient contrast;
- reduced motion;
- reduced transparency;
- high-contrast operation;
- visible focus;
- non-color-dependent status communication;
- accessible labels for every icon-only action.
 
Cast controls should remain usable when Glaze transparency and motion are substantially reduced.
 
# 35. GoreeCloud Cast Receiver
 
The **GoreeCloud Cast Receiver** is the receiving-side system service responsible for accepting and rendering Cast sessions.
 
Its responsibilities should include:
 
- discovery advertisement;
- pairing;
- trust verification;
- permission enforcement;
- capability publication;
- session acceptance;
- media playback;
- display rendering;
- audio rendering;
- playback controls;
- session recovery;
- receiver UI;
- telemetry and diagnostics where permitted.
 
# 36. Receiver Idle Experience
 
When not casting, a display receiver may show an optional Cast idle surface.
 
Possible information:
 
- device name;
- time;
- connection readiness;
- approved ambient artwork;
- pairing instructions;
- privacy mode;
- active network state.
 
The idle screen should avoid exposing sensitive account or network information to people physically near the device.
 
# 37. Incoming Cast Request
 
Untrusted or confirmation-required requests should trigger an explicit receiver prompt.
 
Example:
 
```text
╭──────────────────────────────────╮
│ Cast Request                     │
│                                  │
│ Personal Device wants to play    │
│ media on Living Room Display.    │
│                                  │
│        Deny       Allow          │
│                                  │
│ □ Trust this device              │
╰──────────────────────────────────╯
```
 
The prompt should identify:
 
- requesting device;
- requesting application where appropriate;
- requested capability;
- whether permanent trust will be granted.
 
# 38. Receiver Playback Experience
 
During media playback, the receiver should prioritize content.
 
Temporary controls can appear when interaction occurs.
 
The receiver may show:
 
- artwork;
- title;
- creator or source metadata;
- playback position;
- queue;
- subtitles;
- volume;
- connection status;
- controller identity;
- session participants.
 
Persistent overlays should be minimized.
 
# 39. Audio Receiver Experience
 
Receivers without a primary display should communicate state through available indicators and controller-side UI.
 
The controller should remain the primary interface for:
 
- track information;
- queue;
- volume;
- grouping;
- receiver status.
 
# 40. Receiver Privacy Mode
 
A receiver should be able to enter a privacy mode in which:
 
- discovery is restricted;
- guest requests are rejected;
- new pairing is disabled;
- remote Cast requests are blocked;
- existing sessions may optionally continue.
 
This can be temporary or persistent.
 
# 41. Security Model
 
GoreeCloud Cast should use a **zero-assumption trust model**.
 
Discoverability, identity, authentication, authorization, and session permissions must remain distinct concepts.
 
A device appearing on the network is not inherently trusted.
 
# 42. Device Identity
 
Each Cast-capable device should have a cryptographic device identity.
 
The identity should allow trusted peers to determine whether they are reconnecting to the same receiver they previously authorized.
 
Human-friendly device names should not be treated as identities.
 
# 43. Secure Pairing
 
Initial pairing should require a user-verifiable action.
 
Possible pairing methods include:
 
- matching short codes;
- entering a temporary code;
- approving an on-screen request;
- scanning a temporary visual pairing token;
- proximity-assisted confirmation;
- approval through an already trusted GoreeCloud device.
 
Pairing credentials must be revocable.
 
# 44. Session Credentials
 
Long-term device trust should not directly become a reusable Cast-session secret.
 
Each session should use temporary credentials derived specifically for that connection.
 
Compromise of one session should not automatically compromise future sessions.
 
# 45. Encryption
 
Control traffic, media transport where applicable, session state, authentication, and sensitive metadata should be protected against unauthorized observation or modification.
 
Local-first operation should not mean unprotected local traffic.
 
# 46. Permission Model
 
Suggested permission classes:
 
### Discover
 
Allows the device to see that a receiver exists.
 
### Request Cast
 
Allows the device to request a session.
 
### Media Playback
 
Allows media handoff or playback.
 
### Playback Control
 
Allows play, pause, seek, skip, and similar commands.
 
### Queue Control
 
Allows queue modification.
 
### Volume Control
 
Allows receiver volume adjustment.
 
### Audio Cast
 
Allows audio forwarding.
 
### Application Cast
 
Allows an application surface to be shared.
 
### Display Mirror
 
Allows the full display to be shared.
 
### Multi-Receiver Control
 
Allows receiver grouping and synchronization.
 
### Receiver Administration
 
Allows receiver configuration.
 
Administrative permission must remain distinct from ordinary Cast access.
 
# 47. Trust Levels
 
A proposed trust model could include:
 
## Owner
 
Full receiver management authority.
 
## Household / Trusted
 
Can Cast according to receiver policy with minimal prompts.
 
## Approved Device
 
Has explicitly granted permissions.
 
## Guest
 
Temporary permissions with automatic expiration.
 
## Untrusted
 
May only request access where receiver policy permits.
 
Applications should not invent their own incompatible trust levels.
 
# 48. Guest Casting
 
Guest Cast should permit temporary use without permanently trusting a device.
 
Possible flow:
 
1. Receiver enables Guest Cast.
2. Receiver displays a temporary pairing code.
3. Guest enters or scans the code.
4. Receiver grants limited temporary permissions.
5. Access automatically expires.
 
Guest permissions should normally exclude:
 
- receiver administration;
- permanent pairing changes;
- protected display mirroring;
- other users' active sessions;
- historical session data.
 
# 49. Sensitive Screen Protection
 
Display and application casting need stronger privacy rules than ordinary media handoff.
 
Protected surfaces should be able to declare:
 
- do not capture;
- obscure during capture;
- require confirmation;
- allow only trusted receivers.
 
Examples may include authentication interfaces, private credentials, security settings, and protected user information.
 
# 50. Persistent Privacy Indicators
 
When mirroring or capturing an application, the transmitting device must clearly indicate that capture is active.
 
The user should always have a readily available **Stop Sharing** action.
 
Applications must not be able to silently suppress this system indicator.
 
# 51. Notification Privacy
 
During display mirroring, users should be able to automatically:
 
- hide notification content;
- suppress banners;
- show generic notifications;
- disable notifications on the shared display.
 
Application-only casting should exclude unrelated notifications by default.
 
# 52. Microphone and Camera Isolation
 
Casting must not automatically grant microphone or camera access.
 
If an interactive receiver experience requires either source, the Cast session should request separate explicit permission.
 
Active capture must remain visibly indicated.
 
# 53. Remote Casting
 
Remote casting across different networks should be treated as a later capability with stricter controls than local casting.
 
Remote mode should require:
 
- authenticated user relationships;
- trusted devices;
- encrypted communication;
- explicit receiver policy;
- session authorization;
- clear local/remote indicators.
 
Receivers should be able to disable remote access completely.
 
# 54. Remote Relay Service
 
Where direct communication is impossible, an optional GoreeCloud relay service may assist communication.
 
The relay should be designed so that it receives only the minimum information necessary.
 
Direct secure communication should remain preferred when available.
 
# 55. Cast Policy Service
 
A centralized policy layer should govern Cast behavior.
 
Policies may include:
 
- who can discover a receiver;
- who can request sessions;
- whether approval is required;
- whether guests are permitted;
- whether mirroring is permitted;
- whether remote casting is permitted;
- maximum session duration;
- allowed application categories;
- network restrictions;
- receiver-specific controls.
 
# 56. GoreeCloud Cast Settings
 
A centralized settings interface should include sections such as:
 
## My Devices
 
View paired and trusted devices.
 
## Receiver Settings
 
Control whether the current device accepts Cast sessions.
 
## Visibility
 
Choose who can discover the device.
 
## Permissions
 
Review per-device permissions.
 
## Guest Cast
 
Enable or disable temporary guest access.
 
## Remote Cast
 
Control cross-network access.
 
## Groups
 
Create and manage receiver groups.
 
## History
 
Manage Cast activity history.
 
## Privacy
 
Control notification hiding, capture protection, and related safeguards.
 
## Advanced
 
Quality, latency, diagnostics, developer options, and receiver calibration.
 
# 57. Trust Management
 
Each trusted device page should show:
 
- device name;
- category;
- trust level;
- granted permissions;
- first paired date;
- most recent connection;
- whether remote access is permitted.
 
Users should be able to:
 
- change permissions;
- revoke trust;
- rename local representation;
- block the device.
 
# 58. Developer API
 
GoreeCloud Cast should provide a common developer interface so applications can integrate without understanding low-level discovery or network transport.
 
The developer surface should support both:
 
- controller applications;
- receiver applications.
 
# 59. Controller API
 
Applications should be able to:
 
- request Cast-capable devices;
- inspect normalized receiver capabilities;
- create sessions;
- hand off media;
- stream media;
- request application casting;
- request display mirroring;
- send playback commands;
- update metadata;
- manage queues;
- listen for state changes;
- transfer controller ownership;
- terminate sessions.
 
# 60. Media Descriptor
 
Applications should describe Castable content through a normalized media descriptor.
 
Conceptually:
 
```text
CastMedia
├── Identifier
├── Title
├── Subtitle
├── Artwork
├── Media Type
├── Duration
├── Playback Position
├── Content Source
├── Available Variants
├── Audio Tracks
├── Subtitle Tracks
├── Chapters
├── Application Metadata
└── Security Requirements
```
 
The descriptor should represent content intent rather than transport implementation.
 
# 61. Cast Request
 
A conceptual controller call could resemble:
 
```text
session = Cast.connect(receiver)

session.play(media)
session.pause()
session.seek(position)
session.setVolume(level)
session.moveTo(otherReceiver)
session.disconnect()
```
 
Exact implementation language and syntax should be defined separately.
 
The important requirement is a small, coherent conceptual model.
 
# 62. Session Events
 
Applications should be able to observe events such as:
 
```text
receiverConnected
receiverDisconnected
sessionStarted
sessionEnded
playbackChanged
positionChanged
queueChanged
capabilitiesChanged
controllerJoined
controllerLeft
permissionChanged
qualityChanged
errorOccurred
```
 
High-frequency events should be designed carefully to avoid unnecessary application overhead.
 
# 63. Receiver API
 
Applications implementing specialized receivers should be able to:
 
- advertise supported content;
- accept or reject sessions;
- expose playback controls;
- report playback state;
- report buffering;
- publish capabilities;
- handle queues;
- report errors;
- expose application-specific commands.
 
The platform should still retain authority over authentication and permissions.
 
# 64. Receiver Extensions
 
Applications may optionally provide richer receiver experiences.
 
Examples:
 
- specialized media playback;
- collaborative presentation tools;
- dashboards;
- interactive visualizations;
- game display modes.
 
Receiver extensions should operate inside a permission-controlled sandbox.
 
They should not independently bypass GoreeCloud Cast security or trust enforcement.
 
# 65. Application Metadata
 
Applications should be able to provide receiver-friendly metadata including:
 
- title;
- subtitle;
- artwork;
- chapter;
- creator;
- collection;
- content rating;
- playback state.
 
Only metadata necessary for the receiver experience should be transmitted.
 
# 66. Queue API
 
The queue interface should support:
 
- add;
- remove;
- move;
- replace;
- clear;
- skip;
- current item;
- next item;
- previous item.
 
Collaborative sessions should additionally identify the participant responsible for queue modifications where appropriate.
 
# 67. Capability API
 
Applications should be able to query normalized capabilities without depending on receiver-specific implementations.
 
Examples:
 
```text
receiver.supportsVideo
receiver.supportsAudio
receiver.supportsMirroring
receiver.supportsApplicationCasting
receiver.supportsQueue
receiver.supportsSeeking
receiver.supportsMultipleControllers
receiver.supportsGrouping
```
 
Detailed media capability data should also be available when necessary.
 
# 68. Permission API
 
Applications should request Cast capabilities through the platform.
 
Applications should not independently ask receivers for hidden privileges.
 
The platform should determine whether:
 
- permission already exists;
- system consent is required;
- receiver consent is required;
- access is prohibited.
 
# 69. Background Behavior
 
Applications should be able to declare whether a Cast session can continue when the application interface closes.
 
If the receiver independently owns playback, closing the controller should normally not terminate the media.
 
The user should remain able to return to the active session through the system Cast interface.
 
# 70. Cast Session Service API
 
Advanced applications may require session-level functions such as:
 
- attach to existing session;
- detach controller;
- migrate controller;
- inspect participants;
- inspect receiver group;
- request ownership;
- observe connection health;
- request reconnection.
 
These should remain subject to session authorization.
 
# 71. Diagnostics API
 
Development and troubleshooting interfaces should expose appropriate diagnostics such as:
 
- connection state;
- selected Cast mode;
- negotiated capabilities;
- latency;
- buffer health;
- synchronization drift;
- reconnect attempts;
- quality adaptations.
 
Diagnostics must avoid exposing secrets or unnecessary personal information.
 
# 72. Error Model
 
GoreeCloud Cast should use a consistent error model.
 
Possible categories:
 
- receiver unavailable;
- permission denied;
- receiver rejected;
- capability mismatch;
- unsupported media;
- connection lost;
- authentication failed;
- insufficient bandwidth;
- receiver busy;
- session expired;
- source unavailable;
- protected content cannot be shared;
- synchronization failure.
 
Errors should suggest recovery when possible.
 
# 73. Reliability Requirements
 
The platform should be resilient to:
 
- devices sleeping;
- devices waking;
- network roaming;
- temporary network partitions;
- receiver restarts;
- controller restarts;
- duplicated discovery announcements;
- delayed packets;
- out-of-order state changes;
- stale sessions;
- conflicting controllers.
 
# 74. State Authority
 
Every Cast session must have an explicit authority model.
 
For ordinary receiver-side media playback, the receiver should generally be authoritative for real playback state.
 
Controllers issue commands and receive state updates.
 
This prevents two controllers from independently believing different playback positions are correct.
 
# 75. Command Ordering
 
Commands should carry ordering information so delayed events do not overwrite newer state.
 
For example, an old pause message arriving after a newer resume command should not incorrectly stop playback.
 
# 76. Idempotency
 
Important Cast commands should be designed to safely tolerate retransmission.
 
Repeated receipt of the same command should not produce unintended repeated actions.
 
# 77. Observability
 
System diagnostics should provide visibility into:
 
- receiver discovery;
- connection success;
- connection failures;
- session duration;
- reconnection behavior;
- latency;
- synchronization drift;
- adaptation decisions;
- receiver crashes;
- permission failures.
 
User content should not be unnecessarily recorded as part of technical telemetry.
 
# 78. Privacy-Preserving Telemetry
 
Operational metrics should prefer aggregate technical information.
 
For example:
 
**Useful**
 
- session failed during capability negotiation.
 
**Usually unnecessary**
 
- exact title of the movie the user attempted to Cast.
 
Collection should follow GoreeCloud privacy requirements and remain proportionate to diagnostic needs.
 
# 79. Performance Targets
 
Final numerical targets should be established through testing, but development should optimize for:
 
- fast device discovery;
- low connection startup time;
- responsive playback controls;
- minimal controller battery usage;
- stable long-running sessions;
- low audio synchronization drift;
- responsive mirroring;
- efficient background operation.
 
# 80. Power Efficiency
 
GoreeCloud Cast should avoid constant high-frequency network activity when idle.
 
Discovery should adapt to:
 
- foreground activity;
- active Cast surfaces;
- current sessions;
- device power state;
- receiver role.
 
Independent receiver playback should be preferred partly because it allows the originating device to enter lower-power states.
 
# 81. Network Efficiency
 
When multiple devices request the same locally available content, the platform should avoid unnecessary duplicate transfer where safe and appropriate.
 
Multi-receiver architecture should be designed with bandwidth scaling in mind.
 
# 82. Offline Operation
 
Local Cast should continue working without external connectivity when:
 
- discovery remains available;
- devices can authenticate locally;
- content is locally accessible;
- receiver authorization does not require remote validation.
 
A temporary external outage should not automatically break an existing local Cast session.
 
# 83. Multi-User Devices
 
Shared receivers should distinguish user identity from device identity.
 
Policies may allow:
 
- any household user;
- selected users;
- owner only;
- guest access.
 
Playback history and personalized recommendations should not leak between users merely because they share a receiver.
 
# 84. Child and Restricted Profiles
 
Where GoreeCloud supports restricted user profiles, Cast permissions should respect those restrictions.
 
Potential controls include:
 
- allowed receivers;
- allowed content;
- maximum volume;
- remote Cast restrictions;
- guest restrictions;
- time restrictions.
 
The Cast service should not bypass upstream access-control decisions.
 
# 85. Enterprise and Managed Environments
 
Future managed-device policies may control:
 
- whether casting is enabled;
- approved receivers;
- approved networks;
- mirroring permission;
- remote casting;
- guest casting;
- receiver administration;
- logging requirements.
 
Personal and managed policy layers should remain distinguishable.
 
# 86. Initial Implementation Roadmap
 
## Phase 0 — Architecture and Security Foundation
 
Establish the service architecture before building broad media support.
 
Deliverables:
 
- Cast architecture specification;
- threat model;
- trust model;
- device identity model;
- session model;
- discovery protocol design;
- capability schema;
- permission model;
- transport abstraction;
- receiver interface;
- developer API draft;
- Glaze UI interaction prototype;
- error model;
- test architecture.
 
**Exit criterion:** two development endpoints can securely discover, authenticate, create a session, exchange state, and terminate that session through the common architecture.
 
## Phase 1 — Core Local Cast
 
Build the minimum useful product.
 
Capabilities:
 
- local receiver discovery;
- explicit pairing;
- trusted-device storage;
- single controller;
- single receiver;
- media handoff;
- remote play/pause;
- seeking;
- volume control;
- metadata transfer;
- basic queue support;
- disconnect;
- Cast device picker;
- Now Casting UI;
- receiver confirmation;
- basic reconnection.
 
**Goal:** dependable local media playback from one controller to one receiver.
 
## Phase 2 — Session Continuity
 
Expand the session model.
 
Capabilities:
 
- persistent sessions;
- application-independent system controller;
- controller reconnection;
- controller migration;
- multiple controllers;
- improved queue synchronization;
- Continue on…;
- receiver-to-controller state authority;
- stronger recovery after network interruption.
 
**Goal:** Cast feels like a persistent cross-device session rather than a fragile connection.
 
## Phase 3 — Audio Cast
 
Add generalized audio routing.
 
Capabilities:
 
- application audio casting;
- device audio casting;
- audio-only receivers;
- audio receiver controls;
- latency management;
- background operation.
 
**Goal:** make GoreeCloud Cast useful independently of video.
 
## Phase 4 — Application and Display Casting
 
Add interactive visual streaming.
 
Capabilities:
 
- application casting;
- window casting;
- full-display mirroring;
- virtual displays;
- adaptive quality;
- low-latency mode;
- notification privacy;
- protected surfaces;
- persistent privacy indicators.
 
**Goal:** securely support presentations, applications, and displays without weakening privacy.
 
## Phase 5 — Receiver Groups
 
Introduce synchronized multi-device playback.
 
Capabilities:
 
- audio groups;
- synchronization engine;
- drift correction;
- group volume;
- per-device volume;
- receiver calibration;
- dynamic group membership;
- persistent groups.
 
**Goal:** reliable synchronized multi-room playback.
 
## Phase 6 — Advanced Multi-Display
 
Expand grouping to visual receivers.
 
Capabilities:
 
- synchronized display groups;
- presentation groups;
- dashboards;
- signage;
- coordinated playback;
- advanced synchronization diagnostics.
 
## Phase 7 — Guest Cast
 
Add temporary access.
 
Capabilities:
 
- temporary pairing;
- expiring credentials;
- receiver approval;
- limited guest permissions;
- automatic session cleanup;
- administrator controls.
 
## Phase 8 — Remote Cast
 
Enable secure cross-network Cast.
 
Capabilities:
 
- trusted remote receivers;
- optional relay;
- remote discovery for explicitly trusted devices;
- strict remote permissions;
- remote connection indicators;
- revocation;
- session auditing.
 
Remote capability should ship only after local trust and recovery behavior is mature.
 
## Phase 9 — Developer Platform
 
Expand GoreeCloud Cast into a broad platform capability.
 
Deliverables:
 
- stable controller API;
- stable receiver API;
- application integration library;
- receiver extension model;
- sample integrations;
- compatibility test suite;
- developer documentation;
- automated Cast conformance tests.
 
## Phase 10 — Ecosystem Integration and Hardening
 
Integrate Cast consistently across appropriate GoreeCloud applications and system surfaces.
 
Focus areas:
 
- unified Cast iconography;
- consistent Continue on… behavior;
- centralized system Cast controller;
- shared permissions;
- shared device picker;
- unified settings;
- performance optimization;
- accessibility validation;
- security testing;
- recovery testing;
- long-duration session testing;
- multi-device interoperability testing.
 
# 87. Testing Strategy
 
GoreeCloud Cast should receive dedicated test suites for:
 
## Discovery Testing
 
- discovery;
- device disappearance;
- duplicate receivers;
- rapid network changes.
 
## Authentication Testing
 
- valid pairing;
- expired credentials;
- revoked trust;
- impersonation attempts;
- incorrect pairing codes.
 
## Permission Testing
 
- unauthorized controls;
- guest restrictions;
- mirroring restrictions;
- receiver policy changes.
 
## Session Testing
 
- controller disconnect;
- receiver disconnect;
- controller restart;
- receiver restart;
- multiple controllers;
- conflicting commands.
 
## Media Testing
 
- seeking;
- track changes;
- queue changes;
- subtitle changes;
- playback completion;
- unsupported media.
 
## Network Testing
 
- latency;
- packet loss;
- bandwidth reduction;
- connection switching;
- temporary outage.
 
## Synchronization Testing
 
- clock drift;
- mixed receiver latency;
- receiver joining;
- receiver leaving;
- long-running playback.
 
## Privacy Testing
 
- notification suppression;
- protected surfaces;
- application-only capture;
- permission revocation;
- sharing indicators.
 
## Accessibility Testing
 
- keyboard navigation;
- screen reading;
- remote navigation;
- text scaling;
- reduced motion;
- reduced transparency;
- high contrast.
 
# 88. Security Testing
 
Security validation should include:
 
- device impersonation attempts;
- unauthorized discovery;
- credential replay;
- session hijacking;
- controller impersonation;
- unauthorized receiver commands;
- guest privilege escalation;
- stale credential use;
- malicious receiver behavior;
- malicious controller behavior;
- malformed media metadata;
- denial-of-service resistance;
- protected-content bypass attempts.
 
# 89. Success Criteria
 
GoreeCloud Cast should eventually be considered successful when users can:
 
1. See an appropriate receiver quickly.
2. Understand whether that receiver is trusted.
3. Connect with minimal interaction.
4. Move playback without losing meaningful state.
5. Control the receiver naturally.
6. Leave the originating application without unnecessarily stopping playback.
7. Reconnect after brief network interruptions.
8. Clearly identify when screen or application sharing is active.
9. Revoke receiver or controller access easily.
10. Use the same Cast interaction model across compatible GoreeCloud applications.
 
# 90. Product Quality Principles
 
GoreeCloud Cast should feel:
 
**Immediate**  
Receivers appear and respond quickly.
 
**Predictable**  
The same actions behave consistently across applications.
 
**Persistent**  
Sessions survive normal device interruptions.
 
**Private**  
Users understand exactly what is being shared.
 
**Secure**  
Discovery never automatically grants control.
 
**Adaptive**  
The service chooses an appropriate delivery mode.
 
**Accessible**  
Every major capability is usable through accessible interaction methods.
 
**Native to GoreeCloud**  
Applications rely on one shared Cast system rather than implementing disconnected alternatives.
 
# 91. Future Possibilities
 
Potential later capabilities include:
 
- proximity-aware receiver suggestions;
- room-aware receiver recommendations;
- automatic handoff between personal devices;
- follow-me audio;
- follow-me video;
- temporary presentation rooms;
- shared household playback;
- collaborative media queues;
- synchronized event playback;
- device-to-device presentation control;
- remote support sessions;
- cross-device application continuation;
- persistent virtual workspaces;
- intelligent quality prediction;
- receiver health monitoring;
- administrator-controlled Cast zones.
 
These should remain future concepts until individually specified and approved.
 
# 92. Core Product Direction
 
GoreeCloud Cast should evolve into the **cross-device experience transport layer for the GoreeCloud ecosystem**.
 
Its purpose should extend beyond placing a video on another screen.
 
The long-term architecture should allow a GoreeCloud application to describe:
 
**what the user is doing, what state must move, what controls are available, and what permissions are required.**
 
GoreeCloud Cast should determine:
 
**where the experience can move, how it should be transported, how the receiving device should reproduce it, and how the session remains secure and synchronized.**
 
The ideal user experience is therefore not:
 
**“Mirror my device.”**
 
It is:
 
**“Continue this experience there.”**
 
That principle should guide the service architecture, Glaze UI experience, receiver design, security model, developer APIs, and implementation roadmap.

# 93. Experience Handoff Contract

GoreeCloud Cast should define a first-class **Experience Handoff Contract** so applications can move more than media URLs or pixels.

An application should be able to describe the transferable portion of an active experience through a normalized, versioned contract.

Conceptually:

```text
CastExperience
├── Experience Identity
├── Application Identity
├── Experience Type
├── User-Visible Title
├── Transferable State
├── Resource References
├── Required Capabilities
├── Optional Capabilities
├── Control Surface
├── Permission Requirements
├── Privacy Requirements
├── Security Requirements
├── Continuity Policy
├── Recovery Policy
└── Expiration / Revocation State
```

The contract should describe **intent and state**, not a particular network protocol.

Applications should transfer only the minimum state required to continue the experience. Unrelated application memory, private local state, credentials, hidden UI state, and unnecessary personal metadata must remain local unless explicitly required and authorized.

The contract should support application-defined extension fields through namespaced, versioned schemas without weakening the common platform model.

# 94. State Capsule

The transferable state for an experience should be packaged conceptually as a **State Capsule**.

A State Capsule may contain:

- playback position;
- selected item;
- queue state;
- navigation state;
- document or presentation position;
- selected view or mode;
- application-defined continuation state;
- temporary resource references;
- session-scoped control information.

A State Capsule should not automatically contain:

- reusable credentials;
- long-term authentication secrets;
- unrelated application databases;
- unrestricted filesystem access;
- hidden private state that is not required by the receiver.

State Capsules should be:

- versioned;
- integrity protected;
- bound to an authorized session;
- revocable where practical;
- scoped to intended receivers or receiver classes;
- understandable enough for diagnostics without exposing sensitive contents.

Where an application can reconstruct state from a durable source, GoreeCloud Cast should prefer references plus authorized retrieval over copying large private state blobs between devices.

# 95. Handoff Preflight

Before transferring an experience, GoreeCloud Cast should perform a unified **handoff preflight**.

The preflight should evaluate, as applicable:

- receiver reachability;
- receiver capability;
- application compatibility;
- user and device identity;
- session authorization;
- Privacy Shield authorization;
- Wardveil security posture;
- protected-content requirements;
- network suitability;
- power state;
- required local resources;
- optional cloud or remote dependencies;
- receiver availability;
- whether user confirmation is required.

The result should be explainable.

Instead of a generic failure such as **Cannot Cast**, the platform should be able to communicate reasons such as:

- Receiver does not support this experience.
- Approval is required on the receiver.
- Screen sharing is blocked for protected content.
- The receiver is offline.
- This experience requires a trusted device.
- Remote casting is disabled by policy.
- Required application support is unavailable on the receiver.

Applications should receive a normalized result rather than duplicating preflight logic.

# 96. GoreeCloud Cast Broker

A **GoreeCloud Cast Broker** should coordinate requests between applications, the Cast service, receivers, and applicable platform systems.

The broker should not become a new authority that replaces specialized GoreeCloud systems.

Its role should be to:

- normalize Cast requests;
- resolve candidate receiver capabilities;
- coordinate preflight evaluation;
- select an eligible Cast mode;
- establish the session;
- route state and commands;
- coordinate recovery;
- preserve authority boundaries;
- provide one consistent application-facing contract.

Identity remains authoritative for identity and authentication. Privacy Shield remains authoritative for privacy authorization. Wardveil remains authoritative for security posture and security policy. GoreeCloud Mesh remains the ecosystem coordination fabric. GoreeCloud Manager remains the administration plane. Everkeep remains the continuity authority. Glaze UI remains the shared experience system.

# 97. Transport Profile Registry

GoreeCloud Cast should maintain a versioned **Transport Profile Registry** describing platform-supported delivery patterns.

Profiles may include:

- receiver-native playback;
- direct media transfer;
- low-latency application streaming;
- application-rendered virtual display;
- full display mirroring;
- synchronized group audio;
- synchronized group video;
- remote direct connection;
- remote relay-assisted connection.

A profile should define its required capabilities, expected latency characteristics, security requirements, recoverability expectations, and whether the controller can safely disconnect.

Applications should not hard-code transport choices when a supported Cast profile can represent the experience.

# 98. Network Path Selection and Migration

The Cast service should be able to evaluate multiple authorized network paths without exposing transport complexity to applications.

Possible path classes may include:

- existing local network;
- direct device-to-device connectivity;
- GoreeCloud Mesh-mediated reachability where applicable;
- authenticated remote connectivity;
- optional relay-assisted connectivity.

Path selection should consider:

- policy;
- trust;
- latency;
- bandwidth;
- packet loss;
- power cost;
- receiver capability;
- privacy;
- security;
- connection stability.

Where practical, an active session should be able to migrate between compatible network paths without restarting the experience.

Examples include:

- Wi-Fi roaming between access points;
- controller network changes;
- switching from a relay path to a direct path;
- receiver movement between authorized networks.

Path migration must preserve session identity and must not silently broaden authorization.

# 99. Private Discovery Architecture

Discovery should reveal the minimum information necessary before trust is established.

GoreeCloud Cast should support privacy-preserving discovery techniques such as:

- minimal unauthenticated advertisements;
- ephemeral discovery identifiers;
- deferred capability disclosure;
- authenticated capability expansion;
- policy-filtered visibility;
- proximity- or network-scoped discovery where justified.

A device should not need to broadcast detailed ownership, room, account, application, or security information merely to announce that a Cast receiver exists.

After authentication and authorization, peers may reveal richer capability and identity information according to policy.

# 100. Integral Platform System Integration

GoreeCloud Cast should evaluate and integrate all seven Integral Platform Systems according to their authoritative responsibilities.

The planned integration model is:

```text
GoreeCloud Identity  → actor, device, session, and trust identity
Privacy Shield       → permitted data use and sharing authorization
Wardveil Security    → security posture, threat signals, and protection
Everkeep             → continuity, recovery, migration, and preservation
Glaze UI             → consistent user-facing Cast experience
GoreeCloud Mesh      → capability discovery and ecosystem coordination
GoreeCloud Manager   → administration, policy, inventory, and oversight
```

Integration should be substantive and evidence-backed. Documentation, badges, manifests, or UI labels alone must not be treated as implementation.

# 101. GoreeCloud Identity Integration

GoreeCloud Cast should rely on **GoreeCloud Identity** for identity-aware Cast operation where Identity is applicable and available.

Potential responsibilities include:

- user identity;
- device identity;
- receiver identity;
- controller identity;
- authentication;
- session identity claims;
- trusted-device relationships;
- household or organization membership;
- authorization context;
- credential lifecycle integration.

Cast-specific permissions should remain distinct from general account authentication.

A user being signed in should not automatically authorize:

- discovery of every receiver;
- control of every receiver;
- remote casting;
- display mirroring;
- receiver administration.

Local Cast must retain an approved local trust and recovery path for scenarios where remote Identity infrastructure is unavailable and policy permits offline use.

# 102. Privacy Shield Integration

**Privacy Shield** should govern privacy authorization for Cast operations that move or expose user information.

Privacy evaluation should be purpose-aware and capability-specific.

Examples include:

- media metadata disclosure;
- playback history;
- application-state transfer;
- notification suppression;
- display capture;
- microphone forwarding;
- camera forwarding;
- diagnostic telemetry;
- remote relay metadata;
- participant visibility.

Authorization should travel with the Cast operation and remain enforceable throughout the session lifecycle rather than being reduced to a one-time launch prompt.

A session should be able to respond to privacy changes such as:

- permission revocation;
- receiver trust reduction;
- application policy changes;
- user privacy-mode activation;
- data-sharing preference changes.

Where the authorization required for continued operation is withdrawn, Cast should stop, reduce capability, or re-negotiate according to policy rather than silently continuing under stale authority.

# 103. Wardveil Security Integration

**Wardveil Security** should provide Cast-specific security evaluation and protection where applicable.

Potential integrations include:

- receiver reputation and trust signals;
- malicious-controller detection;
- malicious-receiver detection;
- anomalous Cast requests;
- session-hijacking detection;
- replay detection;
- credential-abuse detection;
- denial-of-service protection;
- malformed payload detection;
- risky remote-path detection;
- policy enforcement for managed environments.

Wardveil signals may cause a session to be:

- blocked;
- challenged;
- restricted;
- re-authenticated;
- moved to a safer path;
- terminated.

Security actions should be visible and explainable to authorized users without exposing sensitive detection details unnecessarily.

# 104. Everkeep Integration

**Everkeep** should define continuity expectations for Cast configuration and recoverable user state.

Potentially recoverable information may include:

- trusted receiver relationships where policy allows;
- receiver groups;
- user-created room assignments;
- Cast preferences;
- receiver calibration;
- administrative Cast policies;
- application integration settings.

Ephemeral session secrets and expired temporary credentials should not be preserved as reusable recovery artifacts.

Recovery should distinguish between:

- configuration that should survive device replacement;
- trust that requires re-verification;
- session state that may be restored;
- security material that must be regenerated.

A restored Cast environment must not silently resurrect revoked trust or expired guest authority.

# 105. GoreeCloud Mesh Integration

**GoreeCloud Mesh** should coordinate GoreeCloud Cast as an ecosystem capability without replacing Cast's own receiver discovery or session semantics.

Mesh may provide:

- application capability registration;
- receiver-service capability publication;
- integration-contract discovery;
- application-to-Cast dependency relationships;
- event coordination;
- lifecycle coordination;
- compatibility information;
- cross-device service reachability where appropriate.

Cast should publish normalized capability contracts so GoreeCloud applications can discover supported handoff features without private point-to-point integration agreements.

Mesh reachability must not be treated as Cast authorization.

# 106. GoreeCloud Manager Integration

**GoreeCloud Manager** should provide the administrative control plane for GoreeCloud Cast.

Administrative surfaces may include:

- receiver inventory;
- receiver health;
- trust overview;
- group management;
- remote Cast policy;
- guest Cast policy;
- managed-network restrictions;
- application allow/deny policy;
- capability restrictions;
- diagnostic status;
- software and receiver version visibility;
- conformance and policy evidence.

Manager should aggregate authoritative state without replacing the systems that produced it.

A management dashboard must not display a Cast receiver as secure, private, compliant, healthy, or recoverable unless the relevant authoritative evidence supports that claim.

# 107. Glaze UI Platform Integration

The existing Cast UI should be implemented through approved **Glaze UI** components and contracts rather than creating a parallel visual system.

Reusable Cast patterns should be contributed back into the shared design system when they have ecosystem-wide value.

Candidate reusable components include:

- receiver rows;
- receiver capability badges;
- Cast chips;
- Now Casting surfaces;
- permission prompts;
- privacy-sharing indicators;
- transfer animations;
- remote-control panels;
- receiver-group controls;
- reconnection states.

The Cast experience must remain functional under reduced motion, reduced transparency, high contrast, large text, and non-pointer navigation.

# 108. GoreeCloud Sync Integration

**GoreeCloud Sync** is not an Integral Platform System, but it may support Cast continuity where durable cross-device state synchronization is useful.

Possible integrations include:

- queue synchronization;
- recent receiver preferences;
- non-sensitive Cast settings;
- handoff-ready application state;
- cross-device controller continuity.

Sync should not become a requirement for basic local Cast.

Sensitive session secrets, ephemeral pairing material, and privacy-restricted state should not be synchronized merely for convenience.

# 109. GoreeCloud Home and Location Context

Where authorized, **GoreeCloud Home** and **GoreeCloud Location** may provide optional contextual information that improves receiver selection.

Examples include:

- room association;
- household zones;
- device presence;
- proximity context;
- preferred room receiver;
- current-home versus remote-home distinction.

Contextual suggestions must remain optional and privacy-controlled.

Location data should not be required for ordinary receiver selection, and precise location should not be exposed to applications that only need a room or receiver-category decision.

# 110. GoreeCloud Notify Integration

**GoreeCloud Notify** may provide Cast-related notifications that remain useful after the initiating application leaves the foreground.

Examples include:

- receiver approval required;
- Cast session interrupted;
- receiver unavailable;
- guest session expiring;
- remote Cast request;
- session transferred to another controller;
- security or privacy action affecting a session.

Notifications should link directly to the relevant Cast control surface when possible and should avoid exposing sensitive media metadata on locked or shared devices unless policy permits it.

# 111. Media Application Integration

Compatible GoreeCloud media applications should use the shared Cast model instead of implementing independent casting stacks.

Planned integrations should be evaluated for applications such as:

- GoreeCloud Music;
- GoreeCloud Video;
- GoreeCloud Photos;
- GoreeCloud Gallery;
- GoreeCloud Browser;
- GoreeCloud Reader;
- GoreeCloud Documents.

Each application should expose only the Cast capabilities appropriate to its content.

Examples:

- Music may prefer receiver-native playback and synchronized audio groups.
- Video may prefer receiver-native playback with subtitle and track handoff.
- Photos and Gallery may expose slideshow and presentation modes.
- Browser may transfer media, tabs, supported web applications, or a controlled application surface.
- Reader may hand off reading position or supported presentation views.
- Documents may expose presentation, view-only, or controlled collaborative display modes.

# 112. Browser and Web Receiver Support

GoreeCloud Browser should be able to participate as both a Cast controller and, where appropriate, a controlled receiver surface.

Web-facing receiver support should use explicit GoreeCloud Cast APIs and sandbox boundaries rather than granting arbitrary web content unrestricted device-control authority.

Potential browser integrations include:

- media handoff from a tab;
- Continue on… for supported web applications;
- application-surface casting;
- browser-to-display presentation mode;
- secure receiver controls;
- web receiver extensions through the native GoreeCloud Browser extension/runtime model where separately approved.

A web page must not gain hidden Cast privileges merely because it is open in GoreeCloud Browser.

# 113. Protected Content and Rights Capability

GoreeCloud Cast should support a normalized protected-content capability model without embedding one provider's rights system into the platform architecture.

Content may declare requirements such as:

- trusted receiver only;
- encrypted output path;
- no mirroring;
- no recording;
- no screenshots;
- maximum output resolution;
- receiver-side entitlement verification;
- time-limited authorization.

The Cast platform should enforce these requirements through available platform capabilities and fail closed when a required protection cannot be established.

Applications should receive an explainable failure or fallback option rather than silently weakening content protection.

# 114. Session Evidence and Audit Model

Administrative and security-sensitive environments should be able to produce privacy-preserving evidence about Cast sessions.

Possible evidence fields include:

- session identifier;
- participating device identities;
- application identity;
- selected Cast mode;
- authorization result;
- policy decisions;
- security events;
- start and end time;
- recovery events;
- controller changes;
- termination reason.

Evidence should avoid recording unnecessary content titles, display contents, media payloads, or private application state.

The system should distinguish:

- operational diagnostics;
- security evidence;
- administrative audit records;
- optional user history.

These records may have different retention and privacy requirements.

# 115. Protocol and Schema Evolution

GoreeCloud Cast should be designed for compatibility across different software versions and device generations.

Every major protocol and schema should support explicit version negotiation.

Compatibility behavior should define:

- minimum supported version;
- optional capabilities;
- required capabilities;
- extension negotiation;
- deprecation behavior;
- safe fallback;
- unsupported-version errors.

A newer controller should not assume that an older receiver understands newly introduced commands.

Unknown fields should be handled according to the schema contract rather than causing unsafe interpretation.

# 116. Developer Conformance Kit

The GoreeCloud Cast developer platform should include an automated **Cast Conformance Kit**.

The kit should validate, as applicable:

- receiver discovery behavior;
- capability declarations;
- permission handling;
- session lifecycle;
- state authority;
- reconnect behavior;
- command ordering;
- idempotency;
- privacy indicators;
- protected-content handling;
- accessibility requirements;
- failure behavior;
- protocol-version negotiation;
- Integral Platform System declarations and evidence.

A receiver or application should not be considered conformant solely because it can connect to a test controller.

Conformance must evaluate behavior at the boundaries where privacy, security, recovery, and state correctness can fail.

# 117. Feature Maturity States

GoreeCloud Cast capabilities should carry explicit maturity rather than being treated as equally complete.

Suggested states include:

- Concept;
- Planned;
- Development;
- Experimental;
- Release Candidate;
- Stable;
- Deprecated;
- Retired.

Maturity should be tracked per capability where necessary.

For example, local media handoff could eventually be Stable while remote Cast remains Experimental.

The overall product must not imply that every documented capability is implemented merely because one subset has reached a higher maturity level.

# 118. Expanded Implementation Roadmap

The initial Phase 0 through Phase 10 roadmap should be extended with additional architecture and ecosystem phases.

## Phase 11 — Experience Handoff Contract

Deliverables:

- versioned CastExperience schema;
- State Capsule model;
- application extension namespace rules;
- handoff preflight contract;
- normalized failure reasons;
- application adapter guidance;
- state-minimization tests.

**Goal:** allow applications to transfer structured experiences instead of relying on media-only or pixel-only models.

## Phase 12 — Integral Platform System Integration

Deliverables:

- Identity integration contract;
- Privacy Shield authorization contract;
- Wardveil security contract;
- Everkeep recovery and migration contract;
- Mesh capability and event contract;
- Manager administration contract;
- Glaze UI reusable Cast component contract;
- conformance evidence model.

**Goal:** make GoreeCloud Cast a substantive member of the GoreeCloud platform rather than an isolated service with duplicated cross-cutting functions.

## Phase 13 — Cross-Application Handoff

Deliverables:

- media application integrations;
- Browser handoff support;
- Documents/Reader presentation and continuation support;
- reusable Continue on… integration library;
- application-state compatibility tests;
- protected-content capability negotiation.

**Goal:** make the same Cast interaction model useful across multiple GoreeCloud product categories.

## Phase 14 — Protocol Hardening and Conformance

Deliverables:

- protocol version negotiation;
- schema compatibility tests;
- automated Cast Conformance Kit;
- long-duration mixed-version testing;
- malicious participant testing;
- upgrade and rollback testing;
- capability maturity tracking;
- release evidence and acceptance criteria.

**Goal:** make Cast evolution predictable, testable, interoperable, and safe across device generations.

# 119. Next-Stage Success Criteria

In addition to the original product success criteria, the next architecture stage should be considered successful when:

1. An application can describe a transferable experience without selecting a transport.
2. A receiver can determine whether it can reproduce that experience before transfer begins.
3. The platform can explain why a handoff is permitted, restricted, or unavailable.
4. Privacy or security revocation can change an active session without relying on the originating application to enforce the decision.
5. A compatible session can survive controller replacement and network-path changes.
6. Different GoreeCloud applications can use the same Continue on… contract.
7. Platform-system integrations preserve their own authority rather than being reimplemented inside Cast.
8. Older and newer controllers and receivers can negotiate compatible behavior safely.
9. Receiver and application conformance can be validated automatically.
10. Drive, repository, task, changelog, and implementation state remain distinguishable and synchronized as the product evolves.

# 120. Expanded Product Direction

GoreeCloud Cast should ultimately become a **policy-aware, state-aware, transport-independent cross-device continuation platform**.

The long-term abstraction should be:

```text
Application Intent
      ↓
Transferable Experience
      ↓
Identity + Privacy + Security + Policy Preflight
      ↓
Eligible Receiver and Cast Mode
      ↓
State Capsule + Resource Access
      ↓
Receiver-Side Continuation
      ↓
Persistent Shared Session
```

This expands the original principle without replacing it.

The preferred user action remains:

**“Continue this experience there.”**

The platform-level interpretation becomes:

**“Move only the authorized state required to continue this experience on an eligible receiver, using the safest and most efficient available delivery model, while preserving user control, privacy, security, continuity, and explainable state.”**

That should become the architectural standard for future GoreeCloud Cast development.

# 121. Current Verified Implementation Boundary

As of September 16, 2026, GoreeCloud Cast has entered **Phase 0 Development** in the `GoreeCloud/goreecloud-cast` repository. This section records verified implementation progress without changing the governing rule that this specification alone is not implementation evidence.

The current Development work is held in draft pull request **#1**, `Phase 0: establish native Cast core foundation`, on branch `feature/phase0-core-foundation-20260916`. The current repository implementation version is **0.1.0**.

Verified implemented source scope includes:

- a native Rust core library for Cast domain contracts;
- bounded device and session identity value types;
- normalized capability representation and receiver-first Cast-mode selection;
- privacy-minimized unauthenticated discovery advertisements;
- a versioned and size-bounded State Capsule;
- State Capsule privacy classifications in which Restricted entries are never transferable by the core;
- explicit session state and state-authority types;
- fail-closed consumption of GoreeCloud Identity, Privacy Shield, and Wardveil Security gate decisions without replacing those authorities;
- policy-constrained local-first transport selection;
- unified handoff preflight and normalized preflight failures;
- executable contract tests;
- the required GoreeCloud repository documentation baseline; and
- a Contract 0.2 `goreecloud.platform.yaml` declaration that keeps incomplete Integral Platform System integrations blocked or migration-required.

Exact source revision `f165832a3e2e0be546415672a916f706e21890b8` passed GoreeCloud Cast Core CI run `35155854625`, including `cargo fmt --check` and `cargo test --all-targets`. The first CI attempt stopped on formatting drift before compilation; the reported rustfmt-only differences were corrected before the successful run.

The later documentation and governance reconciliation advanced the draft branch to exact head `fa45646852e42f282650629470c1b4c5458ada0d` while preserving the same bounded core behavior. GoreeCloud Cast Core CI run `35156090305` also passed `cargo fmt --check` and `cargo test --all-targets` on that exact current PR head. This strengthens current-head Development validation but does not establish runtime, production, release, or Stable acceptance.

This verified Development progress does **not** establish:

- cryptographic device identity;
- secure pairing;
- session credential derivation;
- encrypted network transport;
- replay protection;
- persistent trust or revocation storage;
- a controller runtime;
- a receiver runtime;
- media playback or streaming;
- application, window, or display capture;
- Glaze UI implementation;
- live Manager, Privacy Shield, Wardveil Security, Everkeep, Mesh, or Identity adapters;
- guest or remote casting;
- deployment;
- production acceptance;
- release; or
- Stable qualification.

The next bounded Phase 0 implementation increment should add cryptographic identity adapter interfaces, pairing and session-credential interfaces, deterministic protocol serialization, authenticated discovery-detail exchange, command ordering and idempotency primitives, and an in-memory controller/receiver handshake harness. These must remain distinguishable from production networking until runtime evidence exists.

# 122. Verified Phase 0 Protocol and Handshake Increment

As of September 16, 2026, the Phase 0 Development branch has advanced beyond the initial bounded core to implementation version **0.2.0** and Cast protocol version **0.2**. This section records verified repository evidence; it does not convert this Proposed / Planned roadmap into implementation authority.

The `0.2.0` increment added:

- device-identity signing and verification adapter contracts without embedding a cryptographic implementation;
- pairing authorization and opaque session-credential authority interfaces;
- authenticated receiver-detail models tied to rotating discovery identifiers;
- deterministic protocol `0.2` frames with bounded payloads and strict version and trailing-byte validation;
- typed deterministic serialization for authenticated receiver details and session opening;
- per-session command ordering and idempotency primitives, including duplicate recognition, conflicting-replay rejection, wrong-session rejection, out-of-order rejection, and sequence-exhaustion handling; and
- an in-memory controller/receiver handshake harness that orders identity verification before authenticated receiver-detail release, followed by pairing authorization, credential issuance/validation, protocol round trips, and session activation.

The first CI run for this increment, `35156893548`, stopped at `cargo fmt --check` because of rustfmt-only drift, so no test success was claimed from that run. The formatting changes reported by CI were applied without behavioral changes. Exact source revision `c421ce127059a0a1cd8ba33740e9c2188bbf58a3` then passed GoreeCloud Cast Core CI run `35157077714`, including `cargo fmt --check` and `cargo test --all-targets`. Repository/evidence reconciliation commit `55605c18c88d7daddd2a34f739518ee39eb46b70` also passed exact-head CI run `35157324634`.

This increment established Development source/test evidence for the protocol and handshake contracts only. It did **not** establish production cryptography, persistent trust, real network transport, production pairing, deployed platform adapters, production acceptance, release, or Stable qualification.

# 123. Verified Phase 0 Device Identity, Pairing, and Credential Security Increment

The next verified Phase 0 increment advances the repository implementation to **0.3.0** while keeping Cast protocol version **0.2**.

The `0.3.0` increment adds a concrete Development-grade device-identity cryptographic provider and bounded pairing/session-credential lifecycle semantics:

- `ed25519-dalek` is pinned exactly to version `3.0.0` as the first material third-party runtime dependency and is documented in the repository dependency record as a BSD-3-Clause foundational cryptographic dependency with upstream provenance, purpose, maintenance source, security/privacy boundary, and replacement considerations;
- `Ed25519DeviceSigner` signs domain-separated Cast challenge messages that bind the Cast `DeviceId`, challenge context, and 32-byte challenge nonce;
- `Ed25519DeviceVerifier` stores registered verification keys, rejects weak public keys, fails closed for unknown devices or malformed signatures, and uses strict Ed25519 verification;
- private signing key bytes are supplied by a higher-level key-management boundary; Cast does not yet define production key generation, secure storage, rotation, recovery, or revocation distribution;
- `PairingConfirmation` provides explicit Awaiting Confirmation, Confirmed, Denied, Cancelled, and Expired states; pairing requests have explicit deadlines, finalized/expired requests cannot be revived, and pairing grants must match the original controller/receiver binding; and
- in-memory session-credential leases provide explicit issue/expiry timestamps, revocation state, unknown-handle rejection, and binding-substitution rejection without being represented as a persistent production credential store.

Executable security-contract tests verify successful and tampered Ed25519 challenge behavior, fail-closed handling of unregistered devices, pairing expiration and finalization, pairing-grant binding checks, credential expiration, credential revocation, and session/controller/receiver binding isolation.

The first CI run for this increment, `35158343289`, stopped at rustfmt-only drift before tests. The exact formatting diff was applied without behavioral changes. Exact source revision `2bab9042542937efbf96fa9539031a3ba1c4ded9` then passed GoreeCloud Cast Core CI run `35158442444`, including formatting and all current tests. After repository documentation, dependency, roadmap, and Platform Contract evidence were reconciled, exact current draft PR head `15c61be84210458f59e3accc7488702591cbce5c` passed GoreeCloud Cast Core CI run `35158775373`, including `cargo fmt --check` and `cargo test --all-targets`.

Draft pull request **#1**, `Phase 0: establish native Cast core foundation`, remains open, draft, mergeable, and unmerged. Its current head is `15c61be84210458f59e3accc7488702591cbce5c`.

This verified Development progress does **not** establish:

- approved production device-key generation, secure storage, hardware-backed protection where applicable, rotation, recovery, or revocation distribution;
- a complete production pairing experience or pairing service;
- a persistent trusted-device store or revocation-safe restore path;
- encrypted/authenticated network transport;
- controller or receiver endpoint processes;
- complete replay protection across real transport, reconnect, restart, or recovery;
- deployed Manager, Privacy Shield, Wardveil Security, Everkeep, Mesh, or Identity adapters;
- Glaze UI implementation;
- media playback, streaming, capture, guest Cast, or remote Cast;
- deployment, production acceptance, release, or Stable qualification.

The next bounded Phase 0 implementation boundary should add an authenticated local frame-transport prototype carrying protocol `0.2` frames, a revocation-safe persistent trust-store interface and Development persistence harness, separate controller and receiver endpoint/process-level harnesses, credential/trust validation during establishment and recovery, and failure-mode tests for malformed frames, interrupted handshakes, trust revocation, credential revocation, restart, and recovery. Target-platform device-key storage and Integral Platform System runtime acceptance remain independent gates.
