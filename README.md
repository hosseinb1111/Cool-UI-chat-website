# ✨ Cosmic Chat 3000

A single-file, real-time chat app with a pop-art light theme and a cyberpunk dark theme. No build step, no backend to write — just open the HTML file.

## Features

- 🔴 **Real-time messaging** powered by Supabase (Postgres + Realtime)
- 🌗 **Two themes**: hot-pink pop-art (light) and neon matrix cyberpunk (dark), toggle persists via `localStorage`
- 💬 Replies, edits, deletes, and emoji reactions (🔥 / 💀)
- 🧩 Message grouping by sender + date separators (Today / Yesterday / date)
- 🟢 Live connection status indicator
- 📱 Responsive layout for mobile
- 🚀 Inline SVG favicon — no extra asset files

## Getting started

1. Create a `messages` table in your Supabase/Base project with at least:
   - `id` (primary key)
   - `username` (text)
   - `content` (text)
   - `reactions` (jsonb, e.g. `{"🔥": 0, "💀": 0}`)
   - `reply_to` (jsonb, nullable — `{ id, username, snippet }`)
   - `created_at` (timestamp, default `now()`)
2. Enable Realtime on the `messages` table (INSERT / UPDATE / DELETE).
3. Update the `baseUrl` and `supabaseKey` constants in the `<script type="module">` block with your own project credentials.
4. Open `cosmic-chat.html` in a browser — that's it, no build tools required.

## Tech stack

- Vanilla HTML / CSS / JS (ES modules)
- [Supabase JS client](https://supabase.com/docs/reference/javascript) for data + realtime subscriptions
- Google Fonts: Rubik & Space Mono

## License

This project is licensed under the MIT License.

```
MIT License

Copyright (c) 2026 Cosmic Chat Contributors

Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
in the Software without restriction, including without limitation the rights
to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
copies of the Software, and to permit persons to whom the Software is
furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all
copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE
SOFTWARE.
```
