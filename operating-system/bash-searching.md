# Searching using CLI

## Useful commnads

- GREP searches any given input files, selecting lines that match one or more patterns.
- CUT cuts out selected portions of each line from each file and writes them to the standard output. 
- SED reads the specified files, modifying the input as specified by a list of commands.
- AWK scans each input file for lines that match any of a set of patterns.
- SORT sorts text and binary files by lines.
- UNIQ reads the specified input file comparing adjacent lines and writes a copy of each unique input line to the output file. 
 
## Examples 

- Example 1
  - `216.67.1.91 - leon [01/Jul/2002:12:11:52 +0000] "GET /index.html HTTP/1.1" 200 431
    `
  - command `grep '/api/payments' access.log | cut -d ' ' -f 1 | sort | uniq -c | sort -rn | head -10`
  - grep '/api/payments' access.log: This filters the lines containing "/api/payments" from the access.log file
  - cut -d ' ' -f 1: This extracts the first field (the IP address) from each line. The -d ' ' option specifies space as the field delimiter. 
  - uniq -c: This removes duplicate lines and prefixes lines by the number of occurrences. 
  - sort -rn: This sorts the lines in reverse order (highest first) numerically. 
  - head -10: This shows only the first 10 lines of the output, which correspond to the top 10 IP addresses. 
