# Silent Notes

**Serverless, encrypted, and real-time markdown note sharing.**

**Silent Notes** is a lightweight, single-file web application (`index.html`) that allows you to write Markdown notes, encrypt them client-side, and share them instantly via URL or QR code.

No database. No accounts. No server-side storage. All state is managed within the URL hash.

## Key Features

- ✅ **Zero Backend:** The entire app lives in a single HTML file. Data never leaves your browser unless it is encrypted in the URL.
- ✅ **Client-Side Encryption:** Protect your notes with **AES-256** encryption (via CryptoJS) before sharing.
- ✅ **Real-Time P2P Collaboration:** Share a "Live" link to collaborate or present notes in real-time between browsers (using WebRTC/PeerJS).
- ✅ **Markdown Support:** Clean editor with instant live preview.
- ✅ **Mobile Friendly:** Generate QR Codes instantly for easy sharing to mobile devices.
- ✅ **URL Compression:** Uses LZ-String to compress data, allowing for longer notes to be stored in the URL.
- ✅ **Dark Mode:** Automatic system theme detection with a manual toggle.

## Getting Started

There is no installation required. It is a single file.

1. Download `index.html`.
2. Open it in any modern web browser (Chrome, Firefox, Edge, Safari).
3. Start typing!

## Usage Guide

### 1. The Interface

The interface features a split-pane view: Editor on the left, Markdown Preview on the right. The URL updates automatically as you type (compressed).

*(The URL bar contains your data. Copy it to save your note.)*

### 2. Password Protection

If your note contains sensitive data, **encrypt it**:

1. Click the **Lock (🔒)** icon in the toolbar.
2. Set a password.
3. The URL will update to an encrypted payload.
4. A green **SECURE** badge will appear.

Anyone opening the link must enter the password to decrypt and view the content.

### 3. Real-Time P2P Sharing

Collaborate or present your note live without storing data on a server:

1. Click the **P2P (📡)** button.
2. The app generates a unique Peer ID and copies a "Live Link" to your clipboard.
3. Send this link to a friend or colleague.
4. When they open it, a direct **WebRTC connection** is established. Edits are synced instantly.

*Note: If encryption is active, P2P data is also sent encrypted. The guest must know the password to view the live stream.*

### 4. QR Code Sharing

Quickly transfer a note from desktop to mobile:

1. Click the **QR (📱)** button.
2. Scan the code with your phone camera.

## Technical Details

This project is a **Single Page Application (SPA)** that relies entirely on client-side JavaScript.

### How it works

* **Storage:** Data is compressed using `LZString` and stored in the URL hash (`#lz=...` or `#enc=...`). This allows the URL to act as the database.
* **Encryption:** When a password is set, the content is encrypted using `AES` via `CryptoJS`. An HMAC signature is added to verify integrity.
* **Networking:** `PeerJS` is used to broker WebRTC connections. A public STUN server is used to establish the handshake, but the data stream is peer-to-peer.

### Libraries Used (CDN)

* [Marked.js](https://marked.js.org/) - Markdown parsing.
* [Crypto-js](https://github.com/brix/crypto-js) - AES Encryption & HMAC.
* [LZ-String](https://github.com/pieroxy/lz-string) - URL Compression.
* [PeerJS](https://peerjs.com/) - WebRTC wrapper for P2P networking.
* [QRCode.js](https://davidshimjs.github.io/qrcodejs/) - QR Code generation.

> [!WARNING]
> Since this is a client-side application with no backend storage:
> 1. **If you lose the URL, you lose the note.**
> 2. **If you forget the password for an encrypted note, it cannot be recovered.** There is no "Forgot Password" feature.

## License

This project is open source and available under the [BSD-3 License](./LICENSE).
