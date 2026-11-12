# clone-lin-maker-jug-drip

Experimental LIN clone of MakerDAO / Sky `Jug.drip` (i64-positive scale: `RAY'=1e9` not `RAY=1e27`, 128-bit half-up `rpow` and floor `rmul`, fail-closed if the quotient does not fit i64).

- **Upstream:** [makerdao/dss](https://github.com/makerdao/dss) `src/jug.sol` commit `fa4f6630afb0624d04a003e920b0d71a00331d98` (AGPL-3.0-or-later). This repository does **not** vendor the Solidity source. Hashes only: sha256 `cefc440545885a916920ce2dc251916f2fc218701ba32413d3ce4884fba07927`, git blob `dae9b263f699ed917e1d0a16bb51dc8b0326764f`.
- **LIN kernel:** [`src/lin_maker_jug_drip.lin`](src/lin_maker_jug_drip.lin) (sha256 `557ce7eb8ba7e33f50d34375101b9fb370cea33a1cc9e9c0937dc3c2a5665975`, identical to lin-open)
- **C11 oracle copy:** [`test/oracles/maker_jug_drip_c11.c`](test/oracles/maker_jug_drip_c11.c)
- **Proofs (lin-open only):** [kbelludoo/lin-open](https://github.com/kbelludoo/lin-open) `examples/maker_jug_drip/` and `python3 test/prove_maker_jug_drip_external.py` (24 PASS / 0 FAIL / 1 SKIP JIT this run)
- **Class:** EXPERIMENTAL. Not Ethereum Maker vat.ilks.rate uint256. Not RAY=1e27. Not a production stability-fee replacement.

Named goldens (`RAY'=1e9`, `duty=RAY'+1e6`, `prev=RAY'`): identity duty leaves prev unchanged (**1000000000**); `now < rho` fail-closed **0**; dt=2 drip **1002001000** vs first-order linear **1002000000**; dt=10 drip **1010045120** vs linear **1010000000**; fold delta dt=2 **2001000**; naive i64 `7e18*3e18` wraps to **-5389669316318724096**.
