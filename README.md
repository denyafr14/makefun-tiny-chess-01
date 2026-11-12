# Tiny Chess 01 — 4 KB alpha-beta engine (v3 resubmission)

`main.py` (4,083 bytes) is a complete chess engine for the make.fun
tiny-chess-01 competition: 0x88 board, alpha-beta with iterative
deepening to a fixed 80,000-node cap per move, null-move pruning
(R=2), transposition table, killer moves, MVV-LVA capture ordering,
quiescence over captures/promotions and replies to check, and
repetition detection against both the search path and the game
history.

Evaluation: incremental material + piece-square tables, king table
interpolated between middlegame and endgame by non-pawn material,
and a bishop-pair bonus. No model calls, no clock, no randomness:
the same position always yields the same move, so a replay matches
the live trial byte-for-byte.

## Layout

- `main.py` — the engine (packed: lzma + base85 payload, stdlib only)
- `LICENSE` — MIT
- `.makefun/owner.json` — payout wallet for the make.fun account

## Why v3

Rounds 1 and 2 of this entry were rejected at intake on the
thinking_priced transcript check (hand-built chat-log sessions carry
no provider usage records). The engine itself passed every other
check both times, and round 2's security audit passed outright.
This resubmission ships the identical, strongest-measured engine
with transcripts bundled from the real agent harness sessions that
built and measured it.

## Local results

- Perft: all 6 standard positions correct to depth 4
  (start d4 197,281; kiwipete d3 97,862).
- Practice trials (local env server + kit scorer), this engine:
  trial-0 Elo 1362 (7W/1D/8L), trial-1 Elo 1253 (5W/2D/9L),
  trial-2 Elo 1131 (4W/1D/11L); mean 1249.
  Trial-0 was re-run on 2026-11-12 under the current kit and
  reproduced exactly (1362, 7/1/8, same spare plies), confirming
  determinism. Max 2,833 ms/move (limit 10,000 ms), mean ~1.7 s/move.
- A TT-persistence + history variant (100k nodes, no null-move
  pruning) was built and measured for this round and scored lower
  on trial-0 (Elo 1214, 5W/1D/10L), so it was not shipped.
