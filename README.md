# Passtale

Strong passphrases with memorable stories. Chinese (Shuangpin) or English (EFF-long).

## What it does

Generate random passphrases, then use an LLM to create a mnemonic story (and optionally a comic) to help you remember them.

**Chinese mode**: words from the [现代汉语常用词表](https://github.com/liuxilu/Proofread-Modern-Chinese-Common-Lexicon) (~41K unique shuangpin codes). Copy as Chinese, pinyin, or shuangpin.

**English mode**: words from the [EFF Long Wordlist](https://www.eff.org/dice) (7,776 words).

## Entropy

| Passphrase | Chinese (SP) | English (EFF) |
|---|---|---|
| 4 words | ~61 bits | ~52 bits |
| 5 words | ~77 bits | ~65 bits |
| 6 words | ~92 bits | ~78 bits |

5 shuangpin words ~ 6 EFF words, in fewer keystrokes.

## Usage

### Web app

Open `web/index.html` in a browser, or serve it:

```sh
cd web && python3 -m http.server 8787
```

Features:
- Roll the dice for multiple passphrase candidates
- Chinese: shows characters, pinyin, shuangpin code per word
- Configurable separator and tone display
- Copy as Chinese / Pinyin / Shuangpin / English
- Generate mnemonic stories via OpenRouter (DeepSeek, GPT, Gemini, Claude)
- Generate mnemonic comics via Gemini image models

### Regenerate wordlist

```sh
cd wordlist-gen && cargo run --release
```

Downloads the 现代汉语常用词表 (cached), converts to shuangpin, and outputs:
- `web/wordlist.js` — JS wordlist for the web app
- `wordlist.txt` — full wordlist with metadata
- `shuangpin.wordlist` — xkcdpass-compatible (one word per line)
- `sankey.html` — pipeline visualization

## Project structure

```
passtale/
├── web/                  # Web app (static HTML/JS)
│   ├── index.html
│   ├── wordlist.js       # Generated Chinese wordlist
│   └── eff_long.js       # EFF Long Wordlist
├── wordlist-gen/         # Rust CLI wordlist generator
│   ├── Cargo.toml
│   └── src/main.rs
└── README.md
```

## Shuangpin scheme

Xiaohe Shuangpin (小鹤双拼):

**Initials**: zh→v, ch→i, sh→u, others→themselves

**Finals**: ai→d, ei→w, ao→c, ou→z, an→j, en→f, ang→h, eng→g, ong→s, ia/ua→x, ie→p, iao→n, iu→q, ian→m, in→b, iang/uang→l, ing→k, uai→k, ui→v, uan→r, un→y, ue→t

## Data sources

- [现代汉语常用词表](https://github.com/liuxilu/Proofread-Modern-Chinese-Common-Lexicon) — 56K common Chinese words with pinyin (proofread 2025)
- [EFF Long Wordlist](https://www.eff.org/dice) — 7,776 English words
