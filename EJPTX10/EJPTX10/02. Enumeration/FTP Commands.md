## 📋 FTP Interactive Commands

| Command             | Description                                                         |
| ------------------- | ------------------------------------------------------------------- |
| `!`                 | Run a command on the **local system**.                              |
| `?` / `help`        | Show help for FTP commands.                                         |
| `append`            | Append a **local file** to a **remote file**.                       |
| `ascii`             | Set file transfer type to **ASCII**.                                |
| `bell`              | Toggle **bell alert** after each transfer (default: OFF).           |
| `binary`            | Set file transfer type to **binary**.                               |
| `bye` / `quit`      | Exit FTP session and quit.                                          |
| `cd`                | Change **remote** working directory.                                |
| `close`             | End session and return to prompt.                                   |
| `debug`             | Toggle **debug mode** (default: OFF).                               |
| `delete`            | Delete a file on the **remote system**.                             |
| `dir`               | List remote directory contents (detailed).                          |
| `disconnect`        | Disconnect without exiting FTP client.                              |
| `get` / `recv`      | Download a file from remote to local system.                        |
| `glob`              | Toggle wildcard expansion (default: ON).                            |
| `hash`              | Toggle printing `#` for each data block transferred (default: OFF). |
| `lcd`               | Change **local** working directory.                                 |
| `literal` / `quote` | Send raw command to the remote server.                              |
| `ls` / `mls`        | List remote files (short format).                                   |
| `mdelete`           | Delete **multiple remote files**.                                   |
| `mdir`              | List **multiple remote files** (detailed).                          |
| `mget`              | Download multiple remote files.                                     |
| `mkdir`             | Create a directory on remote system.                                |
| `mput`              | Upload multiple local files to remote.                              |
| `open`              | Connect to a specified FTP server.                                  |
| `prompt`            | Toggle prompt for multiple file transfers (default: ON).            |
| `put` / `send`      | Upload a **single file** to remote system.                          |
| `pwd`               | Show **remote** current directory.                                  |
| `remotehelp`        | Display help for remote commands.                                   |
| `rename`            | Rename a **remote file**.                                           |
| `rmdir`             | Remove a **remote directory**.                                      |
| `status`            | Show current FTP status.                                            |
| `trace`             | Toggle **packet tracing** (default: OFF).                           |
| `type`              | Set/show transfer type (ASCII or Binary).                           |
| `user`              | Specify a different **user** for login.                             |
| `verbose`           | Toggle **verbose mode** (default: ON).                              |

---

## 💻 FTP Command-Line Switches

| Switch          | Description                                                     |
| --------------- | --------------------------------------------------------------- |
| `-v`            | Suppress verbose remote server responses.                       |
| `-n`            | Disable **auto-login** on connect.                              |
| `-i`            | Disable **interactive prompts** for multi-file transfers.       |
| `-d`            | Enable **debugging** (show commands between client/server).     |
| `-g`            | Disable **globbing** (wildcards) for local files.               |
| `-s:filename`   | Run FTP commands from a **script file** (no spaces in path).    |
| `-a`            | Bind data connections to **any local interface**.               |
| `-w:windowsize` | Set **custom transfer buffer size** (default: 4096 bytes).      |
| `-computer`     | Remote hostname or IP (must be **last** parameter on the line). |

---

### ✅ Notes:

- Some commands like `send`, `recv`, `quote`, and `literal` are **aliases**.
    
- Useful for scripting FTP sessions or performing bulk transfers.
    

---
