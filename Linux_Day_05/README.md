---

## 📄 Sample Log File

> Create this sample `yc.log` file for practicing all the commands above

### 💾 Sample Content
```log
2024-01-15 08:50:30 INFO Application started successfully
2024-01-15 08:51:15 DEBUG Loading configuration files  
2024-01-15 08:51:45 INFO Configuration loaded
2024-01-15 08:52:# 🐧 Linux Day 05 Pro Commands
## 🔥 Advanced Text Processing with AWK, SED, and GREP

> **Master the three most powerful text processing tools in Linux**  
> *Essential commands for system administrators, developers, and power users*

---

## 📚 Table of Contents
- [🔧 AWK Commands](#-awk-commands)
  - [Column Operations](#column-operations)
  - [Pattern Matching & Filtering](#pattern-matching-and-filtering)
  - [Counting Operations](#counting-operations)
  - [Time-Based Filtering](#time-based-filtering)
  - [Line Number Operations](#line-number-operations)
  - [Advanced AWK Examples](#advanced-awk-examples)
- [✏️ SED Commands](#️-sed-commands)
  - [Substitution Commands](#substitution-commands)
  - [Advanced SED Examples](#advanced-sed-examples)
- [🔍 GREP Commands](#-grep-commands)
  - [Basic Pattern Matching](#basic-pattern-matching)
  - [Advanced GREP Options](#advanced-grep-options)
- [📄 Sample Log File](#-sample-log-file)
- [💪 Practice Exercises](#-practice-exercises)
- [🚀 Command Combinations](#-command-combinations)
- [💡 Tips and Best Practices](#-tips-and-best-practices)

---

## 🔧 AWK Commands

> **AWK** is a powerful pattern-scanning and processing language for text files. It processes files line by line and can perform complex operations.

### 📖 Basic Syntax
```bash
awk 'pattern { action }' filename
```

### 🎯 Key Concepts
- `$0` = Entire line
- `$1, $2, $3...` = Column 1, Column 2, Column 3...
- `NR` = Number of Records (Line Number)
- `NF` = Number of Fields (Columns in current line)
- `FS` = Field Separator (default: whitespace)

### 📊 Column Operations

> **Your Examples (User Provided)**

#### 🔸 Print Specific Columns
```bash
# 💡 Print first three columns ($1, $2, $3 represent columns)
awk '{print $1,$2,$3}' yc.log

# 💡 Print all columns (default behavior)
awk '{print}' yc.log
```

#### 🔹 Additional Examples
```bash
# Print specific columns with custom separator
awk '{print $1 " | " $2 " | " $3}' yc.log

# Print last column
awk '{print $NF}' yc.log

# Print first and last columns
awk '{print $1, $NF}' yc.log

# Add custom text to output
awk '{print "Date: " $1 ", Time: " $2 ", Level: " $3}' yc.log
```

### 🎯 Pattern Matching and Filtering

> **Your Examples (User Provided)**

#### 🔸 Using Filters (/ / = Filter Pattern)
```bash
# 💡 Filter lines containing "INFO" and print them
awk '/INFO/{print}' yc.log

# 💡 Filter and redirect to new file
awk '/INFO/{print}' yc.log > new_yc.log
```

#### 🔹 Additional Filtering Examples
```bash
# Filter multiple patterns (OR operation)
awk '/INFO|ERROR/{print}' yc.log

# Filter with NOT condition
awk '!/DEBUG/{print}' yc.log

# Case-insensitive filtering
awk 'toupper($0) ~ /INFO/ {print}' yc.log

# Filter based on specific column
awk '$3 == "ERROR" {print}' yc.log

# Complex conditions
awk '/ERROR/ && $2 > "08:50:00" {print}' yc.log
```

### 🔢 Counting Operations

> **Your Examples (User Provided)**

#### 🔸 Count Pattern Occurrences
```bash
# 💡 Count INFO occurrences
awk '/INFO/{count++} END {print count}' yc.log

# 💡 Count with descriptive message
awk '/INFO/{count++} END {print "The count of info is: " count}' yc.log
```

#### 🔹 Additional Counting Examples
```bash
# Count total lines
awk 'END {print "Total lines: " NR}' yc.log

# Count non-empty lines
awk 'NF > 0 {count++} END {print "Non-empty lines: " count}' yc.log

# Count different log levels
awk '{level[$3]++} END {for(i in level) print i ": " level[i]}' yc.log

# Count words in entire file
awk '{words += NF} END {print "Total words: " words}' yc.log

# Count lines with specific column value
awk '$3 == "ERROR" {count++} END {print "Error count: " count}' yc.log
```

### ⏰ Time-Based Filtering

> **Your Examples (User Provided)**

#### 🔸 Filter by Time Range
```bash
# 💡 Filter logs between specific times (assuming time is in column 2)
awk '$2 >= "08:51:06" && $2 <= "08:53:22"{print $2}' yc.log
```

#### 🔹 Additional Time Filtering Examples
```bash
# Print entire line for time range
awk '$2 >= "08:51:06" && $2 <= "08:53:22"{print}' yc.log

# Filter by date and time
awk '$1 == "2024-01-15" && $2 >= "10:00:00"{print}' yc.log

# Filter by hour (extract hour from time)
awk 'substr($2,1,2) == "08" {print}' yc.log

# Time range with specific log level
awk '$2 >= "08:50:00" && $2 <= "09:00:00" && $3 == "ERROR" {print}' yc.log

# Count events per hour
awk '{hour=substr($2,1,2); hours[hour]++} END {for(h in hours) print "Hour " h ": " hours[h]}' yc.log
```

### 📝 Line Number Operations

> **Your Examples (User Provided)**

#### 🔸 Working with Line Numbers (NR)
```bash
# 💡 Print lines 2 to 10 (NR = Number of Records/Rows)
awk 'NR>=2 && NR<=10 {print}' yc.log

# 💡 Print line numbers for lines 2 to 10
awk 'NR>=2 && NR<=10 {print NR}' yc.log
```

#### 🔹 Additional Line Number Examples
```bash
# Print line number with content
awk 'NR>=2 && NR<=10 {print NR ": " $0}' yc.log

# Print first 5 lines
awk 'NR<=5 {print}' yc.log

# Print every 3rd line
awk 'NR%3==0 {print}' yc.log

# Print last 5 lines (requires two passes)
awk 'END {for(i=NR-4; i<=NR; i++) if(i>0) print line[i]} {line[NR]=$0}' yc.log

# Skip first line (header)
awk 'NR>1 {print}' yc.log

# Print specific line numbers
awk 'NR==5 || NR==10 || NR==15 {print NR ": " $0}' yc.log
```

### 🚀 Advanced AWK Examples

#### 📊 Mathematical Operations
```bash
# Sum values in column 3 (if numeric)
awk '{sum += $3} END {print "Total: " sum}' numbers.txt

# Calculate average
awk '{sum += $3; count++} END {print "Average: " sum/count}' numbers.txt

# Find maximum value
awk 'NR==1{max=$3} $3>max{max=$3} END{print "Max: " max}' numbers.txt

# Find minimum and maximum
awk 'NR==1{min=max=$3} $3<min{min=$3} $3>max{max=$3} END{print "Min: " min ", Max: " max}' numbers.txt
```

#### 🔧 Field Separator Operations
```bash
# Use comma as field separator
awk -F',' '{print $1, $2}' data.csv

# Use multiple separators
awk -F'[,:]' '{print $1, $3}' mixed_data.txt

# Change output field separator
awk 'BEGIN{OFS="|"} {print $1, $2, $3}' yc.log

# Use tab as separator
awk -F'\t' '{print $1 " -> " $2}' tab_separated.txt
```

#### 🎨 String Operations
```bash
# Convert to uppercase
awk '{print toupper($0)}' yc.log

# Convert to lowercase
awk '{print tolower($3)}' yc.log

# String length
awk '{print "Line " NR " has " length($0) " characters"}' yc.log

# Substring extraction
awk '{print substr($2, 1, 5)}' yc.log  # First 5 characters of column 2

# String replacement
awk '{gsub(/INFO/, "INFORMATION"); print}' yc.log
```

---

## ✏️ SED Commands

> **SED (Stream Editor)** is used for filtering and transforming text. It performs basic text transformations on input streams.

### 📖 Basic Syntax
```bash
sed 'command' filename
```

### 🎯 Key Concepts
- `s` = Substitute command
- `g` = Global flag (replace all occurrences)
- `d` = Delete command
- `p` = Print command
- `i` = Case-insensitive flag
- `n` = Quiet mode (suppress automatic printing)

### 🔄 Substitution Commands

> **Your Examples (User Provided)**

#### 🔸 Basic Substitution
```bash
# 💡 Replace INFO with LOG (s = substitute, g = global)
sed 's/INFO/LOG/g' yc.log

# 💡 Show line numbers for INFO lines and print them
sed -n -e '/INFO/=' -e '/INFO/p' yc.log

# 💡 Replace INFO with LOG in first 10 lines only
sed '1,10 s/INFO/LOG/g' yc.log

# 💡 Replace in first 10 lines, print them, then quit at line 11
sed '1,10 s/INFO/LOG/g; 1,10p; 11q' yc.log
```

#### 🔹 Additional Substitution Examples
```bash
# Replace only first occurrence per line
sed 's/INFO/LOG/' yc.log

# Case-insensitive replacement
sed 's/info/LOG/gi' yc.log

# Replace with special characters
sed 's/ERROR/[ERROR]/g' yc.log

# Replace in specific line (line 5)
sed '5 s/INFO/LOG/g' yc.log

# Replace using different delimiter (useful when pattern contains /)
sed 's|/home/user|/home/newuser|g' file.txt

# Replace with captured groups
sed 's/\([0-9]*\)-\([0-9]*\)-\([0-9]*\)/\3\/\2\/\1/g' yc.log  # Change date format
```

### 🚀 Advanced SED Examples

#### 🗑️ Deletion Operations
```bash
# Delete lines containing INFO
sed '/INFO/d' yc.log

# Delete first line
sed '1d' yc.log

# Delete lines 2-5
sed '2,5d' yc.log

# Delete empty lines
sed '/^$/d' yc.log

# Delete lines starting with #
sed '/^#/d' yc.log

# Delete last line
sed '$d' yc.log
```

#### ➕ Insertion and Appending
```bash
# Insert text before line 1
sed '1i\=== LOG FILE HEADER ===' yc.log

# Append text after lines containing ERROR
sed '/ERROR/a\>>> Check this error immediately <<<' yc.log

# Replace entire line containing INFO
sed '/INFO/c\This line contained INFO' yc.log

# Insert multiple lines
sed '1i\Line 1\nLine 2\nLine 3' yc.log
```

#### 🔧 Multiple Operations
```bash
# Multiple substitutions using -e flag
sed -e 's/INFO/LOG/g' -e 's/ERROR/FAULT/g' yc.log

# Using semicolon for multiple commands
sed 's/INFO/LOG/g; s/ERROR/FAULT/g' yc.log

# Complex multi-line operation
sed '/ERROR/,+2d' yc.log  # Delete ERROR line and next 2 lines

# Range operations
sed '5,10s/INFO/DEBUG/g' yc.log  # Replace only in lines 5-10
```

#### 🎯 Advanced Pattern Operations
```bash
# Print only lines matching pattern (quiet mode)
sed -n '/ERROR/p' yc.log

# Print line numbers and content for matches
sed -n '/ERROR/{=; p;}' yc.log

# Multiple patterns
sed -n '/INFO\|ERROR/p' yc.log

# Use variables in sed
pattern="ERROR"
sed "s/$pattern/CRITICAL/g" yc.log
```

---

## 🔍 GREP Commands

> **GREP (Global Regular Expression Print)** searches for patterns in files and prints matching lines.

### 📖 Basic Syntax
```bash
grep [options] pattern filename
```

### 🎯 Key Options
- `-i` = Case-insensitive search
- `-c` = Count matches only
- `-n` = Show line numbers
- `-v` = Invert match (show non-matching lines)
- `-r` = Recursive search
- `-l` = Show only filenames with matches
- `-o` = Show only matched text
- `-E` = Extended regex
- `-w` = Match whole words only

### 🎯 Basic Pattern Matching

> **Your Examples (User Provided)**

#### 🔸 Simple Search
```bash
# 💡 Print lines containing INFO
grep INFO yc.log

# 💡 Case-insensitive search (ignore case sensitivity like info, INFO)
grep -i info yc.log

# 💡 Count occurrences (-c flag) e.g: 73
grep -i -c info yc.log
```

#### 🔹 Additional Basic Examples
```bash
# Show line numbers with matches
grep -n INFO yc.log

# Show filename with matches (useful with multiple files)
grep -H INFO yc.log

# Show context (2 lines before and after)
grep -C 2 ERROR yc.log

# Show only before context
grep -B 2 ERROR yc.log

# Show only after context  
grep -A 2 ERROR yc.log

# Combine options
grep -i -n -C 1 error yc.log
```

### 🚀 Advanced GREP Options

#### 🔧 Extended Options
```bash
# Show lines that DON'T match (-v flag)
grep -v INFO yc.log

# Show only matched words (-o flag)
grep -o INFO yc.log

# Recursive search in directories (-r flag)
grep -r ERROR /var/log/

# Search multiple files
grep INFO *.log

# Search with wildcards
grep "INFO.*success" yc.log

# Silent mode (only exit code, no output)
grep -q ERROR yc.log && echo "Errors found"
```

#### 🎨 Pattern Matching & Regex
```bash
# Multiple patterns (OR operation using -E)
grep -E "INFO|ERROR|WARN" yc.log

# Lines starting with ERROR (^ = start of line)
grep "^ERROR" yc.log

# Lines ending with 'completed' ($ = end of line)
grep "completed$" yc.log

# Time pattern HH:MM using regex
grep -E "[0-9]{2}:[0-9]{2}:[0-9]{2}" yc.log

# Word boundary matching (-w = whole word)
grep -w "log" yc.log

# Any single character (. = any character)
grep "ER.OR" yc.log

# Character classes
grep "[0-9]" yc.log          # Lines with numbers
grep "[A-Z]" yc.log          # Lines with uppercase
grep "^[A-Za-z]" yc.log      # Lines starting with letter

# Quantifiers
grep "E.*R" yc.log           # E followed by any chars, then R
grep "INFO\+" yc.log         # One or more INFO
grep "LOG\?" yc.log          # Optional LOG
```

#### 📁 File Operations
```bash
# Show only filenames containing pattern (-l flag)
grep -l ERROR *.log

# Show filenames that DON'T contain pattern (-L flag)  
grep -L ERROR *.log

# Count matches per file (-c flag with multiple files)
grep -c ERROR *.log

# Include/exclude files by pattern
grep --include="*.log" -r ERROR /var/log/
grep --exclude="debug.log" ERROR *.log

# Read patterns from file
grep -f patterns.txt yc.log

# Fixed string search (no regex) 
grep -F "INFO[DEBUG]" yc.log
```

#### 🎯 Advanced Combinations
```bash
# Case insensitive with line numbers and color
grep -i -n --color=always ERROR yc.log

# Multiple conditions with pipes
grep INFO yc.log | grep -v DEBUG

# Before and after context with different amounts
grep -B 1 -A 3 ERROR yc.log

# Maximum matches
grep -m 5 INFO yc.log        # Stop after 5 matches

# Binary files
grep -a "pattern" binaryfile  # Treat as text

# Count unique matches
grep -o "INFO" yc.log | sort | uniq -c
```

---

## Sample Log File

Here's a sample `yc.log` file for practicing the commands:

```
2024-01-15 08:50:30 INFO Application started successfully
2024-01-15 08:51:15 DEBUG Loading configuration files
2024-01-15 08:51:45 INFO Configuration loaded
2024-01-15 08:52:10 WARN Memory usage high: 85%
2024-01-15 08:52:30 ERROR Database connection failed
2024-01-15 08:53:00 INFO Retrying database connection
2024-01-15 08:53:22 INFO Database connected successfully
2024-01-15 08:54:00 DEBUG Processing user requests
2024-01-15 08:54:30 INFO User authentication completed
2024-01-15 08:55:00 ERROR Timeout occurred for user session
```

Create this sample file using:
```bash
cat > yc.log << 'EOF'
2024-01-15 08:50:30 INFO Application started successfully
2024-01-15 08:51:15 DEBUG Loading configuration files
2024-01-15 08:51:45 INFO Configuration loaded
2024-01-15 08:52:10 WARN Memory usage high: 85%
2024-01-15 08:52:30 ERROR Database connection failed
2024-01-15 08:53:00 INFO Retrying database connection
2024-01-15 08:53:22 INFO Database connected successfully
2024-01-15 08:54:00 DEBUG Processing user requests
2024-01-15 08:54:30 INFO User authentication completed
2024-01-15 08:55:00 ERROR Timeout occurred for user session
EOF
```

---

## Practice Exercises

### AWK Exercises
1. **Extract Time and Message**: Print only the time (column 2) and log level (column 3) from yc.log
   ```bash
   awk '{print $2, $3}' yc.log
   ```

2. **Count Different Log Levels**: Count INFO, ERROR, WARN, and DEBUG separately
   ```bash
   awk '{level[$3]++} END {for(i in level) print i ": " level[i]}' yc.log
   ```

3. **Filter by Time and Level**: Show only ERROR messages between 08:52:00 and 08:55:00
   ```bash
   awk '$2 >= "08:52:00" && $2 <= "08:55:00" && $3 == "ERROR" {print}' yc.log
   ```

### SED Exercises
1. **Clean Log Format**: Remove timestamps and keep only log level and message
   ```bash
   sed 's/^[0-9-]* [0-9:]* //' yc.log
   ```

2. **Standardize Log Levels**: Convert all ERROR to CRITICAL
   ```bash
   sed 's/ERROR/CRITICAL/g' yc.log
   ```

3. **Add Line Numbers**: Add line numbers to the beginning of each line
   ```bash
   sed '=' yc.log | sed 'N;s/\n/: /'
   ```

### GREP Exercises
1. **Find Critical Events**: Search for ERROR or WARN messages
   ```bash
   grep -E "ERROR|WARN" yc.log
   ```

2. **Database Related Logs**: Find all lines mentioning "Database"
   ```bash
   grep -i database yc.log
   ```

3. **Time Range Analysis**: Find logs between specific times using grep with regex
   ```bash
   grep "08:5[2-4]:" yc.log
   ```

---

## Command Combinations

### Powerful Pipeline Examples

#### AWK + SED + GREP Combined
```bash
# Extract errors, clean format, and count
grep ERROR yc.log | sed 's/^.*ERROR/ERROR/' | awk '{count++} END {print "Errors: " count}'

# Find INFO messages, replace timestamp format, show first 5
grep INFO yc.log | sed 's/-/\//g' | awk 'NR<=5 {print}'

# Complex log analysis pipeline
awk '$3 == "ERROR" {print}' yc.log | sed 's/ERROR/[ERROR]/g' | grep -c "\[ERROR\]"
```

---

## Tips and Best Practices

### Performance Tips
1. **Use grep first** in pipelines to filter data before processing with awk or sed
2. **Avoid unnecessary global replacements** - use specific line ranges when possible
3. **Use -F option in awk** for fixed strings instead of regex when appropriate

### Common Pitfalls
1. **Field separation**: Remember that awk splits on whitespace by default
2. **Regex escaping**: Special characters need escaping in different tools
3. **Line endings**: Be aware of different line ending formats (Unix vs Windows)

### Useful Combinations
```bash
# Log analysis workflow
grep -i error logfile | awk '{print $1, $2}' | sed 's/ERROR/CRITICAL/' > critical_events.log

# Statistical analysis
awk '/ERROR/ {errors++} /WARN/ {warns++} END {print "Errors:", errors, "Warnings:", warns}' yc.log
```

---

**Remember**: Practice these commands with your own log files to become proficient. Each tool has its strengths - grep for searching, sed for simple transformations, and awk for complex text processing and calculations.

---

*Generated for Linux Day 05 Pro Commands Training*