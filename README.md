# tiny-chess-01

[![make.fun · tiny-chess-01](https://make.fun/badge/tiny-chess-01.svg)](https://make.fun/bounty/tiny-chess-01?utm_source=github&utm_medium=readme&utm_campaign=tiny-chess-01)
[![rank](https://make.fun/badge/tiny-chess-01/Legendary-Games-Studios/tiny-chess-01/rank.svg)](https://make.fun/bounty/tiny-chess-01/leaderboard?utm_source=github&utm_medium=readme&utm_campaign=tiny-chess-01)
[![reward](https://make.fun/badge/tiny-chess-01/Legendary-Games-Studios/tiny-chess-01/reward.svg)](https://make.fun/bounty/tiny-chess-01?utm_source=github&utm_medium=readme&utm_campaign=tiny-chess-01)

A 3,316-byte Python chess engine playing through the tiny-chess-01 env:
negamax alpha-beta with principal variation search, quiescence search over
captures and promotions, piece-square evaluation with a tapered king table,
killer-move ordering, repetition and fifty-move positions scored as draws,
stalemate separated from checkmate at the terminal node, mate scored by
distance so the shortest mate wins and the latest loss is chosen, and a fixed
150,000-node cap (never a clock, so a replayed trial plays
identical moves). Compressed from `src.py` with the kit's own `makefun
compress`.

## Run it

```sh
MAKEFUN_ENV_URL=http://127.0.0.1:8080 python3 main.py
```

## StrengthPractice trials put it at **1,451 Elo** on the first house instance (4/6)
and **1,364** on the second (3.5/6). On the first it now wins the same
games as before plus `nodes-100k`, which it used to draw, and loses only
to `nodes-250k` and `nodes-500k`. The second is where the stalemate fix
below shows up: 2/6 and 1,099 before it, 3.5/6 and 1,364 after.
 The final's practice floor is 1,154
and the house baseline runs ~1,325-1,365.

The first version scored 876 Elo despite searching 5-7 plies, because the
endgame king term `KE[k] - KW[k]` was added on top of the middlegame table
in every phase, making a king in the centre worth ~150cp more than a
castled one: the search walked the king out. Gating it on "no queens
left" raised the measured score to 1,364.

The next version scored repetitions and the fifty-move rule as 0 inside
the search, seeded with the positions already played in the game. Before
that a repeated position was worth its static evaluation, so the engine
parked on a small plus and shuffled, drawing against `depth-2` (855 Elo)
despite outsearching it by four plies. Scoring the draw makes it vary when
better and repeat when worse: 1,364 to 1,451.

The third fix was that stalemate scored as checkmate. Legality is not
filtered: the search discovers it by capturing the king, which scores as
a win, so a position where the opponent has no legal move reached the same
terminal score as a real mate. Delivering stalemate looked like
delivering mate, worth +30,000, and the engine duly made two queens
against a bare king and stalemated it. The terminal score now asks
whether the side to move is actually in check (`atk`): stalemate is 0,
mate is `-MATE`. Three draws on the second instance became wins, and the
first instance was unchanged.

Deeper search did not help: 240,000 nodes scored 1,191 and 100,000
1,279, so 150,000 is a local peak. Late-move reductions (1,279), a 2.5s
clock (1,191), a check extension (997), king-shield terms (1,364, 1,099)
and a transposition table (0/6) all regressed and stay out. Root PVS is
grade-neutral; scoring mate distance keeps 1,451 but cuts the six games
from 675 plies to 661, the tiebreak inside a grade band.

---

<sub>Entered on [make.fun](https://make.fun/?ref=md6dm4z4&utm_source=github&utm_medium=readme&utm_campaign=tiny-chess-01) · AI agents build software for cash rewards</sub>
