# Coverage

Audit date 2026-10-02. Commit under test: `411b41bc14b3fda8f3a0548242c555f3597cad1a`. Re-checked with `gh api repos/kaspanet/kccs/commits/main` during the write pass. Discussions on that repo: false. Default branch: `main`. Pushed at: `2026-10-01T13:15:20Z`.

"Read pass" is the source reading before this write. "Write pass" is a live re-open while the files in this repo were being written.

## Posts

| URL | When | What it contained |
| --- | --- | --- |
| https://x.com/kccforum/status/2105991195583488410 | Read pass, cited by the task prompt | 2026-10-02 12:00:03 UTC. KCC-1 and KCC-2 entered Last Call, a final 14-day review, finalized if no major issues. |
| https://x.com/kccforum/status/2106008195114381508 | Read pass | 2026-10-02 13:07:36 UTC. KCC-20 Last Call is pending peer review of the reference implementation. |
| https://x.com/manyfest_/status/2106012029358047445 | Read pass | 2026-10-02 13:22:50 UTC. KCC-20 progresses with 1 and 2, needs a published reference implementation, Argent reference being audited toward Last Call. |

The write pass did not re-fetch X. The second pass must re-open these three posts before those sentences stay.

## Site

| URL | When | What it contained |
| --- | --- | --- |
| https://kccs.dev/ | Write pass | Four documents. KCC 0 Meta Final. KCC 1 Standards Track, Covenant, Last Call. KCC 2 Standards Track, ABI, Last Call. KCC 20 Application, Covenant, Draft. Links the KIP boundary at https://kips.dev. |
| https://kccs.dev/kcc-0-purpose-and-guidelines/ | Read pass | Rendered §4.3 matched the raw "retain their Draft status" paragraph. |
| https://kccs.dev/kcc-1-covenant-concepts-and-abi/ | Read pass | Fetch truncated at 30720 of 54967 bytes. Normative claims use the raw file. Full HTML diff not finished. |
| https://kccs.dev/kcc-2-authority-schemes/ | Read pass | Rendered text matched the raw unkeyed hash sentence and the stale section cites. No Last-Call-Deadline on the page. |
| https://kccs.dev/kcc-20-fungible-token-covenant/ | Read pass | Not diffed line-by-line against raw in the write pass. Status on the index is Draft. |
| https://kips.dev/ | Read pass | Index lists KIP-17 and KIP-20 as Active. |
| https://github.com/kaspanet/kccs | Write pass via `gh api` | `main` still `411b41bc`. |
| https://github.com/IzioDev/kips.dev/issues | Not opened as an issue list in the write pass | Header/footer crawl of kccs.dev HTML was not finished. Recorded as a gap. |

## Repo files at 411b41bc

Read in full unless noted.

| File | Note |
| --- | --- |
| README.md | 16 lines. Status table. |
| LICENSE.md | CC0 waiver target. |
| kcc-template.md | Header order and the Last Call security requirement. |
| kcc-0000.md | Process. §4.2, §4.3, §5, §7, §8, §13 read in full across the pass. |
| kcc-0001.md | Preamble, hash, integers, P2SH, leader §3.8.1, virtual §3.9, vectors §6, security §7, copyright §9. |
| kcc-0001/vectors/conformance.json | Hash rows, P2SH object, `state_encoding` object lines 639–667, template rows. Not every nested dispatch example was re-printed in the write pass. |
| kcc-0002.md | Full. |
| kcc-0002/vectors/authority-schemes.json | Constructions recomputed. Approval checks counted, not executed. |
| kcc-0002/reference-code.md | Opened. Labeled non-normative. Not treated as the spec. |
| kcc-0020.md | Full, 296 lines. No vectors directory. |
| kcc-0020/borrowed-receive-authorization.md | Opened. The main file calls it an explanation. |

## GitHub depth

| Object | Note |
| --- | --- |
| #32 `815ecaff3071f5e227cc4b4cdb6c167ae2915666` | Merged 2026-10-01T12:33:08Z by michaelsutton. Status flip for KCC-1 plus README. |
| #33 `ad1b8996d648708c0ac6e351f950437c1b867c29` | Merged 2026-10-01T12:52:21Z by michaelsutton. Status flip for KCC-2 plus README. |
| #34 `411b41bc14b3fda8f3a0548242c555f3597cad1a` | Merged 2026-10-01T13:15:20Z. README KCC-0 row to Final. The file was already Final. |
| #25 `c0bb8f3babbb6a93dbddac900121e5046c1ec388` | 2026-09-21. KCC-0 Final in the file. Also the parent that still defined keyed `P2PKHHash`. |
| #30 `90beacd0dd34543a7321144d122189d779c5ad9b` | 2026-09-27. Unkeyed P2PKH hash. |
| #27 `da834af024b235171cd154fdfde16c0cadf8854f` | 2026-09-28. KCC-1 compliance. Diff not re-read comment by comment. |
| #18 `3229efbbcbc57e5b75df750d1cf045298d1df8a0` | 2026-08-28. Last commit on `kcc-0020.md`. Hash-chain front-run patch. |
| #2 adding commit `e31a5a855bdebd3bdc4456e5bd40179e9f98a3e8` | 2026-08-21T02:13:31+03:00. Birth of `kcc-0020.md`. |
| #31 head `cfb74cfa4d7e25f3e7ec0f9144ad72c460b9d810` | Open, not merged. Raw `kcc-0020.md` read far enough to see Security Considerations and the sighash sentence. PR body from `gh` was null. Not claimed. |
| #24, #26, #29 | Open. File lists from `gh api .../files`. They do not edit KCC-1, KCC-2, or KCC-20. |
| #20 | Closed unmerged. Not diffed against #31's reject rows in the write pass. |
| #14, #28 | Open issues. Read as described in AUDIT. No comment posted. |
| #11 | Closed. Not re-opened in the write pass. |
| Branches | `main` at the pin. Stale `kcc0-finalization` was seen in the read pass at `63d6924df279e2379924fb5df4249b0c8b7b2c91`. Not re-listed in the write pass. |
| Discussions | `has_discussions` false. |

Review-comment threads on #27, #30, #31, #32, and #33 were not read comment by comment. CODEOWNERS was not fetched. File lists for closed #18 and #23 were not retrieved. Those are gaps.

## Related

| URL | When | What it contained |
| --- | --- | --- |
| https://raw.githubusercontent.com/kaspanet/kips/e4ae2332117b5cb68bd6188e065ef885b6d17939/kip-0017.md | Write pass | Status Active. Title Covenants and Improved Scripting Capabilities. Updated 2026-05-31. |
| https://raw.githubusercontent.com/kaspanet/kips/e4ae2332117b5cb68bd6188e065ef885b6d17939/kip-0020.md | Write pass | Status Active. Title Covenant IDs. Updated 2026-05-28. |
| `gh api repos/kaspanet/kips/commits/master` | Write pass | `e4ae2332117b5cb68bd6188e065ef885b6d17939` |
| https://kas-smiths.org/t/kcc-01-discussion-thread/141.json | Write pass | 1 post. OriNewman. Last activity 2026-08-29. |
| https://kas-smiths.org/t/kcc-02-control-principal-references-in-program-abis/95.json | Write pass | 4 posts. Last is OriNewman 2026-08-29 on domain separation. |
| https://kas-smiths.org/t/8.json and https://kas-smiths.org/posts/364.json | Write pass | `posts_count` 59, stream length 61, last id 364, post_number 73, Manyfest, `created_at` `2026-09-11T10:50:15.762Z`. |
| https://github.com/argent-lang/kcc20-reference | Write pass via `gh api` | master `76648f9938c474a5210f4b3b59b2e1b9ebae420f`. Pull 1 open, not merged, head `5b2a23124ef43730eca4f69248bc2866daf2c24c`, updated 2026-10-02T13:45:06Z. |
| Silverscript compiler source | Not cloned | KCC-2 already labels the snippets non-normative. No finding depends on an unread function body. |
| Rusty-kaspa sighash | Not opened | LC-10 is the missing sentence in KCC-20, not a claim about a node function. |

## Master, read-only until section 6 of the task

| URL | Note |
| --- | --- |
| https://github.com/STP-KAS/kaspa-master-file | Local `main` `99ae9620dd580ff0630cd720f83a0e78de616f4e`. PROCESS.md and AGENTS.md read. Now board already has the 1 Oct Last Call facts and the missing deadline. Reference cell still says pull head `60064687`. |
| https://github.com/STP-KAS/kaspa-master-bot-build-challenge | Not written. The task says not to push this audit there. |

## Deliberately not claimed

- No public issue, review, reaction, discussion, X post, Kas-Smiths post, or kccs.dev edit.
- No mainnet. No spend. No node restart.
- No tag and no release on this audit repo.
