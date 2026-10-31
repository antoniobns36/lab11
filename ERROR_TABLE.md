# Error table

One row per failure. Fill in every column. You need at least eight rows.

| Scenario | Function that detects it | Error value | What the player sees |
|---|---|---|---|
| Fleet file does not exist | `load_fleet` | `Err(DataError::Io(..))` (kind `NotFound`) | _(example: your row goes here)_ |
| Target fleet file path is completely missing | `load_fleet` | `DataError::Io(ErrorKind::NotFound)` | `Error: could not load data/fleet.txt: No such file or directory` |
| Targeted fleet path points to directory instead of file | `load_fleet` | `DataError::Io(ErrorKind::IsADirectory)` | `Error: could not load data/: Is a directory` |
| Selected file contains structural comments only | `load_fleet` | `DataError::NoShips("data/fleet_empty.txt")` | `Error: could not load data/fleet_empty.txt: no valid ships found` |
| Entire payload document contains invalid rows | `load_fleet` | `DataError::NoShips("data/fleet_all_bad.txt")` | `Error: could not load data/fleet_all_bad.txt: no valid ships found` |
| Loaded custom layout only provides 9 layout rows | `parse_board` | `BoardError::WrongRowCount(9)` | `Practice board unavailable: Expected exactly 10 rows, but found 9.` |
| Layout schematic includes unrecognized tile characters | `parse_board` | `BoardError::BadChar { line: 6, ch: 'x' }` | `Practice board unavailable: line 6 contains an invalid character 'x'.` |
| Persistent scores ledger file is absent from disk | `load_scores` | Trapped internally (`io::ErrorKind::NotFound`) | `  no scores yet` |

Scenarios to cover (add more if you find them):

- fleet file missing
- a directory given as the fleet path
- fleet file with only comments
- fleet file where every line is bad
- board file with nine rows
- board file with a bad character
- scores file missing
- scores file that cannot be written
- `K11` typed at the prompt
