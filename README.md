<h1 align="center"><b>FeedTube</b></h1>
<p align="center"><a href=""><img src="https://raw.githubusercontent.com/testertv/FeedTube/refs/heads/main/images/logo.png?raw=true"></a></p>

<p align="center">        
<a href="https://www.gnu.org/licenses/gpl-3.0" alt="License: GPLv3"><img src="https://img.shields.io/badge/License-GPLv3-brightgreen.svg"></a>  
<a href="" alt=""><img src="https://img.shields.io/badge/Platform-Browser-brightgreen.svg"></a>
<a href="" alt=""><img src="https://img.shields.io/badge/SW--Kind-HTML Page-brightgreen.svg"></a>
<a href="" alt=""><img src="https://img.shields.io/badge/Language-HTML+JS-brightgreen"></a> 
<a href="" alt=""><img src="https://img.shields.io/badge/Version-2025.03.06-blue"></a>
</p><p align="center">

## What is FeedTube?

✨ FeedTube is a lightweight userscript that turns YouTube channel RSS into a fast, full‑page feed. It aggregates your subscriptions, caches offline, auto‑switches fetch sources, filters Shorts, and lets you save to local playlists — with one‑click channel adding and NewPipe‑compatible import/export.

## Highlights
- Full‑page grid from channel RSS with per‑channel cache
- Resilient fetching (Direct → Mirror → Proxies) with source switch
- Subscriptions manager + “Add to FeedTube” button on YouTube
- Shorts toggle/sort
- Local playlists + NewPipe import/export
- Quick playback: new tab, popup, or floating panel

## Installation
1. Install the extension [Tampermonkey](https://www.tampermonkey.net)
2. Install the Script
3. Create empty FeedTube.html file or download it
4. Drag&Drop FeedTube.html in your browser


## Fetch Sources

> All modes use the same YouTube RSS; only the transport differs.

<details>
<summary><b>Auto (direct → mirror → proxies)</b></summary>

- Tries: Direct (2x) → r.jina.ai → isomorphic‑git → allorigins  
- Pros: Most resilient  
- Limitations: Can wait ~20s × 2 per channel if Direct stalls; total time dominated by slowest
</details>

<details>
<summary><b>Direct (GM_xhr → youtube.com)</b></summary>

- 20s timeout; anonymous (no cookies)  
- Pros: Fast, private, fresh  
- Limitations: Needs file:// access or localhost; may be blocked by filters; 429 with many channels; may need `@connect youtube.com`
</details>

<details>
<summary><b>Mirror (r.jina.ai)</b></summary>

- Bypasses CORS; good fallback  
- Limitations: Third‑party; possible stale/cache; 403/429/5xx; privacy trade‑off
</details>

<details>
<summary><b>Proxy 1 (isomorphic‑git)</b></summary>

- Simple CORS fallback  
- Limitations: Unpredictable; rate‑limits/Cloudflare; quotas
</details>

<details>
<summary><b>Proxy 2 (AllOrigins, raw)</b></summary>

- Handy raw proxy  
- Limitations: Aggressive caching; quotas; third‑party privacy
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
