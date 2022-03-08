## Tournament Winner

### Description

There's an algorithms tournament taking place in which teams of programmers compete against each other to solve algorithmic problems as fast as possible. Teams compete in a round robin, where each team faces off against all other teams. Only two teams compete against each other at a time, and for each competition, one team is designated the home team, while the other team is the away team. In each competition there's always one winner and one loser; there are no ties. A team receives 3 points if it wins and 0 points if it loses. The winner of the tournament is the team that receives the most amount of points.

Given an array of pairs representing the teams that have competed against each other and an array containing the results of each competition, write a function that returns the winner of the tournament. The input arrays are named `competitions` and `results`, respectively. The `competitions` array has elements in the form of `[homeTeam, awayTeam]`, where each team is a string of at most 30 characters representing the name of the team. The `results` array contains information about the winner of each corresponding competition in the `competitions` array. Specifically, `results[i]` denotes the winner of `competitions[i]`, where a `1` in the `results` array means that the home team in the corresponding competition won and a `0` means that the away team won.

It's guaranteed that exactly one team will win the tournament and that each team will compete against all other teams exactly once. It's also guaranteed that the tournament will always have at least two teams.

### Sample Input

```
competitions = [
  ["HTML", "C#"],
  ["C#", "Python"],
  ["Python", "HTML"],
]
results = [0, 0, 1]
```

### Sample Output

```
"Python"
// C# beats HTML, Python Beats C#, and Python Beats HTML.
// HTML - 0 points
// C# -  3 points
// Python -  6 points
```

## Solution

Time and space complexity:

- time **O(n)**
- space **O(k)**
  where n is the number of competitions and k is the number of teams.

```rust
use std::collections::HashMap;

pub struct Solution;

impl Solution {
    pub fn tournament_winner(competitions: Vec<Vec<String>>, results: Vec<i32>) -> String {
        const HOME_TEAM_WON: i32 = 1;
        let mut current_best_team = String::new();
        let mut scores = HashMap::new();

        for (i, _) in results.iter().enumerate() {
            let home_team = &competitions[i][0];
            let away_team = &competitions[i][1];
            let mut winning_team = String::from(home_team);

            if results[i] == HOME_TEAM_WON {
                match scores.get(home_team) {
                    Some(value) => {
                        scores.insert(home_team, value + 1);
                    }
                    None => {
                        scores.insert(home_team, 1);
                    }
                }
            } else {
                match scores.get(away_team) {
                    Some(value) => {
                        scores.insert(away_team, value + 1);
                    }
                    None => {
                        scores.insert(away_team, 1);
                    }
                }

                winning_team = String::from(away_team);
            }

            match scores.get(&current_best_team) {
                Some(value) => {
                    if scores[&winning_team] > *value {
                        current_best_team = String::from(winning_team);
                    }
                }
                None => {
                    current_best_team = String::from(winning_team);
                }
            }
        }

        return current_best_team;
    }
}

fn main() {
    assert_eq!(
        Solution::tournament_winner(
            vec![
                vec![String::from("HTML"), String::from("C#")],
                vec![String::from("C#"), String::from("Python")],
                vec![String::from("Python"), String::from("HTML")]
            ],
            vec![0, 0, 1]
        ),
        "Python"
    );
    assert_eq!(
        Solution::tournament_winner(
            vec![
                vec![String::from("Bulls"), String::from("Eagles")],
                vec![String::from("Bulls"), String::from("Bears")],
                vec![String::from("Bulls"), String::from("Monkeys")],
                vec![String::from("Eagles"), String::from("Bears")],
                vec![String::from("Eagles"), String::from("Monkeys")],
                vec![String::from("Bears"), String::from("Monkeys")],
            ],
            vec![1, 1, 1, 1, 1, 1]
        ),
        "Bulls"
    );
}
```
