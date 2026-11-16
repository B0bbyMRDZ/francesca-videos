# Project Playbook: AI-Avatar Shorts → Digital Products

**Purpose of this file:** Give this to Claude at the start of a new chat. It describes a working business model, the exact toolchain, and the workflows I used for my first niche (Declutter with Francesca), so a new niche can be researched, built and launched the same way without re-deciding everything.

**How I want to work:** Do the work end to end and hand me finished files. Show me every video before anything is posted. Ask before anything public or hard to undo (posting, deleting, spending money). Keep explanations short; I often read on my phone.

---

## 1. The business model

1. **A niche audience with a recurring pain point**, where a short tip video can deliver real value in 30–45 seconds.
2. **An AI avatar host** (a named, consistent character) who delivers one tip per video in vertical 9:16 Shorts.
3. **The same video goes out on TikTok, Instagram Reels and YouTube Shorts** through Buffer.
4. **Every video ends with one call to action:** "The free checklist is linked in my profile."
5. **The free lead magnet** (a short PDF checklist) collects emails in Kit.
6. **A five-email welcome sequence** sells the core product (about $29).
7. **An upsell or companion product** (about $24) and a bundle (about $44).
8. **Videos are numbered to match the product.** Each video is "Day N of my 30-day plan," so every video advertises the paid product's structure.

### What made the first niche work (criteria to reuse)

- **The audience buys digital products and trusts a calm, older or expert host.** For the first niche that was people 60+ who are downsizing, decluttering or doing "Swedish death cleaning."
- **The topic gives a long list of concrete, filmable tasks** (one per room or one per day), so there are endless video ideas and natural B-roll.
- **The product is a structured plan** (a 30-day workbook) and not a vague guide. Each video is literally one day of it.
- **Stock footage exists for the topic.** Pexels has plenty of footage of homes, hands, boxes, closets and kitchens. Check this early for a new niche.
- **Search demand was checked with DataforSEO** (YouTube SERP and Google search volume). Similar channels were checked for proof that Shorts in the niche get views.

---

## 2. Tools and accounts

| Purpose | Tool | Notes |
|---|---|---|
| Niche and keyword research | **DataforSEO MCP** (connected) | Use YouTube SERP and keyword-volume endpoints. The NexLev MCP is connected too, but its free tier runs out after about 50 calls a week. Kloudboard is connected but has no credits. |
| Avatar video | **HeyGen** (about $30/mo) | I create the talking-avatar video myself from the script Claude writes, then upload the MP4 to the chat. |
| Avatar image | fal.ai or similar | Photorealistic portrait from a prompt Claude writes. |
| Voice | HeyGen voice (ai33.pro credits are also available) | |
| B-roll | **Pexels API** | My API key goes in a `.env` file as `PEXELS_API_KEY=...`. I'll paste it into the new chat. |
| Editing | Claude, in its cloud workspace | ffmpeg + libass, using the scripts in the GitHub repo (section 6). |
| Video hosting for Buffer | **GitHub public repo** | Buffer needs a public URL for each video, so files are served from `raw.githubusercontent.com` URLs. |
| Scheduling and posting | **Buffer MCP** (connected) | Free plan. See the limits in section 7. |
| Email, landing page, product sales | **Kit** (kit.com) | Landing page, double opt-in, sequence, digital products and sales pages. |
| Domain | spaceship.com | Used for the sender email and domain authentication in Kit. |
| Product PDFs | Claude builds them | HTML to PDF with Playwright (Chromium), letter size, printable. |
| Copy documents | Claude Docs artifacts | Living docs for the Kit copy and the content plan. |

### Claude settings needed

- **Pexels domains must be allowed**, or Claude's workspace can't reach them. In **claude.ai Settings → Capabilities → Allowed websites**, add `api.pexels.com` and `videos.pexels.com`. This is a different setting from the browser's site permissions.
- **The GitHub repo must be added to the session.** The Claude GitHub App must also be installed on the repo, or pushes are refused.

---

## 3. Phase 1: Niche research (what Claude did)

1. **Brainstorm** 8–12 niches where a host persona plus a $29 digital product fits (a planner, workbook, checklist bundle, template set or guide).
2. **Check demand for the top three**:
   - DataforSEO keyword volume for product-intent terms (for example "declutter checklist", "downsizing checklist") and topic terms.
   - The YouTube SERP for the main terms, to see whether Shorts rank and how many views small channels get.
   - Similar channels (for example @MarjorieBellDecor was the format reference: an older female avatar, a tip-list format, B-roll and bold captions).
3. **Pick one niche** and define:
   - The audience.
   - The host persona: a name, a look, and the handle `@<topic>.with.<name>`.
   - The core product, the lead magnet and the upsell.
4. **Write the hooks** (about 30) and map each to a day of the plan.

---

## 4. Phase 2: Products

### Products built for Declutter with Francesca (as a template)

| Product | Price | Format | Notes |
|---|---|---|---|
| Free 30-Day Declutter Checklist | Free (lead magnet) | 3-page PDF | One line per day. Links to the sales page. |
| The 30-Day Declutter Plan for 60+ | $29 | 69-page printable workbook PDF | Cover, how-to-use, 30 daily pages (task, why it matters, checklist, keep/donate/toss tracker, notes), room checklists, family conversation scripts, trackers. |
| The Legacy Organizer | $24 | 34-page PDF | Upsell: important documents, accounts, contacts, wishes and "where things are" records. The cover has white write-in boxes for name and "last updated". |
| Bundle | $44 (suggested) | Both PDFs | |

### How Claude builds the PDFs

- **Content is written in Python data files** (days, checklists), and an HTML template is rendered to PDF with Playwright.
  - Letter size with print margins.
  - Brand palette: sage green #5B7F6A, deep green, warm off-white. Fonts: Inter plus a serif for headings.
- **Every page is checked for overflow** before export, and PDF metadata (title, author) is set with pypdf.
- **Product mockup images** are 1600×1600 PNGs made with PIL. They show the cover and two inside pages, fanned with shadows, with a headline such as "PRINTABLE WORKBOOK · 69 PAGES". They're used on the Kit product page and in posts.

---

## 5. Phase 3: Kit setup (in this order)

All copy is written by Claude in a Claude Docs artifact first. Then I paste it into Kit.

1. **Settings:** set the sender name (for example "Francesca, Declutter with Francesca"), the sender email on my own domain (verify it), and a mailing address for the footer (a PO box or virtual mailbox is fine; US law requires one).
   - Authenticate the domain in Kit by adding DNS records at the registrar (spaceship.com).
2. **Product:** create the $29 workbook as a digital product, upload the PDF, and add the product image, the sales copy and the receipt message. Copy the product link.
   - **In Kit, the product page *is* the sales page.** There is no separate sales page to build.
   - **The product page defaults to a two-column layout.** To get full-width text below it, change the layout in the page editor or add full-width content blocks.
   - **Publish:** if "View page" returns a 404, the product isn't published yet. Use the product's publish/status toggle.
3. **Landing page:** create it with the free checklist PDF as the incentive and **double opt-in** on.
4. **Emails:** add the confirmation and delivery emails to the landing page's incentive settings, and set the thank-you page.
5. **Sequence:** create "Welcome: 30-Day Plan" with five emails:
   - 1: delivery and a welcome
   - 2: quick win
   - 3: story and objection handling
   - 4: offer
   - 5: last reminder and the upsell mention
6. **Automation:** when someone subscribes via the landing page, add tag `checklist` and add them to the Welcome sequence. When someone buys, add tag `buyer` and remove them from the Welcome sequence (if the plan allows).
7. **Upsell product:** create it the same way, with its own sales copy and receipt.
8. **Bio links:** put the landing page link in every social profile.
9. **Test:** sign up with my own email, click every link, and buy with a 100% discount code.

**Live links for Francesca (for reference):**
- Free checklist landing page: https://declutter-with-francesca-llc.kit.com/free-checklist
- Workbook: https://declutter-with-francesca-llc.kit.com/products/the-30-day-declutter-plan

**Placeholders in the copy docs:**
- `[SALES PAGE LINK]`: the product URL.
- `[CHECKLIST PAGE LINK]`: the landing page URL.
- `[LAUNCH PRICE]` / `[LAUNCH END DATE]`: an optional discount.
- `{{ subscriber.first_name | default: "friend" }}`: Kit personalization. Keep it exactly as written.

---

## 6. Phase 4: Channel setup

1. **Create TikTok, Instagram (business or creator account, required for Buffer auto-publishing) and a YouTube channel** under the same handle.
2. **Ask Claude for the profile kit:**
   - The YouTube channel description and channel tags.
   - Bios for each platform (with the checklist link).
   - An image prompt for a YouTube banner featuring the host.
3. **Connect all three accounts to Buffer** (buffer.com → Channels → Connect).
4. **Connect the Buffer MCP in Claude.** Claude finds the organization and channel IDs itself with `get_account` and `list_channels`.

---

## 7. Phase 5: Video production workflow (repeat for every video)

### Video format (45 seconds or less)

| Time | Segment | Visual | On-screen title |
|---|---|---|---|
| 0:00–0:03 | Hook (the title, spoken) | Avatar | Hook title in a green box, top of frame. Keep it to 2 short lines so it doesn't cover the face. |
| 0:03–0:07 | Why it matters | B-roll | none |
| 0:07–0:15 | Point 1 | B-roll | "1  POINT NAME" |
| 0:15–0:22 | Point 2 | B-roll | "2  POINT NAME" |
| 0:22–0:30 | Point 3 | B-roll | "3  POINT NAME" |
| 0:30–0:35 | Do it today (small action) | B-roll | "10 MINUTES · START NOW" or similar |
| 0:35–end | Call to action: "This is Day N of my 30-day declutter plan. The free checklist is linked in my profile." | Avatar | "FREE CHECKLIST / LINK IN PROFILE" |

Captions run the whole video: 1–3 words at a time, white with a black outline, the current word in yellow, placed in the lower third.

### Per-video package (Claude writes, before I make the video)

Claude writes one Word doc per video with:
1. **The HeyGen script**, in a copy-paste box. Write numbers as words ("thirty-day") so the voice reads them right.
2. **An edit timeline table.**
3. **A clip CSV** with 12 timed B-roll slots: `video,clip,segment,start,end,duration_sec,script_line,search_query,fallback_queries,notes`. Fallback queries are pipe-separated.
4. **The posting copy:**
   - TikTok caption.
   - Instagram caption: the first line is the spoken hook in sentence case, not Title Case.
   - YouTube title, ending with "#declutter".
   - YouTube description with the real checklist link (never leave a placeholder).
   - A pinned-comment question.

### The loop

1. **I generate the avatar video in HeyGen** from the script and upload the MP4 here.
2. **Claude fetches B-roll from Pexels:** `pexels_fetch.py videoNN_clips.csv --out pexels --candidates 3`. That gives portrait clips, three candidates per slot, 36 clips per video.
3. **Claude times the speech.** Speech-to-text model downloads are blocked in the workspace, so it uses ffmpeg `silencedetect=noise=-30dB:d=0.2` to find phrase boundaries and maps them to the script lines.
4. **Claude picks clips** from contact sheets (`contact_sheet.py`). Weak matches get a second round of targeted searches.
5. **Claude writes the edit config** (`videoNN_edit.json`):
   - `cta_at`: when the closing avatar returns.
   - `broll`: start time, file and in-point for each clip.
   - `speech`: phrase start, end and text.
   - `titles`: start, end, text and style.
6. **Claude renders:** `python3 build_short.py videoNN_edit.json`.
   - Output: 1080×1920, 30 fps, H.264 CRF 18, AAC.
   - Audio normalized to -14 LUFS.
   - Inter ExtraBold captions; sage-green (#5B7F6A) title boxes.
7. **Claude checks frames** across the whole video (one every ~2.5 s): titles in sync, nothing covering the face, B-roll matching the words.
8. **Claude sends me the video for review.** Nothing is posted until I approve.
9. **After approval, Claude pushes the MP4 to GitHub** (`videos/videoNN-topic.mp4`) and confirms the raw URL returns 200.
10. **Claude schedules the posts in Buffer** (section 8).
11. **I pin the comment by hand** after each post goes live.

### Lessons learned

- **HeyGen file names are meaningless.** Claude matches each upload to its script by its pauses and length.
- **Long hook titles** wrap to three or four lines and cover the face. Keep them to about 25 characters per line, 2 lines.
- **Pexels is thin for very specific objects** (instruction manuals, dead batteries). Use broader actions (hands sorting, a person at a laptop) or rewrite the line to be more filmable.
- **HeyGen can do some editing itself,** but captions, titles and B-roll timing are better and more consistent done by Claude.

---

## 8. Phase 6: Posting through Buffer

### Settings for every post

| Platform | Settings |
|---|---|
| TikTok | Video asset (raw GitHub URL), TikTok caption, `isAiGenerated: true` |
| Instagram | `type: "reel"`, `shouldShareToFeed: true`, `isAiGenerated: true`, Instagram caption |
| YouTube | `title`, `categoryId: "26"` (Howto & Style), `madeForKids: false`, `isAiGenerated: true`, description as the post text |

- **Mode:** `customScheduled` with a `dueAt` in the account timezone (America/Chicago, so -06:00 in winter and -05:00 in summer).
- **Raw URL pattern:** `https://raw.githubusercontent.com/<owner>/<repo>/main/videos/<file>.mp4`

### Schedule rules (my preferences)

- **Post to all three platforms** unless I say otherwise.
- **One video per day, in the morning (about 8–10 a.m. Central).**
- **Vary the time by 15–60 minutes from day to day** so it looks human, and put the platforms a few minutes apart (for example TikTok 9:12, Instagram 9:19, YouTube 9:27).
- **Order videos by workbook day** where possible, so the series feels like it moves forward.

### Buffer free-plan limits

- **Only 10 scheduled posts at a time,** which is 3 videos × 3 platforms. Schedule 3 days ahead and top up as posts go out. Claude can set a reminder to do this.
- **No first comment** (paid feature), so pinned comments are manual.
- **Buffer can't set YouTube tags.** Use hashtags in the title and description instead.
- **To cancel a scheduled post,** use `delete_post`. Always check whether I already posted something by hand first.

---

## 9. GitHub repo and reusable scripts

The repo for the first niche is `B0bbyMRDZ/francesca-videos` (public). It holds:
- `videos/`: finished MP4s.
- `tools/pexels_fetch.py`: Pexels downloader. Reads `PEXELS_API_KEY` from the environment or `.env`; flags are `--out`, `--candidates N` and `--no-zip`.
- `tools/build_short.py`: the editor (avatar hook → timed B-roll → avatar call to action, captions, titles, loudness).
- `tools/contact_sheet.py`: frame grids for choosing clips.
- `tools/examples/`: a real clip CSV, edit config and caption JSON from Video 3.

**For a new niche:**
1. Create a new public repo, for example `<handle>-videos`.
2. Add it to the Claude session and install the Claude GitHub App on it.
3. Have Claude copy `tools/` from this repo.

To match a new brand, change only the colours and font in the ASS styles inside `build_short.py`, and the CTA title.

---

## 10. Status of the first niche (as of Nov 16, 2026)

**Brand:** Declutter with Francesca. The host is Francesca, a woman in her 60s with a silver bob and warm, calm delivery. The handle on all platforms is @declutter.with.francesca.

**Videos posted or scheduled so far:**

| # | Topic | Plan day | Status |
|---|---|---|---|
| 1 | Kitchen (duplicate gadgets) | 6 | Posted by me |
| 2 | Bathroom | — | Posted |
| 6 | Junk drawer | 1 | Scheduled Tue Nov 17 |
| 3 | Sheets / linen closet | 4 | Scheduled Wed Nov 18 |
| 4 | Garage dangers | 18 | Scheduled Thu Nov 19 |
| 5 | Empty boxes | 20 | To schedule for Fri Nov 20 |

**Open ideas not yet done:**
- A Legacy Organizer bundle and an after-purchase offer in Kit.
- A Day 20 email.
- A clickable sales link inside the free checklist PDF.

---

## 11. What to do in the new chat

1. **Research 3 candidate niches** with DataforSEO (search demand, YouTube competition, buyer intent). Recommend one, using the criteria in section 1.
2. **Define the persona and handle,** the core product ($29), the lead magnet and the upsell.
3. **Write 30 hooks** mapped to the days of the plan, plus the avatar image prompt.
4. **Build the product PDFs** and mockup images.
5. **Write all Kit copy** in a Claude Docs artifact.
6. **Write the first batch of per-video packages** (Word doc + clip CSV each).
7. **Then run the video loop** in section 7 and the posting rules in section 8.
