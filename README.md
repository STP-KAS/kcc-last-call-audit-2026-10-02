# KCC Last Call audit, 2026-10-02

Private working note for STP-KAS. Prepared by Fermi. No public post.

## What

A sourced reading of KCC-0, KCC-1, KCC-2, and KCC-20 during the window announced on 2026-10-02. KCC means Kaspa Call for a Convention. It is voluntary interoperability. It is not a consensus change. KIPs change consensus or core-node behavior. A Final KCC is a convergence point, not protocol ground truth.

Audited tree: [kaspanet/kccs](https://github.com/kaspanet/kccs) `main` at [`411b41bc14b3fda8f3a0548242c555f3597cad1a`](https://github.com/kaspanet/kccs/commit/411b41bc14b3fda8f3a0548242c555f3597cad1a) (2026-10-01T13:15:20Z). Re-checked at write time: that SHA is still `main`. The repo has discussions disabled.

Verified deadline: **none**. KCC-0 requires a `Last-Call-Deadline` header while status is Last Call. `kcc-0001.md` and `kcc-0002.md` say `Status: Last Call` and do not contain that header. The post [2105991195583488410](https://x.com/kccforum/status/2105991195583488410) (2026-10-02 12:00:03 UTC) calls the window a final 14-day review. Fourteen days from that post would be 2026-10-16 12:00 UTC. That date is not in the files.

## Why

Wallets and indexers are being pointed at these documents. A status word in a header, a README row, a rendered site, and an X post are four different objects. This note records where they agree and where they do not.

## How

The canonical markdown at `411b41bc` was read in full for the four KCCs, the template, the license, the README, the KCC-1 JSON vectors, the KCC-2 JSON vectors, the KCC-2 reference-code file, and the KCC-20 borrowed-receive guide. Hashes in those vectors were recomputed with Python `blake3` 1.0.9. The index at https://kccs.dev/ was opened again at write time. KIP-17 and KIP-20 were opened at the commit KCC-1 pins, which is also the current `kaspanet/kips` `master` tip. The three Comments-URI threads were opened again at write time. Coverage gaps are listed in [COVERAGE.md](COVERAGE.md). Findings are in [AUDIT.md](AUDIT.md).

## Conclusion

Safe to treat as Last Call text, with the process defects below still open: the KCC-1 and KCC-2 byte rules whose vectors recomputed cleanly. That means the unkeyed BLAKE3 hash, the dispatch-tag rule, the P2SH envelope, the template hash, and the five KCC-2 scheme bytes `0x00` through `0x04`. Those documents already contain Security Considerations. A reference implementation is optional before Final and is not required to enter Last Call. KCC-2 says its own snippets are not a conformance-passing implementation.

Must be fixed before anyone treats the window as closed, and before Final:

1. An editor must write `Last-Call-Deadline` into both Last Call preambles. Until that header exists, KCC-0's clock is not running.
2. KCC-0 section 4.3 still says KCC-1, KCC-2, and KCC-20 retain Draft and must conform before Review. The headers of KCC-1 and KCC-2 say Last Call. Review does not appear in the KCC-1 history on this repo. The process document and the status lines disagree.
3. Final, later, still needs agreeing human and machine vectors, one public implementation that passes them and is linked from the KCC or its pull request, and every `Requires` entry Final (KCC) or Active (KIP). KCC-2 requires KCC-1, so KCC-2 cannot be Final until KCC-1 is Final. KIP-17 and KIP-20 are Active at the pin.

Do not ship a wallet against KCC-20 yet. On this commit it is Draft. The body uses lowercase "must", which KCC-0 says has no normative force. There is no Security Considerations section, no vectors directory, no `Requires` header, and the name `P2PKHHash` is not defined in the current KCC-1 or KCC-2. The signed message for a borrow signature is not defined. The July forum opening post describes a different ABI. [kaspanet/kccs#31](https://github.com/kaspanet/kccs/pull/31) is open and unmerged. [argent-lang/kcc20-reference](https://github.com/argent-lang/kcc20-reference) `master` is still the stub [`76648f9938c474a5210f4b3b59b2e1b9ebae420f`](https://github.com/argent-lang/kcc20-reference/commit/76648f9938c474a5210f4b3b59b2e1b9ebae420f). Pull request [#1](https://github.com/argent-lang/kcc20-reference/pull/1) head [`5b2a23124ef43730eca4f69248bc2866daf2c24c`](https://github.com/argent-lang/kcc20-reference/commit/5b2a23124ef43730eca4f69248bc2866daf2c24c) was updated 2026-10-02T13:45:06Z and is not merged.

Three blockers are written up as LC-1, LC-2, and LC-3.
