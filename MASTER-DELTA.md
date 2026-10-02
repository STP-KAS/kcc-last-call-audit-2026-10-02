# Master delta

Facts only. Recommendations stay in [AUDIT.md](AUDIT.md).

Compared with STP-KAS/kaspa-master-file `main` `99ae9620dd580ff0630cd720f83a0e78de616f4e` on 2026-10-02. That board already says KCC-1 and KCC-2 are Last Call since #32 `815ecaff` and #33 `ad1b8996`, that neither header has `Last-Call-Deadline`, that KCC-20 is Draft, that #30 merged the unkeyed hash, and that a Last Call header with no deadline is not a set end date. Do not paste those sentences again.

## Replace the KCC20 reference pin

The Now cell and the matching `master.json` note still name open [argent-lang/kcc20-reference#1](https://github.com/argent-lang/kcc20-reference/pull/1) head `60064687` (27 Sep). Live `gh api` on 2026-10-02:

- Pull 1 is open, `merged` false, base `master`.
- Head is [`5b2a23124ef43730eca4f69248bc2866daf2c24c`](https://github.com/argent-lang/kcc20-reference/commit/5b2a23124ef43730eca4f69248bc2866daf2c24c), `updated_at` `2026-10-02T13:45:06Z`.
- `master` is still [`76648f9938c474a5210f4b3b59b2e1b9ebae420f`](https://github.com/argent-lang/kcc20-reference/commit/76648f9938c474a5210f4b3b59b2e1b9ebae420f).

Replacement sentence: Open argent-lang/kcc20-reference#1 head is `5b2a23124ef43730eca4f69248bc2866daf2c24c` (updated 2026-10-02T13:45:06Z). Not merged. `master` is still `76648f99`. The 27 Sep pin `60064687` is no longer the pull head.

## Add to the KCC row, sourced

On kaspanet/kccs `411b41bc14b3fda8f3a0548242c555f3597cad1a`, `kcc-0000.md` lines 199–200 still say KCC-1, KCC-2, and KCC-20 retain their Draft status and must conform before Review. The headers in that same commit say Last Call for KCC-1 and KCC-2, and Draft for KCC-20.

[@kccforum 2105991195583488410](https://x.com/kccforum/status/2105991195583488410) (2026-10-02 12:00:03 UTC) calls that Last Call a final 14-day review. [@kccforum 2106008195114381508](https://x.com/kccforum/status/2106008195114381508) (13:07:36 UTC) says KCC-20 Last Call is pending reference review. [@manyfest_ 2106012029358047445](https://x.com/manyfest_/status/2106012029358047445) (13:22:50 UTC) says KCC-20 progresses with 1 and 2 and that the Argent reference is being audited toward Last Call. No `Last-Call-Deadline` was added to the files after those posts. `main` was still `411b41bc` when this note was written.

Comments-URI threads, re-read 2026-10-02: topic 141 has one post (id 354, OriNewman, 2026-08-29). Topic 95 has four posts; the last is id 355, OriNewman, 2026-08-29. Topic 8 `posts_count` is 59; the stream's last id is 364, post_number 73, Manyfest, `created_at` `2026-09-11T10:50:15.762Z`. None of those posts is an October Last Call announcement.

## Add to the do-not-weld line

An X post that says "14 days" is not a `Last-Call-Deadline`. The header is still absent at `411b41bc`.

## Do not add

- Any recommended wording, sighash choice, or status revert. Those are in the audit.
- A second copy of the 1 Oct Last Call commits.
- A claim that kaspaexplained changed. It was not re-fetched for this delta.
