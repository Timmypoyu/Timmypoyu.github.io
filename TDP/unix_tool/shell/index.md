### File Management
#### `ls`: To list out all files within current working directory 
#### `cd`: To open a directory
#### `mv`: Move a file to a direcotry, or to change its name  
#### `rm`: remove a file or a direcoty 
#### `mkdir`: creating a directoy

#### Sample Session: 
```
$ clear
$ vim foobar.txt
$ ls
foobar.txt*  index.md*
$ mkdir temp_dir
$ ls
foobar.txt*  index.md*  temp_dir/
$ cd temp_dir
temp_dir$ cd ..
$ mv foobar.txt temp_dir
$ ls
index.md*  temp_dir/
$ cd temp_dir
temp_dir$ ls
foobar.txt*
temp_dir$ mv foobar.txt hihi.txt
temp_dir$ ls
hihi.txt*

```

#### `ln`: creating hard or sym links

```
temp_dir$ ls
hihi.txt*
temp_dir$ ln hihi.txt hihi_hard_link.txt
temp_dir$ ls
hihi.txt*  hihi_hard_link.txt*
temp_dir$ ls -la
total 0
drwxrwxrwx 1 poyu81 512 May 19 19:03 ./
drwxrwxrwx 1 poyu81 512 May 19 19:02 ../
-rwxrwxrwx 2 poyu81   0 May 19 18:51 hihi.txt*  	  # Notice the hard link count
-rwxrwxrwx 2 poyu81   0 May 19 18:51 hihi_hard_link.txt*
temp_dir$ ln hihi.txt hihi_hard_link2.txt
temp_dir$ ls -la
total 0
drwxrwxrwx 1 poyu81 512 May 19 19:03 ./
drwxrwxrwx 1 poyu81 512 May 19 19:02 ../
-rwxrwxrwx 3 poyu81   0 May 19 18:51 hihi.txt*
-rwxrwxrwx 3 poyu81   0 May 19 18:51 hihi_hard_link.txt*
-rwxrwxrwx 3 poyu81   0 May 19 18:51 hihi_hard_link2.txt*
temp_dir$ ln -s hihi.txt hihi_soft_link.txt        # Creating a sym link 
temp_dir$ ls -la
total 0
drwxrwxrwx 1 poyu81 512 May 19 19:04 ./
drwxrwxrwx 1 poyu81 512 May 19 19:02 ../
-rwxrwxrwx 3 poyu81   0 May 19 18:51 hihi.txt*		  # Hard link count did not change 	
-rwxrwxrwx 3 poyu81   0 May 19 18:51 hihi_hard_link.txt*
-rwxrwxrwx 3 poyu81   0 May 19 18:51 hihi_hard_link2.txt*
lrwxrwxrwx 1 poyu81   8 May 19 19:04 hihi_soft_link.txt -> hihi.txt*
temp_dir$
```

### NOTE 
#### `man` command is useful when you forgot what a command does. 
Try `man ln`

### Process Management 
#### `ps`: List out all processes 
#### `top`: Show current CPU usage 
#### `kill`: Send signal to a particular process (specified with PID), use `-l` to list signal names
 
### Running in order, in background
1. `&` runs process in the background (useful when running server and client), the running program still has terminal as STDOUT 
2. `;` runs process in order
3. `&&` runs the latter process if only the previous process exited successfully

#### `jobs:`: see all running processes 

#### Sample Session with `ps` and `top`
```
$ ps
  PID TTY          TIME CMD
    4 tty1     00:00:08 bash
  458 tty1     00:00:00 ps
$ ps -la
F S   UID   PID  PPID  C PRI  NI ADDR SZ WCHAN  TTY          TIME CMD
0 S  1000     4     3  0  80   0 -  4615 -      tty1     00:00:08 bash
0 R  1000   459     4  0  80   0 -  4271 -      tty1     00:00:00 ps
$ top
top - 21:44:52 up 15:48,  0 users,  load average: 0.52, 0.58, 0.59
Tasks:   4 total,   1 running,   3 sleeping,   0 stopped,   0 zombie
%Cpu(s): 16.2 us, 12.1 sy,  0.0 ni, 71.4 id,  0.0 wa,  0.3 hi,  0.0 si,  0.0 st
KiB Mem :  8192044 total,  2444232 free,  5518460 used,   229352 buff/cache
KiB Swap: 25165824 total, 25089056 free,    76768 used.  2539852 avail Mem

  PID USER      PR  NI    VIRT    RES    SHR S  %CPU %MEM     TIME+ COMMAND
  460 poyu81    20   0   17636   2064   1504 R   1.0  0.0   0:00.07 top
    1 root      20   0    8304    128    100 S   0.0  0.0   0:00.18 init
    3 root      20   0    8304     96     60 S   0.0  0.0   0:00.00 init
    4 poyu81    20   0   18460   5040   4928 S   0.0  0.1   0:08.39 bash
```

#### Sample Session with `kill` and `&`

```
$ ./infinite_loop.sh &
[1] 533
$ sudo kill 533
[1]+  Terminated              ./infinite_loop.sh
$
```
#### infinite_loop.sh runs a python infinte loop 
```
#!/usr/bin/python 

while True:
	pass
```

##### See `man` page for `kill` to see what other signal you can send to the process. 
##### For a more in-depth understanding of signaling in the operating system. You can checkout 
`man signal` page and [this brief introduction from Tutorialspoint](https://www.tutorialspoint.com/inter_process_communication/inter_process_communication_signals.html).
#### Piping 
##### There are three streams of input and outp[ut for every process.
1. STDIN (standard in): The program reads input
2. STDOUT (standard out): The program's first option output 
3. STDERR (standard error): the program's second option output 
##### With piping we can redirect the different input/output streams of between processes. 
##### For example, `x|y` makes the STDOUT of `x` the STDIN of `y`. 
##### `x>y`, STDOUT of `x` is written to file `y`
#####  `x2>y`, STDERR of x goes into file `y`
##### `x<y`, STDIN of x is read from file `y`  

### Nifty Commands 
#### grep: output the lines that matches specified pattern 
#### tail: out the last part of a file
#### cat: concatenate file content to STDIN and print it (basically, print file content to STDOUT)  

#### Sample Session of piping, `grep`, `tail` and `cat`
```
temp_dir$ cat hihi.txt
Hello World!
Hello Taiwanese Data Professional!
temp_dir$ echo Hi, my name is Timmy. I am fine. Thank you and you? >> hihi.txt
temp_dir$ cat hihi.txt
Hello World!
Hello Taiwanese Data Professional!
Hi, my name is Timmy. I am fine. Thank you and you?
temp_dir$ cat hihi.txt | grep Taiwan
Hello Taiwanese Data Professional!
temp_dir$ tail -n 1 hihi.txt
Hi, my name is Timmy. I am fine. Thank you and you?
temp_dir$

```

### Shell Script
#### For loop 
#### If loop 
#### Incorporating common commands that we learnt 
#### Whitespace problem 
#### Regular expression 

