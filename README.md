# CoolROM provider for ROM Hub / ROMarr

**Status: not installable, and — unlike the others in this family —
not surveyed. This repository is documentation and a catalogue entry.**

| Capability | Status |
|---|---|
| `search` | **Unimplemented — the site's structure was never inspected** |
| `importer` | Unimplemented, same reason |
| `stream` | Unimplemented, same reason |

## Why there is nothing here

`coolrom.com.au` 301-redirects to `coolrom.com`, whose `robots.txt` is
readable and contains this:

```
User-agent: GPTBot
Disallow: /

User-agent: CCBot
Disallow: /

User-agent: anthropic-ai
Disallow: /

User-agent: Claude-Web
Disallow: /
```

The site operator has explicitly asked Anthropic's agents not to crawl the
site. The survey that produced the other six providers in this family was
performed by one, so **it stopped at `robots.txt` and fetched no further
pages.**

That is the whole reason this repository is empty of code. It is not that
CoolROM is hard, or challenged, or dead — it is that nobody has looked, and
filling the gap by ignoring the request was not on the table.

## What is and is not known

**Known**, from `robots.txt` alone:

* The site is behind Cloudflare, and `robots.txt` itself serves cleanly
  (HTTP 200, `text/plain`) — so there is no blanket managed challenge of the
  kind that blocks CDRomance.
* For a generic client the applicable group is `User-agent: *`, which allows
  the site with **`Crawl-delay: 10`** and disallows `/cr-admin/`, `/members/`,
  `/admin/`, `/api/`, `/ads/` and `/queue.php`.
* The file also blocks a long list of SEO and bulk crawlers (SemrushBot,
  AhrefsBot, MJ12bot, DotBot, BLEXBot, Bytespider, Baiduspider, YandexBot),
  which reads as an operator who is actively managing crawl load rather than
  one who has never thought about it.

**Not known** — and not guessed at anywhere in this repository: whether there
is a paginated per-platform listing, what the detail-page id scheme is,
whether titles carry regions or sizes, what the download flow looks like, and
whether the site still hosts files at all.

## The distinction that matters before anyone continues this

These are two different questions and they should not be run together:

1. **Should an Anthropic agent crawl CoolROM?** No. `robots.txt` answers it
   directly, and that is why this repository is empty.

2. **May the operator's own ROM Hub plugin fetch it?** That is a separate
   question, and it is the operator's to answer rather than this survey's.
   ROM Hub's client identifies as `rom-hub/0.1` (set host-side in
   `rom_hub/broker/fetcher.py`; a plugin cannot change it, which also means it
   cannot forge one). That is not `anthropic-ai` and not `Claude-Web`, so the
   group that applies to it is `User-agent: *` — allowed, at a 10-second crawl
   delay.

So a provider here is buildable in principle, by someone who is not an
Anthropic agent, against a structure that must be surveyed firsthand first.

## If you pick this up

1. Survey it yourself — listing shape, id scheme, whether files are served.
2. Honour `Crawl-delay: 10`. That is a declared rule, not a courtesy, and it
   is ten times the delay the Retrostic provider uses voluntarily.
3. Stay out of `/api/`, `/members/`, `/admin/`, `/cr-admin/`, `/ads/` and
   `/queue.php`.
4. Model the provider on `romarr-plugin-retrostic`, which is the reference for
   this family, and take its platform-mapping discipline with it: every slug
   verified against `romarr.platforms.resolve()` by a test, and any system
   ROMarr does not carry counted and skipped rather than guessed.

## Terms

Nothing here fetches, indexes or redistributes anything. This repository
records why a survey was not performed.

## License

MIT — see `LICENSE`.
