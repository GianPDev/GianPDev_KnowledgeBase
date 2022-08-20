---
tags: [rust, programming, dev, debug, c, c++, gdb]
---
### Install gdb for rust
```bash
sudo yum install rust-gdb
```

### Run gdb on rust executable
```bash
rust-gdb PROJECTNAME/target/debug/PROJECTNAME --tui
```

### Quick Commands
```bash
start #Starts program and starts and stops line by line
kill #Stops the program
run #starts the program normally

n #(next)goes to next line
ni #(nexti)goes forward 1 instruction
s #(step)steps into functions/go to next line
si #(stepi)steps one instruction
fin #(Finish)aka step out, continue running until function returns + prints output

```

### Debugging TUI apps
*note it doesn't show background (maybe more stuff), but dialogue box seems to work*
```bash
cargo install ugdb
```
```bash
ugdb --gdb=rust-gdb PROJECTNAME/target/debug/PROJECTNAMEEXECUTABLE
```
in (gdb) reloads file (for after recompiling):
```bash
!reload
```
### ugdb hotkeys
`ESC` to go into mode select (borders/lines will go yellow)
	`i` to go to gdb input
	`s` to go to source code
	`e` to enter a gdb expression (not sure what this is)
	`t` to go into terminal
	`T` to go into locked mode terminal, requires 2x `ESC` pressed to exit
