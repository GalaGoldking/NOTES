# Base Usage

```
awk 'command {to execute}' [FILE]
```

# Variables

```
awk '{[variable name] = }'
```

## Printing a created variable

```
awk '{variable = $1} END {print variable}
```

## Passing a shell variable

```
val=root

awk -v user="$val" -F: '$1==user {print $0}' /etc/passwd
```

Output:

```
root:x:0:0:root:/root:/usr/bin/zsh
```

## Built-in Variables

`NR` - Current line number

`NF` - Number of fields in the line

```
echo "one two three" | awk '{print NF, $NF}'
```

Output is 3 

```
awk -F: '{print NR, NF, $0}' /etc/passwd
```

Output:

```
1 7 root:x:0:0:root:/root:/usr/bin/zsh
2 7 daemon:x:1:1:daemon:/usr/sbin:/usr/sbin/nologin
3 7 bin:x:2:2:bin:/bin:/usr/sbin/nologin
4 7 sys:x:3:3:sys:/dev:/usr/sbin/nologin
5 7 sync:x:4:65534:sync:/bin:/bin/sync
6 7 games:x:5:60:games:/usr/games:/usr/sbin/nologin
7 7 man:x:6:12:man:/var/cache/man:/usr/sbin/nologin
8 7 lp:x:7:7:lp:/var/spool/lpd:/usr/sbin/nologin
9 7 mail:x:8:8:mail:/var/mail:/usr/sbin/nologin
```

`FNR` - File Number of Records (line number per file)

```
awk '{print FNR, NR, $0}' [FILE1] [FILE2]
```

First file starts FNR=1, NR=1; second file starts FNR=1, NR=last+1

`FS` - Input Field

- Controls how awk splits a line into fields
- Default = whitespace (spaces or tabs)

```
awk 'BEGIN{FS=":"} {print $1, $3}' /etc/passwd
```

Equivalent to 

```
awk -F: {print $1, $3} /ets/passwd
```

`OFS` - Output Field Seperator

- Controls how fields are joined when you use `,` in `print`
- Default = single space

```
echo "a:b:c" | awk 'BEGIN{FS=":"; OFS="--"} {print $1, $2, $3}'
```

Output:

```
a--b--c
```

`RS` - Record Seperator

`ORS` - Output Record Seperator

Default = newline

All outputs separated by ; instead of newline.

```
awk 'BEGIN{ORS=";"} {print $1}' file.txt
```

```
echo -e "line1\nline2\nline3" | awk 'BEGIN{RS="\n"; ORS=";"} {print $0}'
```

Output: line1;line2;line3;

`ARGV` and `ARGC` Command line args

- ARGV - number of arguments
- ARGC - array of arguments

`FILENAME` - Current File Name

```
awk '{print FILENAME, NR, $0}' /etc/passwd
```

Output:

```
/etc/passwd 1 root:x:0:0:root:/root:/usr/bin/zsh
/etc/passwd 2 daemon:x:1:1:daemon:/usr/sbin:/usr/sbin/nologin
/etc/passwd 3 bin:x:2:2:bin:/bin:/usr/sbin/nologin
/etc/passwd 4 sys:x:3:3:sys:/dev:/usr/sbin/nologin
/etc/passwd 5 sync:x:4:65534:sync:/bin:/bin/sync
/etc/passwd 6 games:x:5:60:games:/usr/games:/usr/sbin/nologin
/etc/passwd 7 man:x:6:12:man:/var/cache/man:/usr/sbin/nologin
```

`ENVIRON` - Environment Variables

```
awk 'BEGIN{print ENVIRON["ENV VARIABLE"]}'
```

`IGNORECASE` - Case Sensitive Matching

```
echo "HELLO" | awk 'BEGIN{IGNORECASE=1} /hello/{print "Matched!"}'
```

`CONVFMT` - Conversion Format for numbers

Default = "%.6g"

```
awk 'BEGIN{x=1234567; CONVFMT="%.2f"; print x}'
```

Output: 1234567.00

`OFMT` - Output Format for numbers

```
awk 'BEGIN{OFMT="%.3f"; print 10/3}'
```

Output 3.333

`RLENGTH` and `RSTART` - Regex match info

After using `match()` these variables hold info.

```
echo "abcdef" | awk '{if (match($0,"cd")) print RSTART, RLENGTH}'
```

Output: 3 2

match starts at pos 3, length 2

# Conditions

```
awk '[condition] {print $0}' [FILE]
```

```
awk -F: '$1=="root" {print $1,$3}' /etc/passwd
```

```
awk '{ if ($3 > 1000) print $1, $3 }' /etc/passwd 
```


## if/else form

```
awk '{ if ($3 < 1000) print $1 " → system user"; else print $1 " → normal user" }' /etc/passwd
```

## Multiple conditions

```
awk '{
    if ($3 == 0)
        print $1, "is root";
    else if ($3 < 1000)
        print $1, "is system";
    else
        print $1, "is regular";
}' /etc/passwd
```

## Ternary operator

```
awk '{print $1, ($3 < 1000 ? "system" : "normal")}' /etc/passwd
```

## Pattern VS Condition

```
awk '$3 > 1000 {print $1}' /etc/passwd
```

Equivalent to 

```
awk '{if ($3 > 1000) print $1}' /etc/passwd
```

## next

```
awk '{ if ($3 < 1000) next; print $1, $3 }' /etc/passwd
```

next = skip the rest of the rules for current line.

# Printing column

```
awk '{print $1}'
```

`$1 - number of a column to print`

`$0 - to print everything`

## Printing multiple columns

```
awk '{print $1, $3}'
```

# Split

```
awk -F[seperate by] '{print $1, $3}'
```

```
awk -F: '{print $1,$3}' /etc/passwd
```

Seperate /etc/passwd by ":" character

# Patter Matching

```
awk '/[PATTERN]/ {print $0} [FILE]
```

# BEGIN and END blocks

Useful for formatting beginning text and ending text

```
awk 'BEGIN {print "["TEXT FOR BEGINNING]"} {print $1, $3} END {print "TEXT FOR ENDING"}' [FILE]
```

Can be used seperately

```
awk '{print $0}' END {print "TEXT FOR ENDING"}
```

# Calculations

```
echo "10\n20\n30" | awk '{sum += $1} END {print "Total Sum = " sum}'
```

# Strings

## Convert to lowercase

```
echo "HELLO WORLD" | awk '{print tolower($0)}'
```

## Convert to uppercase

```
echo "hello world" | awk '{print toupper($0)}'
```

# Execute commands using awk

```
awk '{system("echo " $1)}' [FILE]
```
