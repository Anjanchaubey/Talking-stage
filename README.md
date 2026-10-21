# BATTALK

BATTALK is a lightweight, anonymous voice-room website. Visitors can browse live channels, create or join a room, share an invite link, and use reactions while talking.

## Features

- Anonymous display identities generated in the browser.
- Open and password-protected rooms, with a maximum of eight participants.
- WebRTC audio with public STUN/TURN configuration.
- Shareable room links. Open rooms join directly; locked rooms still require the room password.
- Host controls to hand over ownership, remove members, leave a room open, or close it for everyone.
- Host refresh recovery and a three-minute host-offline grace period for room listings.
- Installable PWA with app icons and a cached app shell.

## Run Locally

No build step or package installation is required. From the project directory, run:

```powershell
py -m http.server 8000
```

Then open <http://localhost:8000>. Use `localhost` or HTTPS for microphone access; browsers restrict microphone access on ordinary HTTP sites.

## Deploy

The site is a static website. The included `netlify.toml` configures Netlify to publish the repository root, where `index.html` is located. Connect the repository to Netlify and deploy the `main` branch, or upload the project files to another static host. Use HTTPS for microphone access, service workers, and PWA installation.

## Install

- **iPhone/iPad:** Open the HTTPS site in Safari, tap Share, then choose **Add to Home Screen**.
- **Windows:** Open the HTTPS site in Microsoft Edge or Chrome and choose the browser's **Install app** option.

## Rooms and Availability

Room signaling and the live directory use public MQTT brokers. The directory keeps a retained listing for up to three minutes after the host stops refreshing it. Refreshing the host's tab can restore the room from that tab's session; an intentional host close removes the listing. Guests do not become host automatically. The room needs a connected host to continue audio; the directory grace period does not keep a host's microphone or WebRTC connection running while their browser is closed.

The app tries two public MQTT brokers, but availability and connection speed depend on those third-party services and the visitor's network. WebRTC calls can also fail on restrictive networks despite the configured ICE servers.

## Privacy Note

The app does not require account registration. Room signaling passes through public MQTT brokers, and public channel listings are visible to users of the app. Do not share sensitive personal information in rooms. A locked-room password is not included in invite URLs.
