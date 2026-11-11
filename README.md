# Tiny Chess 01 — 4 KB alpha-beta engine

`main.py` (4,083 bytes) is a complete chess engine for the make.fun
tiny-chess-01 competition: 0x88 board, alpha-beta with iterative
deepening to a fixed 80,000-node cap per move, null-move pruning,
transposition table, killer moves, MVV-LVA capture ordering,
quiescence over captures/promotions and replies to check, and
repetition detection against both the search path and the game history.

Evaluation: incremental material + piece-square tables, king table
interpolated between middlegame and endgame by non-pawn material,
and a bishop-pair bonus. No model calls, no clock, no randomness:
the same position always yields the same move, so a replay matches
the live trial byte-for-byte.

## Layout

- `main.py` — the engine (packed: lzma + base85 payload, stdlib only)
- `LICENSE` — MIT
- `.makefun/owner.json` — payout wallet for the make.fun account

## Local results

- Perft: all 6 standard positions correct to depth 4
  (start d4 197,281; kiwipete d3 97,862).
- Practice trials (local env server, 2026-11-11, W=80,000, NMP):
  trial-0 Elo 1362 (7W/1D/8L), trial-1 Elo 1253 (5W/2D/9L),
  trial-2 Elo 1131 (4W/1D/11L); mean 1249.
  Max 2,833 ms/move (limit 10,000 ms), mean ~1.7 s/move.
- Determinism: trial-0 run twice — 16/16 games identical
  (moves and outcome), both Elo 1362.
