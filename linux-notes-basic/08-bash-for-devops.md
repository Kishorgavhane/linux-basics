# Bash for DevOps

Bash is not about becoming a programmer.
For DevOps, Bash is about **making Linux repeat work for you**.

If you can automate even small tasks,
you reduce errors, save time, and stay calm during pressure.

---

## What Bash Really Is

Bash is:
- a shell
- a command interpreter
- a way to group commands together

Instead of typing commands again and again,
you teach Bash **what steps to follow**.

---

## Why DevOps Engineers Use Bash

DevOps uses Bash to:
- automate setup steps
- check system health
- deploy applications
- clean logs
- glue tools together

Bash scripts are usually:
- short
- readable
- practical

---

## My First Bash Script

Create a file:
```bash
nano hello.sh
```

Add this content:
```bash
#!/bin/bash
echo "Hello from Bash"
```

Save and exit.

Make it executable:
```bash
chmod +x hello.sh
```

Run it:
```bash
./hello.sh
```

This is already automation.

---


Understanding the First Line
```bash
#!/bin/bash
```

This line tells Linux:

> “Use Bash to run this file”

Without this line,
Linux does not know how to execute the script.

---

 ## Running Commands Inside a Script

 A Bash script is just commands written line by line.

Example:
```bash
#!/bin/bash
pwd
ls
whoami
```

---

 ## Variables (Storing Information)

Variables help you reuse values.

Example:
```bash
#!/bin/bash
NAME="DevOps"
echo "Welcome $NAME"
```

Variables:
- reduce repetition
- make scripts readable

---

 ## Command Output as Variable

Sometimes you want command results.
Example:
```bash
DATE=$(date)
echo "Today is $DATE"
```

---

 ## Input from User

 ```bash
#!/bin/bash
echo "Enter your name:"
read USER
echo "Hello $USER"
```

---

Conditions
Scripts often need decisions.
Example:
```bash
#!/bin/bash
if [ -f "/etc/passwd" ]; then
  echo "File exists"
else
  echo "File not found"
fi
```

This teaches Bash:
>“Check first, then act”

---

Loops
Loops remove manual repetition.
Example:
```bash
#!/bin/bash
for i in 1 2 3
do
  echo "Number $i"
done
```

DevOps scripts often loop over:
- servers
- files
- services

---

 ## Checking Command Success
Every command returns a status.
```bash
echo $?
```

- 0 → success
- non-zero → something failed

Example:
```bash
#!/bin/bash
ls /tmp
if [ $? -eq 0 ]; then
  echo "Command succeeded"
fi
```

---

 ## Bash in Real DevOps Tasks

Examples:
- check disk usage
- restart services if down
- clean old files
- print system health
Bash is glue, not magic.

---

 ## Hands-On Learning

 ```bash
bash --version
echo "Learning Bash"
date
whoami
```

Then:
```bash
nano test.sh
```

---

 ## Important Bash Commands

 ```bash
bash            # start-shell
chmod +x        # make-executable
./script.sh     # run-script
read            # user-input
if              # condition
for             # loop
$?              # status-code
```
