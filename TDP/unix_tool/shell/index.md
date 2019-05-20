### File Management
#### `ls`: To list out all files within current working directory 
#### `cd`: To open a directory
#### `mv`: Move a file to a direcotry, or to change its name  
#### `rm`: remove a file or a direcoty 
#### `mkdir`: creating a directoy

#### Sample Session: 
```
poyu81:shell$ clear
poyu81:shell$ vim foobar.txt
poyu81:shell$ ls
foobar.txt*  index.md*
poyu81:shell$ mkdir temp_dir
poyu81:shell$ ls
foobar.txt*  index.md*  temp_dir/
poyu81:shell$ cd temp_dir
poyu81:temp_dir$ cd ..
poyu81:shell$ mv foobar.txt temp_dir
poyu81:shell$ ls
index.md*  temp_dir/
poyu81:shell$ cd temp_dir
poyu81:temp_dir$ ls
foobar.txt*
poyu81:temp_dir$ mv foobar.txt hihi.txt
poyu81:temp_dir$ ls
hihi.txt*

```

#### `ln`: creating hard or sym links

```
poyu81:temp_dir$ ls
hihi.txt*
poyu81:temp_dir$ ln hihi.txt hihi_hard_link.txt
poyu81:temp_dir$ ls
hihi.txt*  hihi_hard_link.txt*
poyu81:temp_dir$ ls -la
total 0
drwxrwxrwx 1 poyu81 512 May 19 19:03 ./
drwxrwxrwx 1 poyu81 512 May 19 19:02 ../
-rwxrwxrwx 2 poyu81   0 May 19 18:51 hihi.txt*  	  # Notice the hard link count
-rwxrwxrwx 2 poyu81   0 May 19 18:51 hihi_hard_link.txt*
poyu81:temp_dir$ ln hihi.txt hihi_hard_link2.txt
poyu81:temp_dir$ ls -la
total 0
drwxrwxrwx 1 poyu81 512 May 19 19:03 ./
drwxrwxrwx 1 poyu81 512 May 19 19:02 ../
-rwxrwxrwx 3 poyu81   0 May 19 18:51 hihi.txt*
-rwxrwxrwx 3 poyu81   0 May 19 18:51 hihi_hard_link.txt*
-rwxrwxrwx 3 poyu81   0 May 19 18:51 hihi_hard_link2.txt*
poyu81:temp_dir$ ln -s hihi.txt hihi_soft_link.txt        # Creating a sym link 
poyu81:temp_dir$ ls -la
total 0
drwxrwxrwx 1 poyu81 512 May 19 19:04 ./
drwxrwxrwx 1 poyu81 512 May 19 19:02 ../
-rwxrwxrwx 3 poyu81   0 May 19 18:51 hihi.txt*		  # Hard link count did not change 	
-rwxrwxrwx 3 poyu81   0 May 19 18:51 hihi_hard_link.txt*
-rwxrwxrwx 3 poyu81   0 May 19 18:51 hihi_hard_link2.txt*
lrwxrwxrwx 1 poyu81   8 May 19 19:04 hihi_soft_link.txt -> hihi.txt*
poyu81:temp_dir$
```

### NOTE 
#### `man` command is useful when you forgot what a command does. 
Try `man ln`

### Process Management 
#### ps 
##### List out all processes 
#### top 
##### Shgow current CPU usage 
#### kill 
##### Send kill signal to a particular process (specified with PID)
#### running in order, in background
##### `&` runs process in the background (useful when running server and client)  
##### `;` runs process in order
##### `&&` runs the latter process if only the previous process exited successfully

#### Sample Session with `ps` and `top`
```
poyu81:shell$ ps
  PID TTY          TIME CMD
    4 tty1     00:00:08 bash
  458 tty1     00:00:00 ps
poyu81:shell$ ps -la
F S   UID   PID  PPID  C PRI  NI ADDR SZ WCHAN  TTY          TIME CMD
0 S  1000     4     3  0  80   0 -  4615 -      tty1     00:00:08 bash
0 R  1000   459     4  0  80   0 -  4271 -      tty1     00:00:00 ps
poyu81:shell$ top
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
poyu81:shell$ ./infinite_loop.sh &
[1] 533
poyu81:shell$ sudo kill 533
[1]+  Terminated              ./infinite_loop.sh
poyu81:shell$
```

#### Piping 
##### There are three streams of input and outp[ut for every process.
##### STDIN (standard in): The program reads input 
##### STDOUT (standard out): The program's first option output 
##### STDERR (standard error): the program's second option output 
##### With piping we can manipulate the different input/output streams of a process. 

### Nifty Commands 
#### grep 
#### tail

### Shell Script
#### For loop 
#### If loop 
#### Incorporating common commands trhat we learnt 
#### Whitespace problem 
#### Regular expression 


