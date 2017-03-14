# Linux Bash notes

## Basic format

```bash
[pi@raspberrypi:~ ]$ command  [-options]  parameter1  parameter2 ...                      指令     選項        參數(1)     參數(2)
```

Command and parameters are separated by whitespace.

`-h` shorthand version

`--help` longhand version

`#` root user prompting symbol

`$` other users prompting symbol

`~` home directory of the current user
e.g. `/root` for root user `/home/cyrus` for the above user

---
## `<Tab>` key usage:

Single Press `<Tab>` = auto complete command / options / file name

Double Press `<Tab>` = prompt / list the possible combination

Double pressing can be used on command [-options]:
```bash
pi@raspberrypi:~ $ date --
--date        --help        --reference=  --rfc-3339=   --universal   
--date=       --iso-8601    --rfc-2822    --set=        --version   
```

---
## Check manual page
e.g. `man bc`

|Example|Description|
|---|---|
|`/word`| Look down for the `word`|
|`?word`|Look up for the `word`|
|`n, N`|Next, Previous search result|  
