# 🏠 Oslune — Smart Home Control Panel

![HTML](https://img.shields.io/badge/HTML5-E34F26?style=for-the-badge&logo=html5&logoColor=white)
![CSS](https://img.shields.io/badge/CSS3-1572B6?style=for-the-badge&logo=css3)
![JavaScript](https://img.shields.io/badge/JavaScript-ES6-yellow?style=for-the-badge&logo=javascript)
![Firebase](https://img.shields.io/badge/Firebase-Realtime%20DB-FFCA28?style=for-the-badge&logo=firebase&logoColor=black)
![Status](https://img.shields.io/badge/Status-Completed-success?style=for-the-badge)

**Oslune** is a minimal, single-file smart home control panel for toggling a connected IoT device (like an ESP32-driven bulb or relay) on and off. It syncs in real time with **Firebase Realtime Database**, so the switch instantly reflects the device's true state — whether it was changed from this panel, a physical device, or another client — all wrapped in a glowing, premium glassmorphism UI.

---

# 📑 Table of Contents

- Features
- Live Demo
- Technologies
- Project Structure
- How It Works
- Configuration
- Installation
- Security Notes
- Future Improvements
- Contributing
- License
- Author

---

# ✨ Features

✅ Large iOS-Style Power Toggle — smooth, spring-animated switch to control the device

✅ 🔥 Firebase Realtime Sync — listens on `bulb/state` and updates instantly across every connected client

✅ 🔄 Optimistic UI with Auto-Revert — the switch updates immediately on tap, and rolls back automatically if the write to Firebase fails

✅ 🎨 Reactive Glow Feedback — the whole card and toggle glow green when on, red when off

✅ 🪟 Premium Glassmorphism Design — blurred glass card, gradient edge highlight, and a soft ambient background

✅ ☁️ Cloud Status Badge — subtle "cloud · realtime" indicator with a live pulse dot

✅ Zero Custom Backend — Firebase Realtime Database handles all sync logic, no server code to maintain

✅ Single-File Simplicity — the entire app lives in one `index.html`, easy to read, tweak, and deploy anywhere

---

# 🚀 Live Demo

https://dhruvpandit46.github.io/Test_Home/

---

# ⚙ Technologies Used

- HTML5
- CSS3 (glassmorphism, gradients, custom toggle animation, radial background)
- JavaScript (Vanilla, ES6)
- Firebase Realtime Database (v8 SDK)
- Font Awesome (icons)
- Google Fonts (Inter)

---

# 📂 Project Structure

```
Test_Home/
│
├── index.html
├── logo.png
└── README.md
```

---

# ⚡ How It Works

1. On load, the app initializes the **Firebase v8 SDK** and attaches a real-time listener to the `bulb/state` path in Realtime Database.
2. Whenever that value changes — from this panel, a physical device (e.g. ESP32), or any other connected client — the toggle position, status text, and glow colors update automatically.
3. Flipping the switch triggers an **optimistic UI update** immediately, then writes the new boolean value to `bulb/state` via `stateRef.set(newState)`.
4. If the write fails (e.g. network issue), the app re-reads the last known value from Firebase and **reverts the toggle** to stay consistent with the actual device state.
5. The card's glow and border color shift to **green** when the device is on and **red** when off, giving instant visual feedback beyond just the switch position.

---

# 🔧 Configuration

The Firebase project config lives directly inside the inline script in `index.html`:

```js
const firebaseConfig = {
  apiKey: "YOUR_API_KEY",
  authDomain: "your-project.firebaseapp.com",
  databaseURL: "https://your-project-default-rtdb.firebaseio.com",
  projectId: "your-project",
  storageBucket: "your-project.firebasestorage.app",
  messagingSenderId: "...",
  appId: "...",
  measurementId: "..."
};
```

To connect this panel to your own device:

1. Create a Firebase project and enable **Realtime Database**.
2. Replace `firebaseConfig` with your project's config (from Firebase Console → Project Settings).
3. Have your microcontroller (e.g. ESP32) read/write a boolean at the same path — `bulb/state` by default — to mirror this panel.
4. Update the `.device-name` text (`ANIQUE`) and `stateRef` path in the script if you're naming or structuring your device differently.

---

# 📦 Installation

Clone the repository

```bash
git clone https://github.com/dhruvpandit46/Test_Home.git
```

Go inside the project

```bash
cd Test_Home
```

Run

Simply open `index.html` in your browser. No build step, no dependencies — just make sure `firebaseConfig` points to a valid, reachable Firebase project.

---

# 🔒 Security Notes

- A Firebase Web API key is safe to expose in client-side code by design — it identifies your project, it doesn't grant access on its own.
- **Actual protection comes from your Firebase Realtime Database security rules.** Make sure `bulb/state` (or whatever path you use) isn't left open with default `.read`/`.write: true` rules, or anyone with your config can read and flip your device's state.
- Consider adding **Firebase Authentication** (even anonymous auth) and rules that require an authenticated request before writes are allowed.

---

# 🎯 Future Improvements

- Firebase Authentication before allowing toggles
- Support for multiple devices/rooms under one dashboard
- Scheduling / timer-based automation via Cloud Functions
- Connection-lost indicator when Firebase is unreachable
- Historical on/off activity log
- Light/dark theme toggle

---

# 🤝 Contributing

Contributions are welcome.

1. Fork the repository
2. Create your feature branch
3. Commit your changes
4. Push your branch
5. Open a Pull Request

---

# 📜 License

Licensed under the **MIT License**.

MIT © 2026 Dhruv Pandit.

See the [LICENSE](LICENSE) file for full license details.

---

# 👨‍💻 Author

**Dhruv Pandit**

GitHub — https://github.com/dhruvpandit46

LinkedIn — https://linkedin.com/in/dhruv-pandit-755786326

Instagram — https://instagram.com/dhruv_pandit2007

---

# ⭐ Support

If you found this project useful, please consider giving it a ⭐ on GitHub.
It helps support future development.
