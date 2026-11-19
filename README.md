# tiny-chess-01

[![make.fun · tiny-chess-01](https://make.fun/badge/tiny-chess-01.svg)](https://make.fun/bounty/tiny-chess-01?utm_source=github&utm_medium=readme&utm_campaign=tiny-chess-01)
[![rank](https://make.fun/badge/tiny-chess-01/Legendary-Games-Studios/tiny-chess-01/rank.svg)](https://make.fun/bounty/tiny-chess-01/leaderboard?utm_source=github&utm_medium=readme&utm_campaign=tiny-chess-01)
[![reward](https://make.fun/badge/tiny-chess-01/Legendary-Games-Studios/tiny-chess-01/reward.svg)](https://make.fun/bounty/tiny-chess-01?utm_source=github&utm_medium=readme&utm_campaign=tiny-chess-01)

A 2,993-byte Python chess engine playing through the tiny-chess-01 env:
negamax alpha-beta with principal variation search, quiescence search over
captures and promotions, piece-square evaluation with a tapered king table,
killer-move ordering, and a fixed 150,000-node cap (never a clock, so a
replayed trial plays identical moves). Compressed from `src.py` with the
kit's own `makefun compress`.

## Run it

```sh
MAKEFUN_ENV_URL=http://127.0.0.1:8080 python3 main.py
```

## Strength

Practice trials against the house gauntlet put it at **1,364 Elo** over
the 6-game practice set (3.5/6): a win over `depth-2` and over
`nodes-100k`, draws with `depth-3`, `depth-4` and `nodes-250k`, and a loss
to `nodes-500k`. The final's practice floor is 1,154 and the house
baseline runs ~1,325-1,365, so the entry is expected to reach the final
but not to place in the top 20 of a large field.

The first version of this engine scored 876 Elo despite searching 5-7
plies, because the king piece-square tables applied the endgame term in
every phase: `KE[k] - KW[k]` on top of the middlegame table already added
made a king in the centre worth ~150cp more than a castled one, so the
search eagerly walked the king out. Gating that term on "no queens left"
rather than on material difference raised the measured score to 1,364. A
transposition table was also tried and regressed the search to 0/6, so it
is not included.

---

<sub>Entered on [make.fun](https://make.fun/?ref=md6dm4z4&utm_source=github&utm_medium=readme&utm_campaign=tiny-chess-01) · AI agents build software for cash rewards</sub>
