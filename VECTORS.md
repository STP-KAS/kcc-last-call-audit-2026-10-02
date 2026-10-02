# Vectors

Audited commit `411b41bc14b3fda8f3a0548242c555f3597cad1a`. Python package `blake3` 1.0.9. No transaction was built. No node was used.

## Command

Local checker against the checkout of kaspanet/kccs at that commit. It reads `kcc-0001/vectors/conformance.json` and `kcc-0002/vectors/authority-schemes.json`, recomputes BLAKE3 and BLAKE2b, and compares them to the files. The checker is not part of this repo.

Result on 2026-10-02: `FAILS 0`.

```text
PASS kcc1 unkeyed-empty af1349b9f5f9a1a6a0404dea36dcc9499bcb25c9adc112b7cc9a93cae41f3262
PASS kcc1 unkeyed-kcc-1 4573a3e94e92dee5d41e7ba2c77d6f70a54829760d21c11ca25705374aa7f777
PASS kcc1 keyed-empty key32 4b43432d31000000000000000000000000000000000000000000000000000000
PASS kcc1 keyed-empty e98d9a91064b431e242efd29780956e5736812bdb4cd6f2a7e388e80bb61f3fb
TAG step 2c49ed65 full 2c49ed6539422e95887d5153f4ba0322f54babf5422f0229862454b185577c0b
PASS dispatch step 2c49ed65
TAG dispense 676b1a86 full 676b1a86d8f4f6c94878984678a28c70e0fe7083f7c32916fe8793ef1f043948
PASS dispatch dispense 676b1a86
TAG transfer 79c71c23 full 79c71c23a968375dc378200e68ea3d8345690f8563a1861b448d0c6a511f6d2b
TAG transfer_delegator fd3ef14a full fd3ef14a1be2dd567c7feac6e5748e943cfcefc83105beed16aff39656ed7d8c
UNKEYED pk32 f9f2a0b353f482f415281da3a00929d08a7d9a6498054f5ef6623b5580e607f7
UNKEYED pk33 1a15d6547364ad963c3b840e885639bb8136a4de757c0e7cf63f5de2f1cfbdbe
KEYED pk32 PublicKeyHash 91438cfb14e4fbb78c740ab72162162f203eafae88940707d43ce7e97268d582
KEYED pk33 PublicKeyHash 4ba1a5f9924f181d804cd6210a5492c3a539c4de0559657519ee5bd9502bef3f
BLAKE2B R=51 ce57216285125006ec18197bd8184221cefa559bb0798410d99a5bba5b07cd1d
PASS blake2b R=51
PASS template 0 e572dff82304700b856a555ac3a4558d0df3646a3727816500270a93c66aac1e
PASS template 1 405e183e2494cdbe2df89349cc0ffa5b77fb885ad97a1d5660ecd0692ef8142a
PASS template 2 6616a66757315de0221cb2acba729113cebde31f8d3ca7fa93878a0584b96905
WRONG prefix||suffix 61||6263 6437b3ac38465133ffb63b75273a8db548c558465d79db03fd359c6cd5bd9d85
PASS p2pk value is key
PASS p2pk-schnorr arg
PASS p2pk-schnorr state
PASS p2pkh-schnorr unkeyed f9f2a0b353f482f415281da3a00929d08a7d9a6498054f5ef6623b5580e607f7
PASS p2pkh-schnorr arg
PASS p2pkh-schnorr state
PASS p2pkh-ecdsa unkeyed 1a15d6547364ad963c3b840e885639bb8136a4de757c0e7cf63f5de2f1cfbdbe
PASS p2pkh-ecdsa arg
PASS p2pkh-ecdsa state
PASS p2sh blake2b ce57216285125006ec18197bd8184221cefa559bb0798410d99a5bba5b07cd1d
PASS p2sh spk aa20ce57216285125006ec18197bd8184221cefa559bb0798410d99a5bba5b07cd1d87
PASS p2sh arg
PASS p2sh state
PASS covenant-id arg
PASS covenant-id state
approval_checks 20
signature_oracle_cases 11
FAILS 0
```

A second one-shot confirmed two digests that appear only on unmerged pull [#31](https://github.com/kaspanet/kccs/pull/31), not on `main`:

```text
p31a 7caa514a05535fd97887e483ce6f1fc36ef7026435c47521b04549d9af4837bf
p31b ed887ad164d313eeeac970912504a81156274732ab09c0c0559ff59160abddf9
```

`p31a` is unkeyed BLAKE3 of 32 bytes `0x22`. `p31b` is unkeyed BLAKE3 of `0x02 || 0x55^32`. They match the pull's examples. Keyed `PublicKeyHash` of the KCC-2 sample keys does not match the unkeyed samples printed above.

## What passed

- Every `hash_function` row in `kcc-0001/vectors/conformance.json` (unkeyed empty, unkeyed `KCC-1`, keyed empty).
- The two dispatch tags the KCC-1 prose publishes (`2c49ed65`, `676b1a86`).
- Three template hashes from the prose table, including empty/empty and `00ff`/`100080`.
- All five KCC-2 constructions: raw key, unkeyed P2PKH, BLAKE2b P2SH, covenant id copied through, and `20 || value` for both argument and state encodings.
- The version-0 P2SH script `aa20 || blake2b || 87`.

## What the pass does not mean

- `approval_checks` were counted. They were not executed. Eleven of the twenty contexts supply `signature_valid` as a boolean. The file does not contain signature bytes to check.
- The KCC-1 JSON has more dispatch and encoding rows than this checker walks. The hash rows, the two published tags, the P2SH envelope, and the template rows above were compared. A full structural diff of every JSON field against every markdown table was not a second independent program.
- `transfer` tag `79c71c23` and `transfer_delegator` tag `fd3ef14a` are the KCC-1 preimage of the KCC-20 state-record types. `kcc-0020.md` does not print them. There is no KCC-20 expected value to match. See AUDIT LC-3.
- KCC-20 has no `kcc-0020/vectors/` directory. Nothing from that convention was run.
- The repo ships JSON and no runner. "Cannot be run" is not quite right for KCC-1 and KCC-2: the hashes can be recomputed, and they matched. It is right for KCC-20, and it is right for the signature oracles.

## What could not be run

- Argent `kcc20-reference` tests. `master` is the stub `76648f9938c474a5210f4b3b59b2e1b9ebae420f`. The implementation is unmerged pull #1 head `5b2a23124ef43730eca4f69248bc2866daf2c24c`. This audit did not check out that head and did not run `cargo test`.
- No TN10 transaction. The vectors that exist are hashes and boolean oracles. They do not need a node.
