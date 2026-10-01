# 10-тарау: execve(), exec() отбасы, fork(), wait()

Методичкадағы барлық листингтер (10.4 – 10.18) осы папкада. Терминалда былай орындалады:

> **macOS ескертпесі.** Методичка Linux-қа арналған. Mac-та жұмыс істеуі үшін осы папкадағы кодқа үш өзгеріс енгізілген (Linux-та да бірдей жұмыс істейді): `execve1.c` ішінде `/bin/uname` орнына `/usr/bin/uname` (Mac-та `uname` тек `/usr/bin`-де), ал `lsstatus.c` мен `killedchild.c` ішінде `<wait.h>` орнына `<sys/wait.h>` (Darwin-да `wait.h` жоқ).

```bash
cd lab10

# Листинг 10.4 — execve1.c: uname -a іске қосу
gcc -o execve1 execve1.c
./execve1

# Листинг 10.5–10.7 — execve2.c + newprog.c + Makefile
make
./execve2

# Листинг 10.8 — execve3.c: бос ортамен env (ештеңе шығармайды — орта бос)
gcc -o execve3 execve3.c
./execve3

# Листинг 10.9 — forkexec1.c: fork() + execve()
gcc -o forkexec1 forkexec1.c
./forkexec1
ps          # 5 секунд ішінде sleep процесі көрінеді

# Листинг 10.10 — execvels.c: fork() + execve("/bin/ls")
gcc -o execvels execvels.c
./execvels

# Листинг 10.11 — execlls.c: execl()
gcc -o execlls execlls.c
./execlls

# Листинг 10.12 — execlels.c: execle() (ортаны беру)
gcc -o execlels execlels.c
./execlels

# Листинг 10.16 — lsroot.c: execlp() (PATH бойынша іздеу)
gcc -o lsroot lsroot.c
./lsroot

# Листинг 10.17 — lsstatus.c: wait() + WIFEXITED / WEXITSTATUS
gcc -o lsstatus lsstatus.c
./lsstatus .              # code=0
./lsstatus abrakadabra    # code=2

# Листинг 10.18 — killedchild.c: WIFSIGNALED
gcc -o killedchild killedchild.c
./killedchild &
ps                        # sleep процесінің PID-ін қара
kill <PID_sleep>          # -> Process with PID=... has exited with signal.
# егер kill жасамай 30 с күтсе -> ... has exited with code=0
```

Тазалау: `make clean` (execve2 және newprog) немесе `rm -f execve1 execve3 forkexec1 execvels execlls execlels lsroot lsstatus killedchild`.
