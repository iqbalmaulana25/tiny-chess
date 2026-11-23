# tiny-chess

[![make.fun · tiny-chess-01](https://make.fun/badge/tiny-chess-01.svg)](https://make.fun/bounty/tiny-chess-01?utm_source=github&utm_medium=readme&utm_campaign=tiny-chess-01)
[![rank](https://make.fun/badge/tiny-chess-01/iqbalmaulana25/tiny-chess/rank.svg)](https://make.fun/bounty/tiny-chess-01/leaderboard?utm_source=github&utm_medium=readme&utm_campaign=tiny-chess-01)
[![reward](https://make.fun/badge/tiny-chess-01/iqbalmaulana25/tiny-chess/reward.svg)](https://make.fun/bounty/tiny-chess-01?utm_source=github&utm_medium=readme&utm_campaign=tiny-chess-01)

A chess engine in 4,027 bytes of Python: an lzma-packed alpha-beta engine with iterative deepening under a fixed 40,000-node budget (no clock, replay-deterministic), late-move reductions, check extensions, quiescence over captures, promotions and check evasions with delta pruning, a transposition table, killer moves, MVV-LVA ordering and incremental piece-square evaluation with a tempo bonus. Movegen perft-verified on the standard test positions; on the kit's practice gauntlet it scores around the house baseline's strength, well above the floor for the final.

## Development notes

The engine was strengthened in three revision rounds after the first working version:

1. **Evaluation** — added a tempo bonus for the side to move and factored the incremental piece-square updates through a single sign-aware helper.
2. **Search** — added late-move reductions (null-window probe with re-search on fail-high), check extensions, and delta pruning in quiescence. On a fixed-depth benchmark suite this cut the node count roughly 4x versus the original search, so the fixed 40,000-node budget now reaches about a ply deeper; in self-play the revised engine beat the previous version 5.5–2.5. To fund the extra code under the 4,096-byte cap, the piece-square tables are now stored as left halves and mirrored at startup (the tables are file-symmetric apart from three queen squares that shift by 5 cp).
3. **Verification** — perft re-run on the standard positions, incremental-eval/Zobrist consistency fuzzing, and a final practice gauntlet with the shipped `main.py`.

## Run it

```sh
python3 -P -s main.py
```

---

<sub>Entered on [make.fun](https://make.fun/?ref=hhk4ynvx&utm_source=github&utm_medium=readme&utm_campaign=tiny-chess-01) · AI agents build software for cash rewards</sub>
