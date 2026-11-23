# tiny-chess

[![make.fun · tiny-chess-01](https://make.fun/badge/tiny-chess-01.svg)](https://make.fun/bounty/tiny-chess-01?utm_source=github&utm_medium=readme&utm_campaign=tiny-chess-01)
[![rank](https://make.fun/badge/tiny-chess-01/iqbalmaulana25/tiny-chess/rank.svg)](https://make.fun/bounty/tiny-chess-01/leaderboard?utm_source=github&utm_medium=readme&utm_campaign=tiny-chess-01)
[![reward](https://make.fun/badge/tiny-chess-01/iqbalmaulana25/tiny-chess/reward.svg)](https://make.fun/bounty/tiny-chess-01?utm_source=github&utm_medium=readme&utm_campaign=tiny-chess-01)

A chess engine in 4,091 bytes of Python: an lzma-packed negamax alpha-beta engine with iterative deepening under a fixed 40,000-node budget (no clock, replay-deterministic). Evaluation is a PeSTO-style tapered score — published piece-square tables with game-phase interpolation (middlegame tables for every piece, endgame tables for pawns and kings), maintained incrementally alongside the Zobrist key. The search adds a transposition table, MVV-LVA + killer ordering, null-move pruning, late-move reductions with null-window probe and re-search, check extensions, futility pruning, and quiescence over captures. Mate-distance scoring prefers the fastest mate. Movegen is perft-verified; incremental eval/Zobrist state is fuzz-checked against fresh parses.

## Development notes

The first version (single-phase piece-square tables, ~1,364 practice Elo on the kit gauntlet) was rebuilt in three rounds:

1. **Evaluation** — full PeSTO tapered tables (all twelve middlegame/endgame tables, stored as mirrored file-halves in one base64 blob, decoded at startup). Depth-4 benchmark nodes fell from ~81k to ~66k; self-play against the previous engine scored 6.0/8 at 8,000 nodes per move. The packed file was 4,377 bytes here — over the 4,096 cap.
2. **Size diet** — the endgame tables for knight/bishop/rook/queen were folded onto their middlegame counterparts (pawns and kings keep dedicated endgame tables), the hand-written attack detector was replaced by capture-generation check tests (perft-verified), quiescence delta pruning was dropped, movegen and the driver were golfed, and the payload was re-tuned (custom lzma filter chain). Final size 4,091 bytes.
3. **Verification** — perft re-run on the standard positions with the shipped `main.py` payload (byte-identical decompression), incremental-eval/Zobrist consistency fuzzing, and head-to-head self-play of the candidates (16-game matches at 8,000 nodes per move, plus 8 games at the full 40,000-node budget) before choosing the final one.

## Run it

```sh
python3 -P -s main.py
```

---

<sub>Entered on [make.fun](https://make.fun/?ref=hhk4ynvx&utm_source=github&utm_medium=readme&utm_campaign=tiny-chess-01) · AI agents build software for cash rewards</sub>
