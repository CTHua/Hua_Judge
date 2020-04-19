# C.D\_Judge

This is a simple C language judge system.  
Only supports on NCCU-ghost(ghost.cs.nccu.edu.tw) currently.  
Created by [CTHua](https://github.com/CTHua) & [Dark9ive](https://github.com/dark9ive).  

## Get started

Step 1. Clone the project to your own directory using the following command:

```
git clone https://github.com/CTHua/C.D_Judge.git
```

Step 2. Change directory into the cloned folder:

```
cd ./C.D_Judge
```

Step 3. Compile necessary files:

```
make
```

## Usage

### WARNING:   

__This project is NOT designed for general user and IS NOT EXPECTING ANY ONE EXCEPT DEVELOPERS TO EXECUTE!!__  
__Running these compiled executable files may CAUSE DAMAGE TO YOUR PERSONAL FILES!!__  
__SO MAKE SURE YOU KNOW WHAT YOU ARE DOING!!__  
__DO EVERYTHING AT YOUR OWN RISK!!__  

### Ganerate encrypted input/output files

You must encrypted your i/o file(s) with following commands:  

```
1keycrypt test_date(YYYYMMDD) num_of_question(s)
```

### Submit answers

Please make sure that you are in the same directory with your "main.c", then type:

```
/home1/student/stud108/s10829/judge/submit test_date(YYYYMMDD)
```

## Intro

This is a simple judge system. Only supports NCCU-ghost(ghost.cs.nccu.edu.tw) currently.  
Planned on making this a website version since we still need more SQL and HTML techniques.  

###	hash.h

__hash.h__ is a C++ source code using [crypt(1)](https://docs.oracle.com/cd/E19253-01/816-5165/crypt-1/index.html) and [MD5 package from OpenSSL](https://www.openssl.org/docs/man1.1.0/man3/MD5_Init.html).  

This file includes only one function, which can __make a hash__ by giving a char array, then return the hash in another char array.  
The Key is generated by the following process:

1. Get MD5 hash of the input string.  
2. Transform the 128-bit hash result into 16 characters(8 bits per character).  
3. Take the first 8 digits of the transformed characters as the encrypt key.  
4. If there is any null byte (0x00) in the key, change it to 0x01.  

### 1keycrypt
  
__1keycrypt__ is the C++ compiled executable of 1keycrypt. See further introduce [below](https://github.com/CTHua/C.D_Judge#cryptcpp).  

### crypt.cpp

__crypt.cpp__ is a C++ source code including [hash.h](https://github.com/CTHua/C.D_Judge#hashh).  
The program uses the date to generate a special key, which is used on __encrypting test files.__  

After the key is generated, the script will then encrypt the test data (input) and Answer (output) files using _crypt_ command.  
  
Although __crypt(1)__ is considered not secure enough, we still use it as our encrypt tool because of its convienience. Plus, the key is hard to be brute-forced since there are about 2<sup>64</sup> combinations in total, and the examinees may only know that the key has something to do with the date. Despite of that, we still planned to add a feature of letting the user to set their own password rather than bind it with the date.  

### submit

__submit__ is the C++ compiled executable of public\_judge. See further introduce [below](https://github.com/CTHua/C.D_Judge#public_judgecpp).

### public\_judge.cpp

__public\_judge.cpp__ is a C++ source code including [hash.h](https://github.com/CTHua/C.D_Judge#hashh).  
  
The judge will do these before grading your code:  

1. Make a ".judge" folder under your current directory.
2. Make a copy of your code into ./.judge and compile it.
3. Make a copy of your code to admins' folder.
4. record submit time

And then start the grading process:  

1. If fails to read the compiled executable, gives CE (Compilation Error).
2. Run the exectable. If runtime stays over 1 second, kill it with signal 9.
3. If the exit code is 137 (kill signal 9), gives TLE (Time Limit Exceed).
4. Other non-zero exit code, gives RE (Runtime Error).
5. Check if the encrypted output file is the same as the encrypted answer, gives AC (Accept).
6. Otherwise, gives WA (Wrong Answer).

The total score is calculated in the following formula:  

<p align="center"><img id="formula" src="https://github.com/CTHua/C.D_Judge/blob/master/pics/formula.png"></p>
  
For N equals to the total number of AC(s).  

Last but not least, clean the trash, show the results and send them to the admins.  

## Submission status

Please visit our [website](http://www.cs.nccu.edu.tw/~s10829/index.html) for current submission status.

## Planned feature(s)

 - Custom password for each encryption.
 - Website version(account create, identity verify, db management, etc...)
