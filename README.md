# Haven Room

A static, GitHub Pages–ready video room in the spirit of VDO.Ninja. Up to **10 people**, timed sessions, host handoff, local recording, and an ALS-friendly type-to-speak panel.

**Ship only `index.html`.** CSS and JavaScript are already inside that file. Media travels peer-to-peer (WebRTC). Signaling uses the public PeerJS cloud, so you do not need your own server.

## Features

- Camera + microphone grid for up to 10 participants
- Host a room with a length of 15–120 minutes; remaining time can be reset by the host
- Pass the host role to someone else, lock the room, or end the meeting for everyone
- Record on your own device: meeting composite, screen/window, or audio only
- ALS / AAC panel: type a phrase, speak it to the room (text-to-speech on every device + caption)
- One-tap **Repeat last** and recent-phrase chips, plus a personal quick-phrase bank
- Invite link with room code (`#r=your-code`)
- Layout tuned for desktop and phones (bottom dock, slide-up speak panel)

## Deploy on GitHub Pages

1. This repo already has `index.html` at the root.
2. **Settings → Pages → Deploy from a branch → `main` / root**.
3. After a minute, open `https://tbenitz.github.io/haven-room/`.
4. Pages is HTTPS, which browsers require for camera and mic.

## How to use

**Host**

1. Enter your name, optional title, optional room code, and length.
2. Create room and allow camera / mic.
3. Copy invite and send it. The link already includes the room code.

**Join**

1. Open the invite or type the room code.
2. Allow camera / mic.

**ALS speak panel**

- Type in the large box. **Enter** speaks to the room; **Shift+Enter** adds a line.
- **Speak to room** plays the phrase on every participant’s device and shows a caption.
- **Repeat last** and the gold chips replay recent phrases without retyping.
- Save personal phrases at the bottom. They stay in that browser.

**Record**

Recordings never upload. Use composite for a grid file, screen capture for the full chrome, or audio only for a small voice file.

## Limits (honest)

- Full-mesh WebRTC: each person sends video to each other person. Ten is the cap on purpose. Use Wi-Fi, not a weak hotspot, when several cameras are on.
- Some corporate firewalls block peer-to-peer. This build uses public STUN only (no TURN relay), so a few networks will fail to connect.
- Signaling depends on `0.peerjs.com`. If that service is down, rooms will not form even though the file is on GitHub.
- Text-to-speech uses the browser’s `speechSynthesis` voices. Quality varies by OS.
- GitHub Pages cannot keep a room alive by itself. The **host tab** must stay open for new people to join. After a host handoff, existing peers stay connected; new joins still go through the original host tab if it is open.

## Local preview

Camera access on `file://` is unreliable. From the folder that contains `index.html`:

```bash
python3 -m http.server 8080
```

Then open `http://localhost:8080`.

## Stack

One HTML file. [PeerJS](https://peerjs.com/) from a CDN. No build step, no accounts, no backend of yours.
