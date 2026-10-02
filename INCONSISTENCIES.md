# Inconsistencies

Both sides are quoted or cited. The audited commit is `411b41bc14b3fda8f3a0548242c555f3597cad1a`. Finding ids point at [AUDIT.md](AUDIT.md).

| ID | Side A | Side B |
| --- | --- | --- |
| LC-1 | KCC-0 lines 154–157 and 276: Last Call sets `Last-Call-Deadline`, and the header is required at that status. | `kcc-0001.md` line 6 and `kcc-0002.md` line 7: `Status: Last Call`, and the header is absent. https://kccs.dev/ and the README say Last Call too. |
| LC-1 | [Post 2105991195583488410](https://x.com/kccforum/status/2105991195583488410) (2026-10-02 12:00:03 UTC): final 14-day review. | No date in either preamble. 2026-10-16 12:00 UTC is arithmetic on the post, not a header. |
| LC-2 | `kcc-0000.md` lines 199–200: KCC-1, KCC-2, and KCC-20 retain Draft and must conform before Review. | Headers and README: KCC-1 and KCC-2 are Last Call. KCC-20 is Draft, which matches §4.3 for that one file. |
| LC-3 | `kcc-0020.md` line 7: `Status: Draft`. https://kccs.dev/ : Draft. | [Post 2106008195114381508](https://x.com/kccforum/status/2106008195114381508) and [post 2106012029358047445](https://x.com/manyfest_/status/2106012029358047445): KCC-20 is progressing with 1 and 2, Last Call waiting on a reference review. |
| LC-3 | Kas-Smiths post 364, `created_at` `2026-09-11T10:50:15.762Z`, Manyfest: the spec is maturing toward finalization and he is working on the reference implementation. | That post is the last one on topic 8. It is not an October status announcement. Topic `posts_count` is 59. The stream's last id is 364, post_number 73. |
| LC-3 | KCC-20 lines 164–165: `P2PKHHash(pubkey)`. | KCC-2 lines 90–93 at this commit: unkeyed `Hash(x)` on the public-key bytes. The name `P2PKHHash` is not defined here. At `c0bb8f3` it was `Hash(pubkey, UTF8("PublicKeyHash"))`. |
| LC-3 | KCC-20 lines 82–84 and 153: KCC-1 Section 9.1 and Section 10. | KCC-1: leader is §3.8.1 (line 675). Virtual elements are §3.9 (line 709). Section 9 is Copyright (line 1135). There is no section 10. |
| LC-3 | KCC-20 state record: `owner: byte[32]`. | Scheme table line 163: `0x00` value typed `pubkey`. |
| LC-3 | Prose lines 279–286: preserve owner, schemes, extension commitment, and total token amount. | Pseudocode lines 250–272: scheme, guard, and amount increase only. The file does not say which wins. |
| LC-3 | KCC-1 pins KIP-20 to commit `e4ae2332117b5cb68bd6188e065ef885b6d17939`. | KCC-20 line 296 links `https://github.com/kaspanet/kips/blob/master/kip-0020.md`. |
| LC-3 | Manyfest post: Argent reference being audited so KCC-20 can reach Last Call. | `argent-lang/kcc20-reference` master `76648f9938c474a5210f4b3b59b2e1b9ebae420f` is a stub. Pull #1 head `5b2a23124ef43730eca4f69248bc2866daf2c24c` is unmerged. `main` has no KCC-20 vectors. |
| LC-4 | KCC-0 lines 191–192: announce status changes at Comments-URI. The word is lowercase "should". | Topic 141 last post id 354 on 2026-08-29. Topic 95 last post id 355 on 2026-08-29. Topic 8 last post id 364 on 2026-09-11. |
| LC-5 | KCC-0 puts Comments-URI after Authors, and asks for the RFC 2119 boilerplate. | KCC-1 puts Comments-URI after Requires (line 11) and uses `MUST` with no boilerplate. KCC-2 has the boilerplate (lines 30–34). |
| LC-6 | §6.8: 44-byte state, three fields, hex ending `0805000000000000800101`. | JSON lines 639–667: label `Kaspa` (`054b61737061`), `encoded_length` 50. KCC-0 says the JSON wins for automated testing. |
| LC-7 | §3.4.3: state int is eight-byte little-endian signed-magnitude. Vector `-5` is `0500000000000080`. | Table line 247: "Eight-byte ScriptNum". |
| LC-8 | KCC-2 cites KCC-1 §3.1, §7, and §11.2. | Those headings are Scope, Security Considerations, and a section that does not exist. The formulas beside the citations match §3.2.1, §3.6, and §6.7. |
| LC-9 | Post 2105991195583488410: finalized if no major issues. | KCC-0 lines 166–176: Final also needs vectors in both forms, a public implementation that passes them, and Final/Active dependencies. KCC-2 requires KCC-1, which is not Final. KCC-2 lines 248–250: the snippets are not a conformance-passing implementation. |
| LC-10 | KCC-2 lines 102–103: the consumer defines the signed message. | KCC-20 lines 230 and 264: "65-byte Schnorr transaction signature" and "verify borrow_signature with one_time_pubkey", no sighash. Unmerged #31 says it does not restrict sighash. |
| LC-11 | KCC-20 `Created: 2026-07-15` and `Updated: 2026-08-25`. | Adding commit `e31a5a855bdebd3bdc4456e5bd40179e9f98a3e8` at 2026-08-21T02:13:31+03:00. Last commit `3229efbbcbc57e5b75df750d1cf045298d1df8a0` at 2026-08-28T11:35:42+03:00. |
| Site | https://kccs.dev/ index: KCC 0 Final, KCC 1 Last Call, KCC 2 Last Call, KCC 20 Draft. Four documents. | README lines 13–16 say the same four statuses. The site and the README agree. They both disagree with KCC-0 §4.3. |
| Master | STP-KAS/kaspa-master-file `main` `99ae9620dd580ff0630cd720f83a0e78de616f4e` already says KCC-1 and KCC-2 are Last Call with no `Last-Call-Deadline`, and that a missing deadline is not a set end date. | The same board still pins argent-lang/kcc20-reference pull #1 at `60064687` (27 Sep). Live head on 2026-10-02 is `5b2a23124ef43730eca4f69248bc2866daf2c24c`. The board does not yet quote §4.3 or the 2 Oct posts. |

Kaspaexplained `/status` was not re-fetched in the write pass. The master already records that on 2026-10-02 07:58 CEST it still said all three were Draft. The kccs files win. This table does not add a new quote from that site.
