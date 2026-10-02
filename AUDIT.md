# Audit

Audited commit: [`411b41bc14b3fda8f3a0548242c555f3597cad1a`](https://github.com/kaspanet/kccs/commit/411b41bc14b3fda8f3a0548242c555f3597cad1a) on [kaspanet/kccs](https://github.com/kaspanet/kccs) `main`. Prepared by Fermi for STP-KAS. Private. 2026-10-02.

KCC-0 is the process. KCC-1 is the covenant ABI. KCC-2 is authority schemes. KCC-20 is the fungible-token covenant. A finding quotes the file it judges.

Line numbers are from that commit's files as checked out for this audit.

## Verdicts in short

| ID | Verdict | Subject |
| --- | --- | --- |
| LC-1 | blocker | KCC-1 and KCC-2 are Last Call with no `Last-Call-Deadline` |
| LC-2 | blocker | KCC-0 §4.3 still says those documents retain Draft |
| LC-3 | blocker | KCC-20 on main is not a convention a wallet can ship |
| LC-4 | should-fix | Status change was not posted on the Comments-URI threads |
| LC-5 | should-fix | KCC-1 header order and missing RFC 2119 boilerplate |
| LC-6 | should-fix | KCC-1 §6.8 state example disagrees with the JSON |
| LC-7 | should-fix | KCC-1 `int` table says "Eight-byte ScriptNum" |
| LC-8 | should-fix | KCC-2 cites KCC-1 sections that are not the definitions |
| LC-9 | should-fix | Final gate: human vectors for approval checks, and a passing implementation |
| LC-10 | should-fix | KCC-20 borrow signatures do not name the signed message |
| LC-11 | nit | `Created` dates and the extra `Updated` header |
| LC-12 | holds | Recomputed hashes, scheme bytes `0x00`–`0x04`, KIP-17 and KIP-20 Active |

---

## LC-1

- **What.** `kcc-0001.md` line 6 and `kcc-0002.md` line 7 say `Status: Last Call`. Neither preamble contains `Last-Call-Deadline`. The README rows for numbers 1 and 2 also say Last Call (README lines 14–15). https://kccs.dev/ shows the same two rows as Last Call.
- **Why it matters.** KCC-0 §4.2 says an editor assigns Last Call and sets `Last-Call-Deadline`, typically 14 days later (`kcc-0000.md` lines 154–157). The header table says that header is required when status is Last Call (lines 275–276). Without it, the 14 days in [post 2105991195583488410](https://x.com/kccforum/status/2105991195583488410) are a social claim. Fourteen days after 2026-10-02 12:00:03 UTC would be 2026-10-16 12:00 UTC. Fourteen days after the status commits on 2026-10-01 would be 2026-10-15. Neither date is in the files. A wallet author who waits for "the end of Last Call" is waiting on a date the process has not set.
- **How you checked.** Read the two preambles and `kcc-0000.md` lines 154–157 and 264–283. `gh api repos/kaspanet/kccs/commits/main` returned `411b41bc14b3fda8f3a0548242c555f3597cad1a`. Pull [#32](https://github.com/kaspanet/kccs/pull/32) merged as `815ecaff3071f5e227cc4b4cdb6c167ae2915666` at 2026-10-01T12:33:08Z and only flips KCC-1 from Draft to Last Call plus the README row. Pull [#33](https://github.com/kaspanet/kccs/pull/33) merged as `ad1b8996d648708c0ac6e351f950437c1b867c29` at 2026-10-01T12:52:21Z and does the same for KCC-2. Both were merged by michaelsutton. https://kccs.dev/ was fetched again on 2026-10-02 and lists KCC 1 and KCC 2 as Last Call.
- **Verdict.** blocker
- **Inconsistency.** KCC-0: "A KCC editor assigns Last Call status and sets a review end date (`Last-Call-Deadline`)." The files: `Status: Last Call` and no such header. The X post: a final 14-day review that will be finalized if no major issues are found. The header table: the deadline header is required when status is Last Call.
- **Proposed solution.** One pull request, for each of KCC-1 and KCC-2, that adds a real editor-chosen date:

  ```text
  Last-Call-Deadline: YYYY-MM-DD
  ```

  Place it after `Status` and before `Type`, which is the order in `kcc-0000.md` lines 275–277. Post that date on the Comments-URI thread in the same change. Do not treat 2026-10-16 as already chosen.
- **Alternative.** Move both documents back to `Review` until the deadline is chosen. That matches the sentence in LC-2. It is the stricter reading. The smaller interoperable fix is to keep Last Call and add the header in the same pull request that amends §4.3.
- **Sources.** `kcc-0000.md` lines 154–157, 275–276. `kcc-0001.md` lines 1–11. `kcc-0002.md` lines 1–11. README lines 14–15. https://kccs.dev/. https://github.com/kaspanet/kccs/pull/32. https://github.com/kaspanet/kccs/pull/33. https://x.com/kccforum/status/2105991195583488410.

## LC-2

- **What.** KCC-0 §4.3 still says KCC-1, KCC-2, and KCC-20 retain Draft and must be brought into conformance before Review. The status lines and the README say Last Call for 1 and 2, and Draft for 20.
- **Why it matters.** The process these documents just marked Final (`kcc-0000.md` status Final; README line 13; pull [#34](https://github.com/kaspanet/kccs/pull/34) `411b41bc` only updates the README index, the file was already Final since [#25](https://github.com/kaspanet/kccs/pull/25) `c0bb8f3babbb6a93dbddac900121e5046c1ec388` on 2026-09-21) still forbids the status that #32 and #33 wrote. A reader of §4.3 and a reader of the header cannot both be right. KCC-1's history on this repository goes from its birth commit to the Last Call flip. `Review` does not appear.
- **How you checked.** Read `kcc-0000.md` lines 197–204. Confirmed the rendered process page was read in the first pass against that paragraph; the index page fetched on 2026-10-02 still labels KCC 1 and KCC 2 Last Call. KCC-1 preamble has no earlier status left in the file.
- **Verdict.** blocker
- **Inconsistency.** §4.3: "KCC-1, KCC-2, and KCC-20 predate this document and retain their Draft status. Before entering Review, each must be brought into conformance with this document." Header of `kcc-0001.md`: `Status: Last Call`. Header of `kcc-0020.md`: `Status: Draft`, which matches the "retain Draft" half for KCC-20 only.
- **Proposed solution.** Replace §4.3 with text that matches the headers the editors actually want. If Last Call is the intended state, the replacement has to stop saying 1 and 2 retain Draft, and it has to wait until LC-1's header exists. Concrete replacement:

  ```text
  KCC-1, KCC-2, and KCC-20 predate this document. KCC-20 retains Draft
  status until it conforms to this document. KCC-1 and KCC-2 are in Last
  Call only while their preambles include Last-Call-Deadline and they meet
  the section requirements of Section 5, including Security Considerations
  and conformance vectors.
  ```

- **Alternative.** Revert #32 and #33 so the headers match §4.3, and enter Review only after the header, boilerplate, and vector gaps in LC-5 through LC-9 are closed.
- **Sources.** `kcc-0000.md` lines 197–204 and 154–176. README lines 13–16. https://github.com/kaspanet/kccs/pull/25. https://github.com/kaspanet/kccs/pull/32. https://github.com/kaspanet/kccs/pull/34.

## LC-3

- **What.** KCC-20 on `main` is Draft, and the current file is not something a wallet should implement. The 2026-10-02 posts talk about it progressing with KCC-1 and KCC-2. The file does not say Last Call.
- **Why it matters.** A wallet that ships the July forum ABI, the August markdown, the unmerged pull #31, and the unmerged Argent pull as one token will split balances. Those are different objects. KCC-0 §13 says lowercase "must" and "should" carry no normative force (`kcc-0000.md` lines 412–418). `kcc-0020.md` uses lowercase "must" and never uses `MUST`. Under the process document, the transfer and borrow rules in that file have no normative force.
- **How you checked.** Read `kcc-0020.md` (296 lines) and `kcc-0020/borrowed-receive-authorization.md`. Confirmed there is no `kcc-0020/vectors/` directory. Re-fetched https://kccs.dev/ : KCC 20 is Application, Covenant, Draft. Re-fetched the Comments-URI. The topic has `posts_count` 59 and a stream whose last id is 364. Raw `created_at` on post 364 is `2026-09-11T10:50:15.762Z`, username Manyfest, post_number 73. The text says the spec is maturing and reaching finalization and that he is working on the final reference implementation. It is not an October Last Call announcement. [Post 2106008195114381508](https://x.com/kccforum/status/2106008195114381508) says KCC-20 Last Call is pending peer review of the reference implementation. [Post 2106012029358047445](https://x.com/manyfest_/status/2106012029358047445) says KCC-20 needs a published reference implementation before it can be finalized and that the Argent reference is being audited toward Last Call.
- **Verdict.** blocker
- **Inconsistency.** Several, each quoted.

  1. Status. File line 7: `Status: Draft`. X posts above: progressing with 1 and 2, Last Call pending a reference review.
  2. Header. KCC-0 order is KCC, Title, Description, Authors, Comments-URI, Status, then Type, Category, Created (`kcc-0000.md` lines 268–279). KCC-20 lines 1–9 put `Category` before `Title`, omit `Description`, `Type`, and `Requires`, and add `Updated`, which is not a KCC-0 header. `Category: Application, Covenant` is two values. The header table allows one of Covenant, ABI, Application, or Interface (line 278).
  3. Authors. Lines 4–5 are `Name <email>` only. KCC-0 lines 294–295 require at least one GitHub username.
  4. Hash name. Lines 164–165 say `P2PKHHash(pubkey)` and `P2PKHHash(ecdsa_pubkey)`. That function is not defined in current `kcc-0001.md` or `kcc-0002.md`. Current KCC-2 lines 90–93 say the P2PKH schemes use unkeyed `Hash(x)` on the public-key bytes. At parent `c0bb8f3babbb6a93dbddac900121e5046c1ec388`, KCC-2 defined `P2PKHHash(pubkey) = Hash(pubkey, UTF8("PublicKeyHash"))`. That definition was removed by [#30](https://github.com/kaspanet/kccs/pull/30) `90beacd0dd34543a7321144d122189d779c5ad9b`. KCC-20's last commit is `3229efbbcbc57e5b75df750d1cf045298d1df8a0` on 2026-08-28, before #30. Recomputation: unkeyed BLAKE3 of 32 bytes `0x22` is `7caa514a05535fd97887e483ce6f1fc36ef7026435c47521b04549d9af4837bf`. Keyed `PublicKeyHash` of the KCC-2 sample 32-byte key is `91438cfb14e4fbb78c740ab72162162f203eafae88940707d43ce7e97268d582`, which does not equal the unkeyed sample `f9f2a0b353f482f415281da3a00929d08a7d9a6498054f5ef6623b5580e607f7`.
  5. Section numbers. Lines 82–84 cite "KCC1 Section 9.1" for the leader. Leader and delegator roles are `kcc-0001.md` §3.8.1 (line 675). Section 9 of KCC-1 is Copyright (line 1135). Lines 53 and 153 and 191 cite "KCC1 Section 10". KCC-1 ends at section 9. Virtual elements are §3.9 (line 709).
  6. Owner type. The state record types `owner` as `byte[32]` (lines 32–34). The scheme table types `0x00` as `pubkey` (line 163). KCC-1 dispatch tags are built from record field types, not from the scheme table's word. The file never prints a dispatch tag. Under the state-record types, the KCC-1 preimage `transfer({int,byte[32],byte,byte,byte[32],byte[32]}[],byte[])` hashes to tag `79c71c23`. That tag is not written in `kcc-0020.md`.
  7. Prose and pseudocode. Lines 279–286 say the borrowed successor must preserve `owner`, `owner_scheme`, `borrow_scheme`, and `extension_commitment`, and that the leader must preserve the total token amount. The pseudocode at lines 250–272 checks the scheme, the guard, and `amount_difference > amount_threshold`. It does not check the owner or the sum. KCC-0 §5 says that when prose and pseudocode state the same rule, the specification says which is authoritative (`kcc-0000.md` lines 223–224). This file does not.
  8. KIP link. Line 296 links KIP-20 at `blob/master`, unpinned. KCC-0 §8.1 says a normative KIP link is pinned to a commit (lines 307–310). KCC-1 pins `e4ae2332117b5cb68bd6188e065ef885b6d17939`.
  9. Reference. No implementation is linked from `kcc-0020.md`. `argent-lang/kcc20-reference` `master` is `76648f9938c474a5210f4b3b59b2e1b9ebae420f`, whose README is the stub title. Pull [#1](https://github.com/argent-lang/kcc20-reference/pull/1) is open, not merged, head `5b2a23124ef43730eca4f69248bc2866daf2c24c`, updated 2026-10-02T13:45:06Z. There is no `kcc-0020/vectors/` tree, so there is nothing for that pull to pass on `main`.
  10. Forum opening versus the file. The opening post of topic 8 is a July draft. The merged file's state is amount, owner, owner_scheme, borrow_scheme, borrow_guard, extension_commitment. The opening discussion used a different identifier layout. Post 364 does not replace that opening post and does not announce Last Call.

- **Proposed solution.** Leave `Status: Draft`. Do not merge a Last Call label onto this file until all of the following are in the same pull request:
  - RFC 2119 boilerplate and capitalized normative words.
  - One `Category`, a `Type: Standards Track`, a `Description`, a `Requires: KCC-1, KCC-2, KIP-20`, and at least one `(@username)`.
  - Replace `P2PKHHash(...)` with unkeyed `Hash(x)` as KCC-2 §2.2 defines it, and cite KCC-1 §3.2.1.
  - Replace "Section 9.1" with "Section 3.8.1" and "Section 10" with "Section 3.9".
  - A Security Considerations section that defines the signed message and the sighash, and that states whether prose or pseudocode wins.
  - Human and JSON vectors, including the reject cases.
  - A copyright waiver line as in KCC-0 §5.
  - Pin the KIP-20 URL to `e4ae2332117b5cb68bd6188e065ef885b6d17939` or to a newer commit the editor names.

  [kaspanet/kccs#31](https://github.com/kaspanet/kccs/pull/31) head `cfb74cfa4d7e25f3e7ec0f9144ad72c460b9d810` is the open attempt at a lot of that header work. It is not on `main`. Its security text still says the document does not restrict the sighash type. It still has no `Last-Call-Deadline`. It still cites KCC-1 Section 9.1 and Section 10 and still writes `P2PKHHash`. Two example digests in that pull, `P2PKHHash` of 32 bytes `0x22` and of `0x02 || 0x55^32`, recompute as unkeyed BLAKE3 (`7caa514a...` and `ed887ad1...`). The name in the pull is still undefined. Do not treat #31 as the convention.
- **Alternative.** Freeze KCC-20 as Informational notes and write a new number once the ABI, the hash, and the sighash are stable. That is larger. The small fix is to repair this number in place while it is still Draft, which §4.3 already requires before Review.
- **Sources.** `kcc-0020.md` lines 1–10, 31–39, 82–84, 162–170, 245–296. `kcc-0000.md` lines 245–254, 268–295, 307–310, 412–418. `kcc-0001.md` lines 130–135, 675, 709, 1135. `kcc-0002.md` lines 90–103. Parent text at `c0bb8f3babbb6a93dbddac900121e5046c1ec388`. https://kccs.dev/. https://kas-smiths.org/posts/364.json (`created_at` `2026-09-11T10:50:15.762Z`). https://github.com/kaspanet/kccs/pull/31. https://github.com/argent-lang/kcc20-reference/pull/1. https://x.com/kccforum/status/2106008195114381508. https://x.com/manyfest_/status/2106012029358047445. Vector command output in [VECTORS.md](VECTORS.md).

## LC-4

- **What.** KCC-0 says every status change except the initial Draft merge should be announced at the `Comments-URI` (`kcc-0000.md` lines 191–192). The word is lowercase "should". §13 says lowercase forms have no normative force. The threads were still not updated.
- **Why it matters.** The public record the process points at still answers older questions. A reader of topic 141 or topic 95 does not learn that the status line changed on 2026-10-01.
- **How you checked.** `https://kas-smiths.org/t/kcc-01-discussion-thread/141.json`: `posts_count` 1, last post id 354, username OriNewman, `last_posted_at` rendered 08/29/2026 08:35:42. The post asks about `add_i64` versus minimal ScriptNum and about `bool` encoding. `https://kas-smiths.org/t/kcc-02-control-principal-references-in-program-abis/95.json`: `posts_count` 4, last post id 355, OriNewman, 08/29/2026 09:05:46, preferring no domain-separation key. That preference matches what #30 later did. Topic 8's last post is 364 on 2026-09-11, quoted under LC-3.
- **Verdict.** should-fix
- **Inconsistency.** Process sentence asks for an announcement. The three threads' last posts predate 2026-10-01. The lowercase word means this is not an RFC 2119 failure. It is still the discussion record the header names.
- **Proposed solution.** The editor posts the status, the deadline from LC-1, and a pointer at the merge commits on topic 141 and topic 95. Topic 8 gets a post only when KCC-20's status actually changes.
- **Alternative.** Leave the threads as they are and change `Comments-URI` to a place that will receive the announcement. The existing threads are the ones the preambles name.
- **Sources.** `kcc-0000.md` lines 191–195 and 412–418. `kcc-0001.md` line 11. `kcc-0002.md` line 6. The three topic JSON URLs above. https://kas-smiths.org/posts/364.json.

## LC-5

- **What.** KCC-1's preamble order is KCC, Title, Description, Authors, Status, Type, Category, Created, Requires, Comments-URI. KCC-0 puts `Comments-URI` after Authors and before Status. KCC-1 uses `MUST` and does not include the RFC 2119 boilerplate. KCC-2 does include it (lines 30–34).
- **Why it matters.** KCC-0 §5 says normative requirements use the capitalized key words and include the boilerplate (`kcc-0000.md` lines 220–223). §13 repeats the boilerplate and says lowercase forms have no force. KCC-1's `MUST` lines are the normative core of the ABI. The boilerplate is what tells a reader those words are RFC 2119. The header-order miss is editorial. The missing boilerplate is the part a lawyer or a second implementer will trip on.
- **How you checked.** Compared `kcc-0001.md` lines 1–11 with `kcc-0000.md` lines 268–283 and 412–418. Searched `kcc-0001.md` for the boilerplate sentence. It is absent. `MUST` is used from §3.2.1 onward (first hit line 137).
- **Verdict.** should-fix
- **Inconsistency.** KCC-0 requires the boilerplate in the specification section. KCC-1's specification section starts at line 92 with no boilerplate. KCC-2 has it.
- **Proposed solution.** Move `Comments-URI` to sit after `Authors`. Insert, at the start of §3, the sentence already printed in `kcc-0000.md` lines 414–417 and already used by KCC-2.
- **Alternative.** Stop using `MUST` in KCC-1 until the boilerplate is added. That would strip the normative force the vectors assume. Adding the boilerplate is the smaller fix.
- **Sources.** `kcc-0000.md` lines 220–223, 268–283, 412–418. `kcc-0001.md` lines 1–11 and 137. `kcc-0002.md` lines 30–34.

## LC-6

- **What.** §6.8 prints a 44-byte state for pubkey, int counter `-5`, and bool. The JSON vector for `state_encoding` inserts a string label `Kaspa` and says `encoded_length` 50.
- **Why it matters.** KCC-0 says the human and machine vectors must agree, and the machine form is authoritative for automated testing (`kcc-0000.md` lines 235–240). A test runner that encodes the prose example fails the JSON. A test runner that encodes the JSON fails the prose length.
- **How you checked.** Read `kcc-0001.md` lines 959–981 and `kcc-0001/vectors/conformance.json` lines 639–667.
- **Verdict.** should-fix
- **Inconsistency.** Prose: fields `pubkey key = 07^32`, `int counter = -5`, `bool enabled = true`, then "The 44-byte encoded state is" `2007…0708050000000000800101`. JSON: four fields, the second named `label`, type `string`, value `Kaspa`, encoded `054b61737061`, `encoded_length` 50, hex `2007…07054b6173706108050000000000800101`.
- **Proposed solution.** Pick the JSON, which KCC-0 says is authoritative. Change §6.8 so the field list includes `string label = Kaspa` and the length is 50, with the JSON hex. If the 44-byte example is the one the editors want, delete the label from the JSON and set `encoded_length` to 44.
- **Alternative.** Label the prose example as a different vector id so the two are no longer presented as the same case.
- **Sources.** `kcc-0001.md` lines 959–981. `kcc-0001/vectors/conformance.json` lines 639–667. `kcc-0000.md` lines 235–240.

## LC-7

- **What.** The scalar table calls the `int` payload "Eight-byte ScriptNum" (`kcc-0001.md` line 247). §3.4.3 says an argument is minimal ScriptNum and a state payload is eight-byte little-endian signed-magnitude (lines 231–239). The vector row for `-5` is argument `0185` and state `0500000000000080` (line 870).
- **Why it matters.** ScriptNum and signed-magnitude are different byte strings for the same integer. The table row collapses them into one cell. An implementer who encodes state as ScriptNum will not match the vector.
- **How you checked.** Read those lines side by side. The JSON `state_encoding` counter for `-5` is `080500000000000080`, which is the push length plus the signed-magnitude payload.
- **Verdict.** should-fix
- **Inconsistency.** §3.4.3 names signed-magnitude for state. The table says "Eight-byte ScriptNum". The vector bytes match signed-magnitude with the sign in the high bit of the last byte (`0500000000000080` for `-5`). §3.4.3 does not say which bit holds the sign. The vector and §6.4 do.
- **Proposed solution.** Change the table cell to: "State: eight-byte little-endian signed-magnitude, sign in the high bit of the last byte. Argument: minimal ScriptNum via PushMinimal." Add one sentence to §3.4.3 that names that bit, copying the vector.
- **Alternative.** Leave the table and add "see §6.4" in the cell. Weaker, because the wrong noun stays.
- **Sources.** `kcc-0001.md` lines 231–239, 247, 865–874. `conformance.json` lines 654–658.

## LC-8

- **What.** KCC-2 cites three KCC-1 section numbers that are not where those rules live. The local formulas and the JSON still match a recomputation.
- **Why it matters.** A reader who follows the citation lands in the wrong section and can implement the old keyed hash, or look for a section 11 that does not exist.
- **How you checked.** Read the citations and the target headings.
- **Verdict.** should-fix
- **Inconsistency.**

  | KCC-2 says | At `411b41bc` that section is | The rule actually lives at |
  | --- | --- | --- |
  | "unkeyed `Hash(x)` form defined by KCC-1 Section 3.1" (line 90) | §3.1 Scope and Dependencies (line 94) | §3.2.1 Hash Function (line 130) |
  | "commitment as defined by KCC-1 Section 7" (line 110) | §7 Security Considerations (line 1043) | §3.6 P2SH Covenant Envelope (line 438) |
  | "KCC-1 Section 11.2 hash fixture `R = 51`" (line 225) | no section 11; §9 is Copyright | §6.7 P2SH Envelope (line 942) |

  The bytes next to those citations are still right: authority value `ce57216285125006ec18197bd8184221cefa559bb0798410d99a5bba5b07cd1d` and script `aa20` + that hash + `87` (lines 214–216). Recomputed BLAKE2b-32 of `51` matches.
- **Proposed solution.** Replace the three citations with §3.2.1, §3.6, and §6.7.
- **Alternative.** Add a one-line alias in KCC-1. That keeps stale numbers alive. Fixing the citations is smaller.
- **Sources.** `kcc-0002.md` lines 90–93, 109–112, 211–228. `kcc-0001.md` lines 94, 130, 438, 942, 1043, 1135. [VECTORS.md](VECTORS.md).

## LC-9

- **What.** Final is a higher bar than Last Call. KCC-0 §4.2 requires, in addition to a completed Last Call: human and machine vectors that agree, at least one public implementation that passes the machine vectors and is linked from the KCC or its pull request, and every `Requires` entry Final (KCC) or Active (KIP) (`kcc-0000.md` lines 166–176). §5 says a reference implementation is optional before Final (lines 241–244). Security Considerations are required before Last Call (lines 245–250). KCC-1 and KCC-2 have Security Considerations. They do not yet have the Final ingredients.
- **Why it matters.** The X post says the documents will be finalized if no major issues are found. Final is not automatic at day 14, and day 14 is not set (LC-1). KCC-2 `Requires: KCC-1, KIP-20`. KCC-1 is not Final. KIP-20 is Active. So KCC-2 cannot become Final in the same breath as KCC-1. KCC-1 `Requires: KIP-20, KIP-17`, both Active, so the KIP half of KCC-1's Final gate holds.
- **How you checked.** Read those KCC-0 lines. Read KCC-2 §5 (lines 246–250): "These snippets are not a complete application or a demonstrated conformance-passing implementation." Counted `approval_checks` in `authority-schemes.json`: 20 entries, 11 of which carry `signature_valid` in the context. Those are boolean oracles. They do not check a signature. The human §4.2 describes the oracle. It does not restate each of the 20 rows. `registry_checks` are JSON-only. KCC-1's constructions are in both the markdown §6 and the JSON. The state-length pair in LC-6 is the place they disagree.
- **Verdict.** should-fix before Final. Not a Last Call defect by itself. Reference code is labeled non-normative in `kcc-0002/reference-code.md` line 3, and the main text repeats that. Do not read those snippets as the specification.
- **Inconsistency.** Post 2105991195583488410: finalized for ecosystem adoption if no major issues are found. KCC-0: Final needs a finished Last Call plus the three gates above. KCC-2: the linked snippets are not that implementation.
- **Proposed solution.** Before any Final pull request: publish one implementation, run it on the JSON, link the commit from the KCC, copy every `approval_checks` and `registry_checks` row into the markdown or add a sentence that the JSON list is the human list by inclusion, and move KCC-1 to Final before KCC-2.
- **Alternative.** Keep both at Last Call and say so in the Comments-URI, so the X wording is corrected by the process thread.
- **Sources.** `kcc-0000.md` lines 166–176 and 241–250. `kcc-0002.md` lines 11, 230–250. `kcc-0001.md` lines 10–11. `kcc-0002/vectors/authority-schemes.json`. KIP headers below in LC-12. https://x.com/kccforum/status/2105991195583488410.

## LC-10

- **What.** The hash-chain borrow patch binds the one-time public key into the guard. It does not define the bytes that the signature covers.
- **Why it matters.** KCC-1 §7.4 says the transaction id does not commit to the signature script, and that arguments are not evidence of signer intent unless a signature covers them (`kcc-0001.md` lines 1113–1124). A borrow witness sits in that signature script. KCC-2 lines 102–103 say the higher-level convention defines the signed message. KCC-20 is that convention. Its hash-chain rule says `verify borrow_signature with one_time_pubkey` (lines 260–264) and calls the witness "a 65-byte Schnorr transaction signature" (line 230). It never names a sighash. The borrowed-receive guide is an explanation (lines 217–218). KCC-0 says auxiliary material is non-normative unless the main document says otherwise. The guide's `VerifySchnorr(pubkey, transaction, signature)` is not a sighash.
- **How you checked.** Read `kcc-0020.md` §5 and the top of the guide. Commit `3229efbbcbc57e5b75df750d1cf045298d1df8a0` is the last commit that touches `kcc-0020.md` (`git log -1 -- kcc-0020.md`). The current rule is `Hash(revealed_guard || one_time_pubkey) == borrow_guard` with unkeyed BLAKE3 (lines 247–263). That closes the old "copy the 32-byte preimage" race. It does not close a signature that can be reused under a sighash that omits outputs.
- **Verdict.** should-fix. It sits inside LC-3 for as long as KCC-20 is the document a wallet would ship. It is not a defect in the KCC-1 hash or the KCC-2 scheme bytes.
- **Inconsistency.** KCC-2: the consumer defines the signed message. KCC-20: "transaction signature" and "verify … with one_time_pubkey", and no message. Open pull #31's security section says the document does not restrict the sighash type of a signature in `witness`. That sentence, on the unmerged head `cfb74cfa4d7e25f3e7ec0f9144ad72c460b9d810`, admits the gap in the pull that would otherwise move KCC-20 forward.
- **Proposed solution.** In KCC-20 Security Considerations, require one consensus sighash that commits to the outputs the borrow is allowed to create, and name it. State that the signature covers that sighash of the spending transaction and no other message. Put the same sentence in the pseudocode as `verify`.
- **Alternative.** Require the covenant script to check the output set itself and treat the signature as proof of the one-time key only. That works only if the script's output checks are normative and complete. Today the owner and amount-sum checks are prose beside a shorter pseudocode (LC-3 item 7), so this alternative is unsafe until those checks are in the normative text.
- **Sources.** `kcc-0020.md` lines 217–218, 226–272, 279–286. `kcc-0001.md` lines 1113–1124. `kcc-0002.md` lines 102–103. https://github.com/kaspanet/kccs/commit/3229efbbcbc57e5b75df750d1cf045298d1df8a0. Raw `kcc-0020.md` on `cfb74cfa4d7e25f3e7ec0f9144ad72c460b9d810`.

## LC-11

- **What.** `Created` does not match the merge date on three of the four files. KCC-20 also carries `Updated: 2026-08-25`, which is not a KCC-0 header, and the file's last commit is 2026-08-28.
- **Why it matters.** KCC-0 defines `Created` as the date the KCC was merged as a Draft (`kcc-0000.md` line 279). A wrong date is how later "this predates the process" arguments get their facts wrong.
- **How you checked.** `git log --diff-filter=A -- kcc-0020.md` is `e31a5a855bdebd3bdc4456e5bd40179e9f98a3e8` at 2026-08-21T02:13:31+03:00. Header line 8 says `Created: 2026-07-15`. Last commit on the file is `3229efbb` at 2026-08-28T11:35:42+03:00. KCC-2 `Created: 2026-08-20` matches its birth. KCC-0's header says 2026-08-25 and the Final text's birth is the later process work; KCC-1's header says 2026-07-16. Those two dates were recorded from the headers and the commit list in the read pass. The KCC-20 pair was re-checked at write time.
- **Verdict.** nit
- **Inconsistency.** Header `Created: 2026-07-15` versus the adding commit on 2026-08-21. Header `Updated: 2026-08-25` versus the last touch on 2026-08-28.
- **Proposed solution.** Set `Created` to the merge date in `YYYY-MM-DD` from the adding commit, and delete `Updated`.
- **Alternative.** Keep the original drafting date and add a sentence that `Created` here means first public draft rather than merge. That contradicts KCC-0's definition. Deleting the contradiction is smaller.
- **Sources.** `kcc-0020.md` lines 8–9. `kcc-0000.md` line 279. `git log` output for `e31a5a855bdebd3bdc4456e5bd40179e9f98a3e8` and `3229efbbcbc57e5b75df750d1cf045298d1df8a0`.

## LC-12

- **What.** The computations and the dependency statuses that do hold.
- **Why it matters.** The process defects above are not a license to throw out the byte rules that already match.
- **How you checked.** Python `blake3` 1.0.9 against the JSON and the prose fixtures. Command and output: [VECTORS.md](VECTORS.md). KIP headers fetched from the commit named in `kcc-0001.md` lines 1130–1133. `gh api repos/kaspanet/kips/commits/master` returned the same SHA.
- **Verdict.** holds
- **Inconsistency.** None on these points. The stale section numbers in LC-8 point at the right bytes and the wrong headings. Both are true.
- **Proposed solution.** None for the hashes. Fix the headings under LC-8.
- **Alternative.** None.
- **Sources.**
  - Unkeyed BLAKE3 of the empty string: `af1349b9f5f9a1a6a0404dea36dcc9499bcb25c9adc112b7cc9a93cae41f3262`.
  - Unkeyed BLAKE3 of UTF-8 `KCC-1`: `4573a3e94e92dee5d41e7ba2c77d6f70a54829760d21c11ca25705374aa7f777`.
  - Keyed empty message, key UTF-8 `KCC-1` zero-padded to 32 bytes: `e98d9a91064b431e242efd29780956e5736812bdb4cd6f2a7e388e80bb61f3fb`.
  - Dispatch tags: `step(int,byte[4],bool,byte)` → `2c49ed65`. `dispense({byte[4],byte,bool}[])` → `676b1a86`.
  - KCC-2 sample unkeyed hashes: 32-byte `79be667e…` → `f9f2a0b353f482f415281da3a00929d08a7d9a6498054f5ef6623b5580e607f7`. 33-byte `0279be66…` → `1a15d6547364ad963c3b840e885639bb8136a4de757c0e7cf63f5de2f1cfbdbe`. Keyed domain `PublicKeyHash` does not match those (`91438cfb…` and `4ba1a5f9…`).
  - BLAKE2b-32 of redeem script `51`: `ce57216285125006ec18197bd8184221cefa559bb0798410d99a5bba5b07cd1d`. Script `aa20` + hash + `87`.
  - Template hash of `61` and `6263`: `405e183e2494cdbe2df89349cc0ffa5b77fb885ad97a1d5660ecd0692ef8142a`. The rejected construction `Hash(prefix || suffix)` for `61 || 6263` is `6437b3ac38465133ffb63b75273a8db548c558465d79db03fd359c6cd5bd9d85`.
  - Scheme bytes in KCC-2 §2.1 and in KCC-20 lines 162–167 agree for `0x00` through `0x04`. The hash function applied to `0x01` and `0x02` does not agree, because of the undefined name in LC-3.
  - KIP-17 at `e4ae2332117b5cb68bd6188e065ef885b6d17939`: `Status: Active`, Title "Covenants and Improved Scripting Capabilities", Updated 2026-05-31.
  - KIP-20 at the same commit: `Status: Active`, Title "Covenant IDs", Updated 2026-05-28.
  - `kaspanet/kips` `master` tip on 2026-10-02: `e4ae2332117b5cb68bd6188e065ef885b6d17939`.

## What was judged and left as holds or out of scope

- KCC-1 Security Considerations exist (§7, line 1043), including malleability in §7.4. §7.5 Design Decisions is the text `N/A` (line 1128). That is thin. It is not an absent section, so it is not the Last Call gate in `kcc-0000.md` lines 245–250.
- KCC-2 Security Considerations exist (line 252) and say consensus validity is not application authorization.
- Open pulls that do not edit the four audited files' normative text on `main`: [#24](https://github.com/kaspanet/kccs/pull/24) (KCC-0012), [#26](https://github.com/kaspanet/kccs/pull/26) (KCC-0023), [#29](https://github.com/kaspanet/kccs/pull/29) (KCC-0003, KCC-0004, KCC-0005). They are out of this Last Call. File lists were taken from `gh api repos/kaspanet/kccs/pulls/{24,26,29}/files`.
- Issue [#14](https://github.com/kaspanet/kccs/issues/14) (extension commitment partitions supply) is still open. The current §4 says states are fungible only when commitments match. That is specified. The missing piece is a Security Considerations warning, which folds into LC-3.
- Issue [#28](https://github.com/kaspanet/kccs/issues/28) records that more than one public object uses the name KCC-20. This audit does not weld them. No comment was added.
- Editor abstention: `kcc-0000.md` lines 398–399 say an editor who authored a KCC should abstain when more than one editor exists. The word is lowercase. michaelsutton authored KCC-1 and KCC-2 and merged #32 and #33. This audit did not fetch CODEOWNERS, so it does not claim a head count of editors. Left as unverified, not as a blocker.
- Silverscript `checkSigECDSA` and the real `blake3` binding were not opened in the compiler source. KCC-2 already says the snippets are not a passing implementation (LC-9). No finding here depends on a guessed function body.
- Rusty-kaspa sighash source was not opened. LC-10 rests on the spec gap, not on a node function.
