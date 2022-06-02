---
tags: [ssh, mosh, sysadmin, bash, powershell, edit, script, scripting, sed, terminal, editing, pipe, search, replace]
---

#### Using Sed to modify files and pipe
```bash
# search and replace without -i it just outputs to console
sed 's/{SEARCH}/{REPLACE}/' FILENAME
# search and replace all matches in file
sed 's/{SEARCH}/{REPLACE}/g' FILENAME
# search and replace but can use escaped characters
sed 's;{SEARCH};{REPLACE};' FILENAME
# outputs file with LINENUMBER deleted
sed '{LINENUMBER}d' FILENAME
# ouputs line to be deleted
sed '{LINENUMBER}!d' FILENAME
# searches string then deletes the string
sed '/{STRING}/d' FILENAME
# searches string then returns only selected strings (opposite of delete)
sed '/{STRING}/!d' FILENAME
# adds string to line
sed '{LINENUMBER}a\{VALUE SPACES ESCAPED}' FILENAME
# saves output to file
sed -i {COMMANDS}
# saves .bak file of previous contents then saves file
sed -i.bak {COMMANDS}
# does not show output
sed -n {COMMANDS}
# piping sed (-E)
echo "test,ts2,t3" | sed -E 's/,/\n/g'
```