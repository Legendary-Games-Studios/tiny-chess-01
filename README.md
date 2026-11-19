# tiny-chess-01 entry

`main.py` is a self-contained chess engine (2,993 bytes, Python 3.13,
standard library only) that plays every game through the env. It was
written for the tiny-chess-01 bounty and compressed from `src.py` with
the kit's own `makefun compress`, which the size rule explicitly allows.

## How it plays

- Negamax alpha-beta with principal variation search.
- Quiescence search over captures and promotions, so it does not
  horizon on a hanging piece.
- Material plus piece-square tables, with the king table swapped between
  middlegame and endgame by remaining material, and a small bonus for
  the bishop pair.
- Killer-move heuristic for ordering, plus cap-first ordering in
  quiescence. Mate scores are propagated as +/-30000; a king capture in
  search counts as mate.
- Fixed node cap (`CHESS_NODES`, default 150,000) with iterative
  deepening. It never looks at a clock, so a replayed trial plays the
  same moves byte for byte.
- If anything in the move path raises, it falls back to
  `legal_moves[0]` rather than forfeiting.

## Honest measurement

Practice trials against the house gauntlet put it around **876 Elo**:
it draws the `depth-2` and `depth-3` anchors and loses to `depth-4` and
the node-limited engines. The practice floor for the final is 1,154 and
the house baseline is roughly 1,325-1,365, so this is a valid entry that
is not expected to place. A transposition table was attempted and
regressed the search to 0/6, so it was left out.

## Size rule

`main.py` is at most 4,096 bytes as committed and reads, imports or
execs no other file in the repository. The rest of the tree (this README,
LICENSE, `.makefun/owner.json`) is at most 8,192 bytes in all.
