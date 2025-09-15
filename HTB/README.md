![img](https://github.com/hackthebox/public-templates/blob/master/Challenge/assets/banner.png)

<img src="https://github.com/hackthebox/public-templates/blob/master/Challenge/assets/htb.png" style="zoom: 80%;" align=left /> <font size="10">Nuclear Meltdown</font>

**15th September 2025**

**Prepared By:** `GalaGoldking`  
**Challenge Author(s):** `GalaGoldking`  
**Difficulty:** <font color="orange">Very Easy</font>

---

# Synopsis (!)

- The user must exploit an intentionally restricted terminal to read a secret file located at `/opt/secret/flag.txt`. The challenge is solved by using a permitted `echo` command with command-substitution to run `cat` on the secret file.

## Description (!)

This CTF challenge simulates a restricted operator terminal in a DMZ node of a nuclear facility. Many commands are blocked or simulated, but a narrow simulation allowlist permits command substitution for a limited `cat` operation. The flag is stored at `/opt/secret/flag.txt` on the target filesystem and is intended to be retrieved via command substitution inside `echo`.

## Skills Required (!)

- Basic Linux command-line familiarity  
- Understanding of command substitution (`$(...)` and backticks)  
- Reading/examining server-side source code (Python/Flask)  
- Basic reasoning about simulated vs. real filesystem behavior

## Skills Learned (!)

- How command substitution can expose file contents even in restricted shells  
- How a simulated environment may expose an attack surface if file reads are allowed in a controlled helper function  
- How to reason about intended vs. fallback behavior in CTF challenge code

# Enumeration (!)

## Analyzing the source code (*)

Files provided for this challenge include (at minimum):

- `main.py` — the Flask application that implements the simulated restricted terminal and command handling.  
- `templates/index.html` — the web frontend terminal UI that POSTs commands to `/api/execute`.  
- `Dockerfile` and `flag.txt` — used to run the challenge; they are present but not required to understand the intended solution.

A short summary of the interesting points in the code:

1. There is a `BLOCKED_COMMANDS` list in `main.py` intended to prevent dangerous commands, but the server implements a custom command simulation instead of executing a real shell.  
2. `simulate_echo()` specifically parses for command substitution patterns (`$()` and backticks) and implements a narrowly-scoped handler that allows `cat <path>` where the path resolution checks simulated paths and the real filesystem.  
3. The application copies a shipped `flag.txt` (if present beside `main.py`) into `/opt/secret/flag.txt` when the server starts; the flag content is not stored in `FILE_CONTENTS` but is placed on the real filesystem under `/opt/secret/flag.txt`.  
4. The frontend (`templates/index.html`) sends user commands to `/api/execute` as JSON; it also contains a local fallback simulation for offline use that **does not** reveal the flag.

# Solution (!)

## Finding the vulnerability (*)

The key vulnerability is the combination of:

- The server allowing command substitution inside `echo` via `simulate_echo()`.  
- The `simulate_echo()` permitting a limited `cat <path>` behavior for absolute paths and a fallback to read files from the real filesystem (i.e., it will `open()` and return contents if `/opt/secret/flag.txt` exists on disk).

Because `simulate_echo()` explicitly attempts to open files when the substitution is `cat /opt/secret/flag.txt`, an attacker can place a `cat` inside an `echo` substitution and retrieve the file contents even though many commands appear blocked.

## Exploitation (!)

### Connecting to the server (*)

Run the challenge (typically via Docker as packaged) and open the web interface. The terminal UI sends commands to `/api/execute` (HTTP POST with JSON `{ "command": "..." }`).

### Attack steps and PoC

1. From the web terminal (or by POSTing to `/api/execute`) submit the following command exactly as shown: `echo $(cat /opt/secret/flag.txt)`


2. The server's `simulate_echo()` will detect the `$(...)` substitution, see the inner command `cat /opt/secret/flag.txt`, and since the file exists on the server filesystem it will read and return its contents. The `echo` output returned to the web UI will therefore contain the flag.

3. The frontend checks output for a flag pattern (e.g. `HTB{...}`) and will present a success modal when it finds the flag string.

### Getting the flag (!)

Recap:

- The intended and supported method to retrieve the flag is to use command substitution inside `echo` to run `cat` on the absolute path `/opt/secret/flag.txt`.  
- Example command to retrieve the flag: `echo $(cat /opt/secret/flag.txt)`

This returns the flag in the terminal output (formatted `HTB{...}` in the challenge). The frontend will detect the flag pattern and reveal the success modal.

