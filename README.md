# Qwen-Style AI Chatbot

> This is the official repo of Project Sampaguita.

A complete, working AI chatbot web app inspired by chat.qwen.ai — in a single `index.html` file.

No build step. No API key. No backend. Just open it and chat.

> Built-in local mock reply engine guarantees every message gets a smart-looking reply, fully offline.

## ✨ Features

**Sidebar chat list**
- New Chat button
- Search chats
- Pinned / recent chat list with auto-titles from first message
- Rename, delete, and clear-all chats
- Collapsible on mobile

**Header with model picker**
- Model dropdown like Qwen: `Qwen-Max`, `Qwen-Plus`, `Qwen-Turbo`, `Qwen-VL`
- Each model shows a short capability description
- Theme toggle (dark / light)
- Clear chat button

**Message thread**
- Clean Qwen-style bubbles: user right, AI left with avatar
- Typing indicator (three-dot animation)
- Auto-scroll to latest message
- Timestamps, copy button on AI messages
- Welcome / empty-state with suggestion prompts
- Markdown-lite rendering (code blocks, bold, inline code, line breaks)

**Composer**
- Auto-growing textarea (Enter to send, Shift+Enter for newline)
- Send / Stop button
- Live character counter (`#count` below the input): always shows the current input length as `N characters`, updates as you type, and resets to `0 characters` after send
- Quick suggestion chips

**Local mock reply engine**
- Works 100% standalone — no fetch, no API key
- Keyword-aware replies: greetings, who-are-you, help, code, python/javascript examples, weather, joke, time/date, math
- Typing simulation with word-by-word streaming effect
- Context-aware: uses your name if you tell it, remembers message count
- Fallback smart echo with helpful follow-ups

## 🌙 Dark mode

- **Toggle:** click the 🌙/☀️ button (`#themeBtn.themebtn`) in the header next to the model picker to switch the whole page between light and dark themes — sidebar, header, thread, bubbles, and composer all switch together.
- **How to try it:**
  1. Open `index.html` (defaults to dark on first visit, button shows 🌙).
  2. Click the theme button once for light (button shows ☀️).
  3. Reload the page — your choice is remembered.
  4. Click again to go back to dark.
- **Persistence:** your choice is saved in `localStorage` key `fable_theme` (separate from chat history in `fable_chats`) and restored on every load via `applyTheme(getTheme())`, including an early `<script>` in `<head>` that applies the saved theme before first paint (no flash). It persists across reloads/sessions.
- **Implementation:** theming uses CSS variables on `:root,[data-theme="dark"]` for dark (default) plus `[data-theme="light"]` overrides for light, with `color-scheme` set per theme and smooth transitions. Button has `title` + `aria-label` for accessibility (label updates to `Switch to dark / light mode`).
- Existing features (chats, model picker, composer, mock replies) are unaffected — only colors change.

## 🚀 Usage

### Option 1: Open locally
1. Download or clone this repo:
   ```bash
   git clone https://github.com/jepongspideymuse/qwen-style-ai-chatbot.git
   cd qwen-style-ai-chatbot
   ```
2. Just open `index.html` in any browser:
   - Double-click `index.html`, or
   - `npx serve .` then visit the URL

### Option 2: GitHub Pages
1. Go to repo Settings → Pages
2. Source: Deploy from branch → `main` / `(root)`
3. Open `https://jepongspideymuse.github.io/qwen-style-ai-chatbot/`

### Option 3: Any static host
Upload `index.html` to Vercel, Netlify, Cloudflare Pages — no config needed.

## 📁 Project Structure

```
qwen-style-ai-chatbot/
├── index.html  # Complete app: CSS + HTML + JS in one file
└── README.md   # This file
```

## 🧠 How it works

- All state lives in memory + `localStorage` (chat history persists across reloads where allowed).
- `mockReply()` function inspects the user message for keywords and returns a relevant formatted reply.
- Streaming effect is simulated word-by-word with a stop button.
- Model picker changes the AI avatar label and reply tone prefix — no API needed.

To connect a real API later, replace `mockReply()` with a `fetch()` to your LLM endpoint.

## 📄 License

MIT — free to use, remix, and ship.
