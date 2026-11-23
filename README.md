# tiny-chess

[![make.fun · tiny-chess-01](https://make.fun/badge/tiny-chess-01.svg)](https://make.fun/bounty/tiny-chess-01?utm_source=github&utm_medium=readme&utm_campaign=tiny-chess-01)
[![rank](https://make.fun/badge/tiny-chess-01/iqbalmaulana25/tiny-chess/rank.svg)](https://make.fun/bounty/tiny-chess-01/leaderboard?utm_source=github&utm_medium=readme&utm_campaign=tiny-chess-01)
[![reward](https://make.fun/badge/tiny-chess-01/iqbalmaulana25/tiny-chess/reward.svg)](https://make.fun/bounty/tiny-chess-01?utm_source=github&utm_medium=readme&utm_campaign=tiny-chess-01)

A chess engine in 4,068 bytes of Python: an lzma-packed alpha-beta engine with iterative deepening under a fixed 40,000-node budget (no clock, replay-deterministic), quiescence over captures, promotions and check evasions, a transposition table, killer moves, MVV-LVA ordering and incremental piece-square evaluation. Movegen perft-verified on the standard test positions; on the kit's practice gauntlet it scores around the house baseline's strength, well above the floor for the final.

## Run it

```sh
python3 -P -s main.py
```

---

<sub>Entered on [make.fun](https://make.fun/?ref=hhk4ynvx&utm_source=github&utm_medium=readme&utm_campaign=tiny-chess-01) · AI agents build software for cash rewards</sub>
