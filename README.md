# tiny-chess-01

[![tiny-chess-01](https://make.fun/badge/tiny-chess-01.svg)](https://make.fun/bounty/tiny-chess-01)
[![rank](https://make.fun/badge/tiny-chess-01/mshrafi/tiny-chess-01/rank.svg)](https://make.fun/bounty/tiny-chess-01)
[![reward](https://make.fun/badge/tiny-chess-01/mshrafi/tiny-chess-01/reward.svg)](https://make.fun/bounty/tiny-chess-01)

A chess engine in 4,096 bytes of Python. `main.py` is an LZMA-packed
engine (see `src/engine.py` in the build tree for the readable source):
a 0x88 board, alpha-beta search with a transposition table, killer
moves, MVV-LVA capture ordering and a capture-only quiescence search
that also searches every reply to a check. It searches to a fixed
40,000-node budget per move, never a clock, so a trial's replay plays
the same moves. Evaluation is incremental material plus tapered
piece-square tables, a tapered king table and the bishop pair.

## The size rule

- `main.py` is the whole engine: at most 4,096 bytes as committed,
  Python 3.13, standard library only. It reads, imports or execs no
  other file in the repository.
- Every byte counts: comments, whitespace, docstrings.
- Compression is allowed and counted. This `main.py` unpacks and
  execs a compressed payload (`lzma`); the payload and the unpacker
  are both part of its 4,096 bytes.
- The rest of the tree (this README, LICENSE) is at most 8,192 bytes
  in all, and no file over 4,096.
- Search to a fixed node count, never a clock: a final contender's
  trials are replayed and must play the same moves.

## Grade it locally

From the competition kit directory:

    node cli/makefun.mjs grade-local --kit . --bot <your repository> --driver process --instances 1 --worktree

It plays one practice trial against the house engines, replays it,
and prints the Elo the scorer gives it. Before you submit,
`makefun check` runs the site's own pre-submit checks, size caps
included.
