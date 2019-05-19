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
##### `&` runs process in the background 
##### `;` runs process in order 

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


