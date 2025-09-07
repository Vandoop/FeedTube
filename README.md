<h1 align="center"><b>FeedTube</b></h1>
<p align="center"><a href=""><img src="https://raw.githubusercontent.com/testertv/FeedTube/refs/heads/main/images/logo.png?raw=true"></a></p>

<p align="center">        
<a href="https://www.gnu.org/licenses/gpl-3.0" alt="License: GPLv3"><img src="https://img.shields.io/badge/License-GPLv3-brightgreen.svg"></a>  
<a href="" alt=""><img src="https://img.shields.io/badge/Platform-Browser-brightgreen.svg"></a>
<a href="" alt=""><img src="https://img.shields.io/badge/SW--Kind-HTML Page-brightgreen.svg"></a>
<a href="" alt=""><img src="https://img.shields.io/badge/Language-HTML+JS-brightgreen"></a> 
<a href="" alt=""><img src="https://img.shields.io/badge/Version-0.1(Beta)-blue"></a>
</p><p align="center">

## 📺 What is FeedTube?

FeedTube is a lightweight userscript that turns YouTube channel RSS into a fast, full‑page feed. It aggregates your subscriptions, caches offline, auto‑switches fetch sources, filters Shorts, and lets you save to local playlists — with one‑click channel adding and NewPipe‑compatible import/export.

YouTube has a very busy interface that takes a long time to load and freezes. To watch videos on FeedTube, embed links are used by default because they allow you to load and watch videos faster.

It is not very easy to recreate YouTube's full functionality in script, so some features may not work correctly or, as in the case of video search, may be missing altogether and redirect you to the original site.

## ✨ Highlights
- No registration or login data needed
- Full‑page grid from channel RSS with per‑channel cache
- Resilient fetching (Direct → Mirror → Proxies) with source switch
- Subscriptions manager + “Add to FeedTube” button on YouTube
- Shorts toggle/sort
- Local playlists + NewPipe Subscriptions import/export supported
- Quick playback: new tab, popup, or floating panel

## 🖼️ Screenshots
<p align="center"><a href=""><img src="https://raw.githubusercontent.com/testertv/FeedTube/refs/heads/main/images/screenshot1.png?raw=true"></a></p>

<p align="center"><a href=""><img src="https://raw.githubusercontent.com/testertv/FeedTube/refs/heads/main/images/screenshot2.png?raw=true"></a></p>

## ⚙️ Installation
1. Install the extension [Tampermonkey](https://www.tampermonkey.net)
2. Install the [Script](https://github.com/testertv/FeedTube/releases/download/v0.1_(Beta_Greasyfork_namespace)/FeedTube-0.1_Greasyfork_namespace.user.js) or Greasyfork [Script](https://update.greasyfork.org/scripts/548703/FeedTube.user.js)
3. Create empty FeedTube.html file or [download](https://raw.githubusercontent.com/testertv/FeedTube/refs/heads/main/files/FeedTube.html) it (Right mouse click -> Save Link As)
4. Drag&Drop FeedTube.html in your browser


## 🔗 Fetch Sources
Below is a summary for each Source mode in your script and its limitations. All modes fetch the same YouTube RSS (feeds/videos.xml); they differ only in “how/through whom” the request is made.

> All modes use the same YouTube RSS; only the transport differs.

<details>
<summary><b>Auto (direct → mirror → proxies)</b></summary>

- How it works: Tries in order: Direct (2 attempts) → r.jina.ai → cors.isomorphic-git.org → allorigins.
- Pros: Most resilient; something usually works.
- Limitations: If Direct is unavailable, you may wait a long time (up to ~20s × 2 per channel due to GM_xhr timeout). Total load time can be stretched by the slowest channel.
</details>

<details>
<summary><b>Direct (GM_xhr → youtube.com)</b></summary>

- How it works: GM_xmlhttpRequest directly to youtube.com (CORS is not an issue). Timeout 20s, anonymous: true (no cookies).
- Pros: Fast, no middlemen; better privacy (requests go only to YouTube); less chance of stale responses.
- Limitations:
  - On file:// you must enable your userscript manager’s “Allow access to file URLs” (otherwise it won’t run). Alternative: serve FeedTube.html via http://localhost.
  - Can be blocked by AdBlock/DNS/Firewall rules (youtube.com, i.ytimg.com).
  - With many subscriptions you may hit 429 or rate limits from YouTube.
  - In some setups (e.g., Greasemonkey/Firefox) you may need explicit @connect youtube.com (you already have @connect *).
</details>

<details>
<summary><b>Mirror (r.jina.ai)</b></summary>

- How it works: Proxied request: https://r.jina.ai/http/<target URL>.
- Pros: Bypasses CORS easily; often works where Direct is blocked.
- Limitations:
  - Public third‑party service: possible limits, 403/429/5xx, regional/network hiccups.
  - Can serve stale data (caches along the path); you append &_tm=… to bust cache, but it’s not guaranteed.
  - Privacy: channel feed URLs go to a third party.
</details>

<details>
<summary><b>Proxy 1 (isomorphic‑git)</b></summary>

- How it works: https://cors.isomorphic-git.org/https://www.youtube.com/feeds/videos.xml?...&_tm=...
- Pros: Another CORS proxy fallback.
- Limitations:
  - Frequently hits rate limits/Cloudflare → 403/502.
  - Unpredictable stability; public service.
  - Potential limits on request size/count.
</details>

<details>
<summary><b>Proxy 2 (AllOrigins, raw)</b></summary>

- How it works: https://api.allorigins.win/raw?url=<encoded URL>&_tm=...
- Pros: Simple raw CORS proxy; convenient fallback.
- Limitations:
  - Aggressive caching on the service side (you add _tm, but cache may still appear).
  - Stability/quotas/5xx typical of public proxies.
  - Privacy: again, third‑party service.
</details>

### General constraints
- file:// access required for Direct (or use localhost)
- Ad‑blockers/CORS can block required domains
- Proxy fetches may need explicit timeouts
- Concurrency can hit rate limits
- YouTube RSS typically returns ~15 items

### Recommendations
- Use Auto; switch to Direct if slow
- Use Mirror if Direct is blocked
- Allowlist domains and reduce concurrency for large lists

## 🛡️ Privacy Policy
The FeedTube project aims to ensure privacy, anonymity, and speed when using YouTube. Therefore, the application does not collect any data without your consent. Despite this, the script has the ability to download video information through third-party servers that may collect your data.

## 🐂 License
FeedTube is Free Software Script: You can use, study, share, and improve it at will. Specifically you can redistribute and/or modify it under the terms of the GNU General Public License as published by the Free Software Foundation, either version 3 of the License, or (at your option) any later version.

## 💳 Please support my projects! 🤗 Thx.!!!
<p align="center">
<a href="" alt=""><img src="https://img.shields.io/badge/Ethereum-Wallet%20➡️-blue"></a>  0x23A82beB500b8781c55E6F17b7e327d85F7f4108 <a href="" alt=""><img src="https://img.shields.io/badge/-⬅️%20Wallet-blue"></a>
</p><p align="center">
