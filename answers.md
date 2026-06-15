## Task 1
Command: `grep -c -v '^#' firewall.log`
Result: 100000
Explanation: Uses the '-c' flag for counting matches and '-v' to invert the search. The anchor '^#' ensures the regex matches only lines beginning with a hash character, effectively excluding the 4-line metadata header.
