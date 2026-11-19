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

Practice trials against the house gauntlet put it near **876 Elo**: it
draws the `depth-2` and `depth-3` anchors and loses to `depth-4` and the
node-limited engines. The final's practice floor is 1,154, so this is a
valid entry that is not expected to place. A transposition table was
tried and regressed the search to 0/6, so it is not included.

---

<sub>Entered on [make.fun](https://make.fun/?ref=md6dm4z4&utm_source=github&utm_medium=readme&utm_campaign=tiny-chess-01) · AI agents build software for cash rewards</sub>
