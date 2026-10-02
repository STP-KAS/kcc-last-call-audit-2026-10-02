# Second pass

2026-10-02, after the first push. No verdict changed. No finding was deleted.

## What was re-opened

- This repo's `AUDIT.md`, top to bottom, against the live pages below.
- https://x.com/kccforum/status/2105991195583488410 and the reply https://x.com/kccforum/status/2106008195114381508.
- https://x.com/manyfest_/status/2106012029358047445, which quotes the first post.
- https://kccs.dev/ and https://kccs.dev/kcc-0-purpose-and-guidelines/ in full.
- https://kccs.dev/kcc-1-covenant-concepts-and-abi/ header: Status Last Call. The string `Last-Call-Deadline` does not appear.
- https://kccs.dev/kcc-2-authority-schemes/ : Status Last Call, unkeyed `Hash(x)`, citation "KCC-1 Section 3.1", citation "KCC-1 Section 11.2". No `Last-Call-Deadline`.
- https://kccs.dev/kcc-20-fungible-token-covenant/ : Status Draft, `Updated: 2026-08-25`, `P2PKHHash(pubkey)` and `P2PKHHash(ecdsa_pubkey)` still in the scheme block. No Security Considerations heading.
- kaspanet/kccs `main` was still `411b41bc14b3fda8f3a0548242c555f3597cad1a` at the write-pass `gh api` check. The site "View canonical source" links point at `blob/main` for the same four files.

## What held

| ID | Second-pass result |
| --- | --- |
| LC-1 blocker | Held. Rendered KCC-1 and KCC-2 say Last Call. The deadline header is absent on the site and in the raw preambles. The 14-day sentence is in post 2105991195583488410 and not in the files. |
| LC-2 blocker | Held. The rendered §4.3 is the same sentence as `kcc-0000.md` lines 199–204: KCC-1, KCC-2, and KCC-20 retain Draft and must conform before Review. |
| LC-3 blocker | Held. Rendered KCC-20 is Draft and still says `P2PKHHash`. The reply post says Last Call is pending a reference review "in the coming days." The file has no reference link and no vectors directory. |
| LC-4 should-fix | Held. Not re-fetched in this pass beyond the write-pass topic JSON. The posts do not claim the Kas-Smiths threads were updated. |
| LC-5 through LC-11 | Held. They are quotes from the raw files at the pin. The site copies of KCC-2's stale section numbers match the raw file. |
| LC-12 holds | Held. Not recomputed again in this pass. The write-pass run was `FAILS 0` and the site still prints the same P2SH and P2PKH sample strings. |

KCC numbers were checked again. 0 is the process. 1 is the covenant ABI. 2 is authority schemes. 20 is the fungible token. The borrowed-receive guide is auxiliary. The site and the raw KCC-2 both call the Silverscript file non-normative reference code. This pass did not treat it as the specification.

## What changed in the audit text

The LC-3 citation of post 2106008195114381508 now uses the reply's own sentence, including "final milestone in the KCC process" and "expected in the coming days." The verdict stays blocker. KCC-0's Last Call gate is Security Considerations plus the deadline header. The reference implementation is a Final gate. The reply names the reference as the milestone. That is a sharper form of the same conflict, not a new one.

## Still not verified

- Full HTML diff of the KCC-1 page. The first fetch of that page truncated. This pass checked the status header only.
- Header and footer link crawl of kccs.dev.
- Silverscript compiler source.
- Rusty-kaspa sighash implementation.
- CODEOWNERS and the review-comment threads on #27, #30, #31, #32, and #33.
- Whether #31's reject rows equal closed #20.
- `cargo test` on unmerged argent-lang/kcc20-reference#1.
- kaspaexplained `/status`. The master already records a 2026-10-02 morning read. This pass did not fetch it.

None of those gaps are holding up LC-1, LC-2, or LC-3. Those three rest on the headers, §4.3, and `kcc-0020.md`, which were re-read.
