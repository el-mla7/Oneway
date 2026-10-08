# Assignment
Some times you find urself working on things you dont really specialize at doing...
In this repo iam storing assignments. things i didnt specialize at doing, yet did it one way or another.

Oneway is a website that turns ur password into a hash via a veracity of hashing functions.

A single HTML file that runs seven cryptographic hash functions in your browser. Type anything, pick a function, watch the digest change byte by byte. Flip one input bit and see how much of the output moves.

No build step. No dependencies. No network calls. Nothing you type leaves the tab.

Built as a course assignment for a cybersecurity module.

Live: `https://el-mla7.github.io/oneway` 

---

## What's in it

Four things, all on one page:

**The bench.** A textarea, a list of algorithms, and a digest viewer. Every digest is rendered twice — as raw hex, and as a grid of bytes where each cell's darkness tracks its value. Change the input and the whole grid repaints.

**The avalanche view.** A button under the digest that flips a single input bit and re-runs the hash. The second grid highlights every byte that changed. A good hash flips roughly half the output bits; the page prints the exact count so you can check.

**The password vault.** Two panels side by side. On the left, alice and bob both pick the same password and it gets stored as an unsalted SHA-256 digest — identical rows, one crack unlocks both accounts. On the right, the same password goes through PBKDF2 with a fresh random salt per user — completely different records. Real timings are measured on your device and printed under each panel.

**The reference table.** Bits, bytes, and hex characters for ten common functions, plus status. This is where the "16, 32, 64" question gets answered: divide bits by 8 for bytes, by 4 for hex characters.

---

## The functions

| Function | Bits | Bytes | Hex chars | Status |
|---|---:|---:|---:|---|
| MD5 | 128 | 16 | 32 | Broken — collisions in seconds |
| SHA-1 | 160 | 20 | 40 | Deprecated — collisions shown 2017 |
| SHA-256 | 256 | 32 | 64 | Standard |
| SHA-384 | 384 | 48 | 96 | Fine |
| SHA-512 | 512 | 64 | 128 | Fine |
| SHA3-256 | 256 | 32 | 64 | Standard |
| SHA3-512 | 512 | 64 | 128 | Fine |

Each one has an info button under its row in the picker — click it for construction details, what it's good for, and what to avoid.

---

## How it's built

**MD5 and SHA-3 are hand-written JavaScript.** MD5 follows RFC 1321. SHA-3 is a Keccak-f[1600] sponge over BigInt, following FIPS 202. Both run anywhere, including plain `http://` pages.

**SHA-1 and the SHA-2 family use the Web Crypto API** (`crypto.subtle.digest`). These require a secure context — `https://` or `localhost`. If you open the file over `file://` or an insecure origin, those five functions disable themselves and the page explains why.

**Every function is self-tested before the page trusts it.** On load, each algorithm hashes `"abc"` and compares against its published NIST/RFC test vector. Any function that fails is greyed out in the picker with a reason. This is not decoration — if the browser ships a broken Web Crypto implementation, you see it instead of silently getting wrong digests.

**PBKDF2 for the vault** uses `crypto.subtle.deriveBits` with SHA-256, a 16-byte random salt from `crypto.getRandomValues`, and your choice of 100k / 310k / 600k iterations.

## Author

**Mohamed Mousa**

- GitHub: [el-mla7](https://github.com/el-mla7)
- LinkedIn: [mohammed-mousaa](www.linkedin.com/in/mohammed-mousa-97b03931b)
- Email: mohammed.mousa.dev@gmail.com

---

Made With DeepSeek.
