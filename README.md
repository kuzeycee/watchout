WatchOut

A desktop app that tracks your blink rate in real time and reminds you to blink, look away, and sit back before digital eye strain kicks in.

The problem

After long screen sessions I get temporary blurry vision, sometimes I can't even read text a meter away from me. This is a known effect called digital eye strain. We normally blink 15-20 times a minute, but that drops to 5-7 times a minute when we're focused on a screen. Eye doctors recommend the 20-20-20 rule, every 20 minutes look at something 20 feet away for 20 seconds, but almost nobody actually remembers to do it. WatchOut automates that reminder.

What it does

WatchOut runs as a small widget that sits in the corner of your screen and watches your blink rate through your webcam. No images are ever saved, everything is processed frame by frame and discarded.

It uses MediaPipe Face Landmarker to detect eye landmarks and calculate a blink score in real time. If you go 8 seconds without blinking, a small red dot appears in the center of the screen. It has no text on purpose, reading a warning takes conscious attention which defeats the point of a low friction reminder, a small color cue in your peripheral vision is enough. It also warns you when you're leaning too close to the screen.

On top of that, it tracks low blink activity over a longer window and sends a real desktop notification following the 20-20-20 rule when it's actually time for a break.

There's also a simple session system, start a session when you begin working, pause it for breaks, end it to see a summary of total time, blinks, and warnings. The app has two modes, a small always on top widget icon, and a full dashboard that opens when you click it.

Why some of these choices

The 8 second threshold came from the fact that normal blink intervals are usually shorter than that, so the warning only fires when you're genuinely staring too long, not during normal reading. I used MediaPipe's blendshape scores instead of manually calculating Eye Aspect Ratio because it's Google's own trained model and worked more reliably in testing than my own EAR calculation. Electron was needed for the desktop shell because a browser tab can't keep running in the background once you switch to another app, and that persistence was the whole point.

Tech stack

HTML, CSS, JavaScript for the core app. MediaPipe Face Landmarker for face and eye tracking. Electron for the desktop packaging, window modes, and notifications.

Development notes

The web prototype, camera access, MediaPipe integration, blink detection logic, and session/threshold behavior were written and understood by me while learning HTML, CSS, and JavaScript from scratch during this hackathon. The Electron packaging was built with help from Claude as a coding assistant. I reviewed and understand that code and can walk through it.

Getting started
git clone https://github.com/kuzeycee/watchout.git
cd watchout
npm install
npm start

This opens WatchOut as a small widget in the top right corner. Click the icon to open the dashboard and start a session. You need Node.js, a webcam, and camera permission granted to the app.

What's next

See ideas.md for things I'd want to add later, like head-turn aware blink detection, long term eye health reports, a browser extension version, and self calibrating thresholds.

License

ISC
