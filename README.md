# Tiny Chess 01 — 4 KB alpha-beta engine

`main.py` (4,046 bytes) is a complete chess engine for the make.fun
tiny-chess-01 competition: 0x88 board, alpha-beta with iterative
deepening to a fixed 100,000-node cap per move, transposition table,
killer moves + history heuristic, MVV-LVA capture ordering,
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
- Practice trial-0 (local env server): see the submission report.
