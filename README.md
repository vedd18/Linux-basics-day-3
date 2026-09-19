# Linux Basics – Day 3

This practical is about learning basic Linux commands for:

* Viewing files
* Searching text
* Counting lines
* Extracting columns
* Sorting data
* Using `grep`
* Using `cut`
* Using `awk`
* Using pipes `|`
* Redirecting output using `>`
* Using `sudo`

---

# General Instructions

1. Perform the tasks in order.
2. Read the complete task before starting.
3. Take screenshots only where requested.
4. Make sure important commands are visible in screenshots.
5. Do not include passwords, private keys, or other sensitive information in screenshots.
6. Stop/terminate AWS resources when instructed to avoid unnecessary charges.
7. Submit the GitHub repository in the submission form.

---

# Practical Tasks

## Q1. Display the first 5 lines of `/etc/group` and redirect the output to `/file2.txt`

### What do we need to do?

We need to:

1. Read the `/etc/group` file.
2. Take only the first 5 lines.
3. Save those lines into `/file2.txt`.

### Command

```bash
sudo sh -c "head -n 5 /etc/group > /file2.txt"
```

### Simple explanation

* `sudo` → runs the command with administrator permission.
* `sh -c` → tells the shell to execute the complete command.
* `head` → displays the beginning of a file.
* `-n 5` → display 5 lines.
* `/etc/group` → input file.
* `>` → redirects the output into a file.
* `/file2.txt` → destination file.

### Check the result

```bash
sudo cat /file2.txt
```

### What we learned

`head -n 5` is used when we need the first 5 lines of a file.

---

# Q2. Show the first 10 lines of `/root/anaconda-ks.cfg` and redirect the output to `/anaconda.txt`

### What do we need to do?

We need to take the first 10 lines from the file and save them in `/anaconda.txt`.

### Command

```bash
sudo sh -c "head -n 10 /root/anaconda-ks.cfg > /anaconda.txt"
```

### Explanation

* `head` → shows the beginning of the file.
* `-n 10` → takes 10 lines.
* `/root/anaconda-ks.cfg` → input file.
* `>` → saves the output.
* `/anaconda.txt` → output file.

### Check

```bash
sudo cat /anaconda.txt
```

### What we learned

`head -n 10` displays the first 10 lines.

---

# Q3. Display the first 32 lines of `/etc/passwd` and redirect to `/file3.txt`

### What do we need to do?

Take the first 32 lines from `/etc/passwd` and save them to `/file3.txt`.

### Command

```bash
sudo sh -c "head -n 32 /etc/passwd > /file3.txt"
```

### Check

```bash
sudo cat /file3.txt
```

### Verify number of lines

```bash
sudo wc -l /file3.txt
```

Expected:

```text
32 /file3.txt
```

### What we learned

`head -n 32` means **first 32 lines**.

---

# Q4. Save the last 10 lines of `/etc/shadow` to `/file4.txt`

### What do we need to do?

We need the last 10 lines instead of the first 10 lines.

For this, we use `tail`.

### Command

```bash
sudo sh -c "tail -n 10 /etc/shadow > /file4.txt"
```

### Explanation

* `tail` → displays the end of a file.
* `-n 10` → takes the last 10 lines.
* `/etc/shadow` → input file.
* `>` → saves the output.
* `/file4.txt` → output file.

### Check

```bash
sudo cat /file4.txt
```

### What we learned

`head` → beginning of file.

`tail` → end of file.

---

# Q5. Capture the first 15 lines of `/etc/passwd` and save them in `/file5.txt`

### Command

```bash
sudo sh -c "head -n 15 /etc/passwd > /file5.txt"
```

### Check

```bash
sudo cat /file5.txt
```

### Verify

```bash
sudo wc -l /file5.txt
```

### What we learned

We can change the number after `-n` depending on how many lines we need.

Examples:

```bash
head -n 5 file.txt
head -n 10 file.txt
head -n 15 file.txt
```

---

# Q6. Extract the first 100 characters from `/root/anaconda-ks.cfg`

### What do we need to do?

This question asks for **characters**, not lines.

Therefore, we use `-c`.

### Command

```bash
sudo sh -c "head -c 100 /root/anaconda-ks.cfg > /file6.txt"
```

### Explanation

* `head` → reads the beginning.
* `-c 100` → takes the first 100 characters.
* `>` → saves the result.
* `/file6.txt` → output file.

### Check

```bash
sudo cat /file6.txt
```

### Verify character count

```bash
sudo wc -c /file6.txt
```

Expected:

```text
100 /file6.txt
```

### What we learned

`-n` → lines.

`-c` → characters.

---

# Q7. Search for lines ending with `bash` in `/etc/passwd` and save the number of matching lines in `/bash.txt`

### What do we need to do?

We need to:

1. Search `/etc/passwd`.
2. Find lines ending with `bash`.
3. Count those lines.
4. Save the count in `/bash.txt`.

### Command

```bash
sudo sh -c "grep -c 'bash$' /etc/passwd > /bash.txt"
```

### Explanation

* `grep` → searches for text.
* `-c` → counts matching lines.
* `bash` → text we are searching for.
* `$` → means the **end of the line**.
* `/etc/passwd` → file to search.
* `>` → saves the result.

### Check

```bash
sudo cat /bash.txt
```

For example, if 2 lines match:

```text
2
```

### Important

```text
'bash'
```

means search for `bash`.

```text
'bash$'
```

means the line must **end with `bash`**.

### What we learned

`grep -c` counts matching lines.

---

# Q8. Find lines containing `nologin`, count them, and save the count in `/word.txt`

### What do we need to do?

We need to find lines where `nologin` appears anywhere in the line.

### Command

```bash
sudo sh -c "grep -c 'nologin' /etc/passwd > /word.txt"
```

### Explanation

* `grep` → searches.
* `-c` → counts matching lines.
* `nologin` → text to search.
* `/etc/passwd` → file to search.
* `>` → saves the count.
* `/word.txt` → output file.

### Check

```bash
sudo cat /word.txt
```

### Difference between Q7 and Q8

Q7:

```bash
grep -c 'bash$' /etc/passwd
```

`$` means `bash` must be at the **end**.

Q8:

```bash
grep -c 'nologin' /etc/passwd
```

No `$`, so `nologin` can appear **anywhere in the line**.

### What we learned

`grep "word"` → search anywhere.

`grep "word$"` → search at the end.

---

# Q9. Find `systemd` in `/etc/passwd` and `/etc/group`

### What do we need to do?

Search for `systemd` in **two files** and save the matching lines.

### Command

```bash
sudo sh -c "grep 'systemd' /etc/passwd /etc/group > /passgroup.txt"
```

### Explanation

```text
grep 'systemd'
```

→ search for `systemd`.

```text
/etc/passwd /etc/group
```

→ search in both files.

```text
>
```

→ save the result.

### Check

```bash
sudo cat /passgroup.txt
```

### What we learned

`grep` can search multiple files at the same time.

---

# Q10. Search for `root`, `rhel`, and `systemd` in `/etc/passwd`

### What do we need to do?

We need to search for **any one** of these three words:

* `root`
* `rhel`
* `systemd`

### Command

```bash
sudo sh -c "grep -E 'root|rhel|systemd' /etc/passwd > /search.txt"
```

### Explanation

* `grep` → search.
* `-E` → enables extended pattern matching.
* `|` → means **OR**.
* `/etc/passwd` → file to search.
* `>` → saves results.

So:

```text
root|rhel|systemd
```

means:

```text
root OR rhel OR systemd
```

### Check

```bash
sudo cat /search.txt
```

### Important

If `rhel` does not appear in your `/etc/passwd`, that is okay.

`grep` only shows words that actually exist in the file.

### What we learned

`grep -E` can be used with `|` to search for multiple patterns.

---

# Q11. Extract the 5th column from `/etc/passwd`

### What do we need to do?

The `/etc/passwd` file uses `:` to separate its columns.

Example:

```text
root:x:0:0:root:/root:/bin/bash
```

Columns:

```text
1 → root
2 → x
3 → 0
4 → 0
5 → root
6 → /root
7 → /bin/bash
```

We need column 5.

### Command

```bash
sudo sh -c "cut -d: -f5 /etc/passwd > /file1.txt"
```

### Explanation

* `cut` → extracts columns.
* `-d:` → tells `cut` that `:` is the delimiter.
* `-f5` → selects field/column 5.
* `/etc/passwd` → input file.
* `>` → saves the result.

### Check

```bash
sudo cat /file1.txt
```

### What we learned

For `/etc/passwd`:

```text
-d: → colon is the separator
-f5 → select column 5
```

---

# Q12. Print columns 1 to 4 from `/etc/passwd`

### Command

```bash
sudo sh -c "cut -d: -f1-4 /etc/passwd > /file2.txt"
```

### Explanation

```text
-d:
```

means `:` separates the columns.

```text
-f1-4
```

means:

```text
column 1 through column 4
```

### Check

```bash
sudo cat /file2.txt
```

### What we learned

`-f1-4` selects a range of columns.

---

# Q13. Print columns 1 and 7

### Command

```bash
sudo sh -c "cut -d: -f1,7 /etc/passwd > /file3.txt"
```

### Explanation

```text
-f1,7
```

means select:

```text
column 1
column 7
```

The comma means we are selecting separate columns.

### Check

```bash
sudo cat /file3.txt
```

### What we learned

```text
-f1,7  → columns 1 and 7
-f1-4  → columns 1 through 4
```

---

# Q14. Sort the first column alphabetically

### What do we need to do?

We need to:

1. Extract column 1.
2. Send it to `sort`.
3. Sort it alphabetically.
4. Save the result.

### Command

```bash
sudo sh -c "cut -d: -f1 /etc/passwd | sort > /file4.txt"
```

### Explanation

First:

```bash
cut -d: -f1 /etc/passwd
```

gets column 1.

Then:

```text
|
```

sends that output to the next command.

Then:

```bash
sort
```

sorts the names alphabetically.

Finally:

```text
> /file4.txt
```

saves the result.

### Check

```bash
sudo cat /file4.txt
```

### What we learned

The pipe `|` connects commands.

```text
Command 1 | Command 2
```

means:

**Take the output of Command 1 and give it to Command 2.**

---

# Q15. Extract column 3 from `/etc/passwd`

### Command

```bash
sudo sh -c "cut -d: -f3 /etc/passwd > /userid.txt"
```

### Explanation

```text
-d:
```

→ `:` is the delimiter.

```text
-f3
```

→ select column 3.

In `/etc/passwd`, column 3 contains the **UID (User ID)**.

### Check

```bash
sudo cat /userid.txt
```

### What we learned

`cut -d: -f3` extracts the third column.

---

# Q16. Use `awk` to print the first and last columns

### What do we need to do?

We need to print:

* First column
* Last column

For this task, we use `awk`.

### Command

```bash
sudo sh -c "awk -F: '{print \$1, \$NF}' /etc/passwd > /awkfile.txt"
```

### Explanation

```text
awk
```

→ processes text and columns.

```text
-F:
```

→ tells `awk` that `:` separates the fields.

```text
$1
```

→ first column.

```text
$NF
```

→ last column.

`NF` means **Number of Fields**.

Therefore:

```text
$NF
```

means the last field.

### Why is `$` written as `\$`?

Because we are putting the `awk` command inside:

```bash
sudo sh -c "..."
```

The `\` prevents the outer shell from interpreting `$1` and `$NF`.

### Check

```bash
sudo cat /awkfile.txt
```

### What we learned

With `awk`:

```text
$1  → first column
$2  → second column
$3  → third column
$NF → last column
```

---

# Q17. Use `awk` to print columns 1, 2 and 3 using `-` as output delimiter

### What do we need to do?

We need to:

1. Read `/etc/passwd`.
2. Select columns 1, 2 and 3.
3. Put `-` between them.
4. Save the output.

### Command

```bash
sudo sh -c "awk -F: 'BEGIN {OFS=\"-\"} {print \$1, \$2, \$3}' /etc/passwd > /awkfile2.txt"
```

### Explanation

```text
-F:
```

→ `:` is the input field separator.

```text
$1
```

→ first column.

```text
$2
```

→ second column.

```text
$3
```

→ third column.

```text
OFS="-"
```

→ Output Field Separator is `-`.

For example:

Without `OFS`:

```text
root x 0
```

With:

```text
OFS="-"
```

we get:

```text
root-x-0
```

### Check

```bash
sudo cat /awkfile2.txt
```

### Example output

```text
root-x-0
bin-x-1
daemon-x-2
```

### What we learned

`OFS` controls how `awk` separates multiple columns when printing them.

---

# Q18. Find `nologin` lines and print only the first column

### What do we need to do?

We need to:

1. Search `/etc/passwd`.
2. Find lines containing `nologin`.
3. Print only the first column.
4. Save the result to `/awkfile3.txt`.

### Command

```bash
sudo sh -c "awk -F: '/nologin/ {print \$1}' /etc/passwd > /awkfile3.txt"
```

### Explanation

```text
awk -F:
```

→ tells `awk` that `:` separates the columns.

```text
/nologin/
```

→ searches for lines containing `nologin`.

```text
{print $1}
```

→ prints only the first column.

```text
> /awkfile3.txt
```

→ saves the result.

### Example

Suppose the line is:

```text
operator:x:11:0:operator:/root:/sbin/nologin
```

`awk` sees:

```text
$1 = operator
$2 = x
$3 = 11
$4 = 0
...
$7 = /sbin/nologin
```

Because the line contains `nologin`, it prints:

```text
operator
```

### Check

```bash
sudo cat /awkfile3.txt
```

### What we learned

`awk` can **search a condition and print a specific column**.

---

# Important Linux Commands

| Command   | Meaning                           |                                |
| --------- | --------------------------------- | ------------------------------ |
| `head`    | Show beginning of a file          |                                |
| `tail`    | Show end of a file                |                                |
| `grep`    | Search text                       |                                |
| `grep -c` | Count matching lines              |                                |
| `grep -E` | Extended pattern matching         |                                |
| `cut`     | Extract columns                   |                                |
| `sort`    | Sort data                         |                                |
| `awk`     | Process and extract text          |                                |
| `sudo`    | Run with administrator privileges |                                |
| `sh -c`   | Execute a command string          |                                |
| `>`       | Redirect output to a file         |                                |
| `         | `                                 | Send output to another command |

---

# Important Options and Symbols

## `head`

```bash
head -n 10 file.txt
```

→ First 10 lines.

```bash
head -c 100 file.txt
```

→ First 100 characters.

---

## `tail`

```bash
tail -n 10 file.txt
```

→ Last 10 lines.

---

## `grep`

```bash
grep "word" file.txt
```

→ Search for `word`.

```bash
grep -c "word" file.txt
```

→ Count matching lines.

```bash
grep "word$" file.txt
```

→ Search for lines ending with `word`.

---

## `grep -E`

```bash
grep -E "root|rhel|systemd" file.txt
```

`|` means **OR**.

---

## `cut`

```bash
cut -d: -f5 /etc/passwd
```

* `-d:` → `:` is delimiter
* `-f5` → fifth column

```bash
cut -d: -f1-4 /etc/passwd
```

→ columns 1 to 4.

```bash
cut -d: -f1,7 /etc/passwd
```

→ columns 1 and 7.

---

## `awk`

```text
-F:
```

→ `:` is the field separator.

```text
$1
```

→ first column.

```text
$2
```

→ second column.

```text
$3
```

→ third column.

```text
$NF
```

→ last column.

```text
OFS="-"
```

→ output columns are separated by `-`.

---

# Understanding `sudo sh -c`

Sometimes we save output to a protected location such as:

```text
/file.txt
```

A normal user may not have permission to create files directly under `/`.

This may fail:

```bash
sudo head -n 10 /etc/passwd > /file.txt
```

Why?

Because `sudo` applies to `head`, but the `>` redirection is handled by the current shell.

Instead:

```bash
sudo sh -c "head -n 10 /etc/passwd > /file.txt"
```

Here the **complete command**, including the redirection, runs with administrator permission.

### Simple rule

```text
sudo command
```

→ run the command as root.

```text
sudo sh -c "command > file"
```

→ run the complete command, including `>`, as root.

---

# What I Learned

After completing these 18 tasks, I learned how to:

* Display the beginning of files using `head`
* Display the end of files using `tail`
* Search text using `grep`
* Count matching lines using `grep -c`
* Use `$` to match the end of a line
* Search multiple patterns using `grep -E`
* Extract columns using `cut`
* Use delimiters with `cut -d`
* Sort output using `sort`
* Connect commands using `|`
* Process columns using `awk`
* Use `$1`, `$2`, `$3`, and `$NF`
* Use `OFS` to change output separators
* Redirect output using `>`
* Use `sudo` for administrator permissions
* Understand when `sudo sh -c` is needed

---

# Final Summary

These Linux commands are commonly used in:

* Linux system administration
* DevOps
* AWS/Cloud
* Server management
* Log analysis
* Shell scripting
* Text processing

**Linux Basics – Day 3 completed with 18 practical tasks.**
