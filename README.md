# Tiny Chess Engine

A chess engine in 4,068 bytes of Python for make.fun's tiny-chess-01
bounty. main.py holds an lzma-packed alpha-beta engine: iterative
deepening under a fixed 40,000-node budget (no clock, deterministic),
quiescence over captures, promotions and check evasions, a transposition
table, killer moves, MVV-LVA ordering and incremental piece-square
evaluation. It plays the house gauntlet through the env at
MAKEFUN_ENV_URL. MIT licensed.
