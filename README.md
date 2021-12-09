# common-container-exit-codes

Knowing this is especially helpful for Day 2 operations when your org recently adopt Kubernetes.

![image](https://user-images.githubusercontent.com/627278/145432100-9071ff9a-9134-481e-8ee3-00db891ac3f9.png)


## Common exit codes

Container exit codes follow [chroot exit codes](https://tldp.org/LDP/abs/html/exitcodes.html).


| Exit Code | Description                                                                                              | Example                                                                           |
|-----------|----------------------------------------------------------------------------------------------------------|-----------------------------------------------------------------------------------|
|     0     | Absence of an attached foreground process                                                                |                                                                                   |
|     1     | Failed due to application error. Catchall for general errors                                             | Miscellaneous errors, such as "divide by zero" and other impermissible operations |
|     2     | Misuse of shell builtins (according to Bash documentation)                                               |                                                                                   |
|    126    | Permission problem or command is not executable                                                          |                                                                                   |
|    127    | Possible some typos in shell script with unrecognizable characters, command not found, etc..             | Possible problem with $PATH or a typo                                             |
|    128    | Invalid argument to exit                                                                                 | exit takes only integer args in the range 0-255                                   |
|   128+n   | Fatal error signal "n"                                                                                   | Control-C is fatal error signal 2. (130 = 128 + 2). See below                     |
|    130    | Container terminated by ctrl-C                                                                           | (128+2) Container received a Ctrl+C signal                                                                                   |
|    137    | Indicates failure as container received SIGKILL (Manual intervention or ‘oom-killer’ [OUT-OF-MEMORY])    | (128+9)Container received a SIGKILL                                               |
|    139    | Indicates failure as container received SIGSEGV, It could because ‘out of memory’, ‘stack overflow’ etc. | (128+11) Container received a SIGSEGV                                             |
|    143    | Indicates failure as container received SIGTERM                                                          | (128+15) Container received a SIGTERM                                             |

## The 128+n code

For the `128+n` code, it's quite simple. Eg: code `130` = 128+2 meaning it exits because container receive a signal code 2 (which is `Ctrl+C`)

For the list of common `n` signal, see [here](https://www.man7.org/linux/man-pages/man7/signal.7.html)

![image](https://user-images.githubusercontent.com/627278/145429500-e9d7ca8e-8929-4283-8b79-a1af8043f3c4.png)

