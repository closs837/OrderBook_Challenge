# Order book

Price–time limit order books, one per trading symbol: the program consumes a CSV of new
orders, cancellations and flushes, and publishes top-of-book changes (best bid and best
ask) for every book it touches.

```
cargo build
cargo run input_csv.csv
cargo test -- --show-output
```

`cargo test -- --show-output` runs the exercise's scenarios; `input_csv.csv` is a small
sample feed to run against.

## Layout

| Path | Purpose |
| --- | --- |
| `src/csv_parse.rs` | CSV parsing |
| `src/process_order.rs` | New order, cancel and flush handling |
| `src/lib.rs` | Book structures and top-of-book output |

`serde` is vendored under `serde/` so the exercise builds without network access.

## Open items

Written as an exercise, and the bonus challenges were left out on purpose (trade
execution, scenarios 13 and 14, containerising the program). The two things I would pick
up next:

- reuse the read buffer instead of allocating a fresh `String` per CSV line
  (`src/csv_parse.rs`);
- replace the linear scan used for cancellations with a binary search
  (`src/process_order.rs`), and move the per-symbol books onto threads.

<details>
<summary>Original exercise brief</summary>

Produce a program which maintains price-time limit order books, one per trading symbol.
The program should accept new orders, order cancellations, and flushes from a CSV file and
publish top of book (best bid and ask) changes for each order book. Supporting trades or
matching is optional.

Bonus challenges not solved in this solution: trade orders, scenarios 13 and 14, extra
scenarios, containerising the program.

</details>
