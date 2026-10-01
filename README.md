# ✨ Cosmic Chat 3000

A single-file, real-time chat room with a pop-art light theme and a cyberpunk dark theme. No build step and no server code to write: add your Supabase details and open `index.html`.

## Features

- 🔴 **Real-time messaging** with Supabase (Postgres + Realtime)
- 🌗 **Two themes**: hot-pink pop-art and neon matrix cyberpunk. The first visit follows your system setting, then your choice is remembered
- 💬 **Replies, edits, deletes and reactions** (🔥 / 💀). Click a reply preview to jump to the original message
- 🧩 **Smart grouping**: consecutive messages from one person within five minutes collapse together, with Today / Yesterday / date separators
- 🟢 **Live status, online count and typing indicator**
- ⤵️ **"N new" jump button** when messages arrive while you are scrolled up, plus an unread count in the tab title
- ♻️ **Self-healing connection**: after a dropped connection it re-syncs missed messages, edits and deletes
- 📜 **History paging**: loads the latest 100 messages, with "Load earlier messages" for the rest
- 🔗 **Safe links**: URLs in messages become clickable, and message text is never parsed as HTML
- ✍️ **Better composer**: auto-growing box, character counter, restores your text if sending fails
- 👾 **Pick and change your callsign** in a proper dialog instead of a browser prompt
- ♿ **Accessible**: keyboard focus styles, labelled controls, live regions, reduced-motion support
- 📱 **Responsive** down to small phones

## Getting started

1. Create a [Supabase](https://supabase.com) project and run this in the SQL editor:

   ```sql
   create table public.messages (
     id         bigint generated always as identity primary key,
     username   text        not null check (char_length(username) between 1 and 15),
     content    text        not null check (char_length(content) between 1 and 1000),
     reactions  jsonb       not null default '{"🔥": 0, "💀": 0}',
     reply_to   jsonb,
     created_at timestamptz not null default now()
   );

   alter table public.messages enable row level security;

   create policy "anyone can read"   on public.messages for select using (true);
   create policy "anyone can post"   on public.messages for insert with check (true);
   create policy "anyone can edit"   on public.messages for update using (true);
   create policy "anyone can delete" on public.messages for delete using (true);

   alter publication supabase_realtime add table public.messages;
   ```

2. In **Project Settings → API**, copy your project URL and the `anon` (public) key.
3. Open `index.html` and fill in the `CONFIG` block at the top of the `<script type="module">`:

   ```js
   const CONFIG = {
       SUPABASE_URL: 'https://YOUR-PROJECT-REF.supabase.co',
       SUPABASE_ANON_KEY: 'YOUR_SUPABASE_ANON_KEY',
       ...
   };
   ```

4. Open `index.html` in a browser, or host it anywhere static (GitHub Pages works great).

Until the config is filled in, the app shows a setup screen instead of failing silently.

> Never put the `service_role` key in this file. Only the `anon` key belongs in a browser.

## Good to know

Cosmic Chat has **no accounts**. A name is just a label, so:

- Anyone can choose any name, including someone else's.
- The "edit" and "delete" buttons only appear on your own messages, but the policies above let any visitor change any row. That is fine for a private room among friends. For a public deployment, add Supabase Auth and tighten the policies to `auth.uid()`.
- Reactions are counted per browser (a second click removes yours). Counts are stored in the message's `reactions` column, so rapid simultaneous clicks can occasionally race.

## Tech stack

- Vanilla HTML, CSS and JavaScript (ES modules)
- [`@supabase/supabase-js`](https://supabase.com/docs/reference/javascript) v2, loaded from jsDelivr
- Google Fonts: Rubik and Space Mono

## License

MIT. See [LICENSE](LICENSE).
