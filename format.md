# Contest structure

Over-advanced example can be found at https://github.com/cms-dev/con_test/tree/master/batch

## Root directory

One directory for each task

One file: contest.yaml

### `contest.yaml`

Contains contest name/description and a list of tasks. Task names should match names of subdirectories.

Example:

```yaml
name: "big_contest"
description: "The Big Contest"
tasks:
  - "easy_question"
  - "hard_question"

# these two lines are necessary but don't need to be changed
token_mode: disabled
users: []
```

## Task directories

One task.yaml file and a few directories: input, output, statement, and optionally check.

### `task.yaml`

Metadata for the given task.

Example:

```yaml
name: "easy_question" # should match directory name
title: "Easy Question" # can be anything
time_limit: 1 # timeout in seconds
memory_limit: 256 # memory limit in MB
n_input: 10 # number of test cases

# below shouldn't need to be changed
public_testcases: all # thing for tokens
infile: "" # use stdin for input
outfile: "" # use stdout for output
```

### `input` directory

Should contain input files, named input0.txt to inputN.txt.

### `output` directory

Output files, named output0.txt to outputN.txt.

### `statement` directory

Should contain one file, `statement.pdf`, which will be available on the task page.

### `check` directory (optional)

If needed, contains the checker program. Should be a single executable named `checker`.
Python scripts appear to work with the correct hashbang, as an example:

```python
#!/usr/bin/python3

# accept any output that contains a single even number

import sys

def correct():
    print("1.0") # score, usually 1.0
    print("Correct", sys.stderr) # message shown to the user
    sys.exit(0)

def wrong():
    print("0.0")
    print("Wrong", sys.stderr)
    sys.exit(0)

input_f, correct_output_f, user_output_f = sys.argv[1:]

with open(user_output_f) as f:
    n = int(f.read().strip())

    if n % 2 == 0:
        correct()
    else:
        wrong()
```
