# TIL

20.02.2017 - Get PID from a port: `lsof -n -i :PORT | grep LISTEN` for example to get the process that is using port 80: `lsof -n -i :80 | grep LISTEN`.

01.03.2017 - `tput` is a useful command to interact with a TTY:
  - `tput cols` get number of columns.
  - `tput lines` get number of lines.
  - `tput sc` save cursor position.
  - `tput rc` restore cursor position.
  - `tput colors` get number of supported colors.
 
01.03.2017 - When the dimensions of the terminal change a `SIGWINCH` signal is sent.

04.03.2017 - PHP's `microtime` and `time` do not return a monotonic timestamp. This is bad for timing because the returned timestamp is dependent on the user's time setting.

15.06.2017 - Use `CTRL+Z` to pause execution of a long command. To resume simply enter `%`.

23.07.2017 - When bundling packages it's common to set the owner and group to `root:root`.
This is because when extracting as a normal user, tar will set the owner to the current user executing the command.
However, extracting as root retains the owner and group from the tar archive.
This can lead to wrong / corrupt ownership permissions. 
To set the root:root ownership without having to need root permissions you can use `fakeroot` to bundle the tar.

10.08.2017 - PHP's `session_start()` can return `true` even when the session was not created. Workaround: create a value and save it to disk to check if the disk storage is sufficient.

13.08.2017 - `return`ing in a `finally` block causes an exception to be 'swallowed': **A function can either throw an exception or return a value but not both.**

19.11.2017 - Bash's `command &> output` is not POSIX compliant. Portable scripts should use `command > output 2>&1`.

06.03.2017 - Linux kernel modules: 

- Load module: `modprobe <module-name> <module-params>`.
- Unload module: `modprobe -r <module-name>`.
- Force unload: `rmmod -f <module-name>`.
- List loaded modules: `lsmod`.
     
06.03.2017 - nandsim kernel module:

`nandsim` simulates a NAND chip:

first_id_byte=0x00 (manufacturer ID)

second_id_byte=0x00 (chip ID)

third_id_byte=0x00 (optional)

fourth_id_byte=0x00 (optional)

06.03.2017 - One can list all MT-devices with `$ cat /proc/mtd`.

06.03.2017 - Mounting an UBIFS image:

`$ modprobe nandsim (first_id_byte ...)`

`$ modprobe ubi`

`$ ubiformat /dev/mtdX -y -f UBIFS.img` (you may need to use `-O` and `-s`)

`$ ubiattach -p /dev/mtdX`

`$ mount -t ubifs ubiX /path/to/mount/point/`

Unmounting:

`$ umount /path/to/mount/point/`

`$ ubidetach -p /dev/mtdX`

09.03.2018 - Flickering animations in WebKit? Add `transform: translate3d(0, 0, 0);` to element before executing animation.

27.11.2018 - `kill -0 <pid>` (checking if "process exists") can fail with `Operation not permitted`.

17.12.2018 - `seteuid` and `setegid` instead of `setuid` and `setgid` (if you want to change back to root later).

29.03.2019 - If you need to know which user called `sudo [command]` you can read the `SUDO_UID` and `SUDO_GID` environment variables.  

23.06.2019 - `console.log()` in node may leak memory.

23.06.2019 - To test network speed use `pv /dev/zero | nc -l PORT` respectively `nc IP PORT > /dev/null`.

21.07.2020 - One can set `PS1` with a script: `PROMPT_COMMAND` in bash or `precmd()` in ZSH.

30.08.2020 - JavaScript: `ArrayBuffer` is a fast array buffer. Needs a ''view'' to access/modify data. For example `Uint8Array` or `Uint16Array`.

## General commands

- Switch directory: `cd <path>`
- Go back to previous directory: `cd -`
- List contents of directory: `ls`
- List contents of path: `ls <path>`

## GIT

- Init repo: `git init`
- Add file: `git add <filename>`
- Remove file: `git rm [-r] <filename>`
- Remove file without deleting it from disk: `git rm --cached <filename>`
- Show repo status: `git status`
- Commit changes: `git commit`
- Discard changes: `git reset --hard HEAD`

- Create branch: `git branch <name>`
- Switch branch: `git checkout <name>`
- Merge into current branch: `git merge --no-ff <name>`

- Pushing tags: `git push origin tag-name`
- Removing tags on origin: `git push :refs/tags/tag-name`.
- Removing tags locally: `git tag -d tag-name`.

- Show diff between two branches or commits: `git diff <1> <2>`.
- Show diff between current HEAD and last commit: `git diff HEAD^`.

- Nuke repo: `rm -r .git`

## VIM

- Open file: `vim <filename>`

- Go to insert mode: `i`
- Erase character: `x`
- Erase until end of line: `d$`
- Erase word: `dw` or `de`

- Discard changes: `:q!`
- Save changes: `:wq`
