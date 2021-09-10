



## Port Knocking

```console
for x in 7000 8000 9000; do nmap -Pn --host_timeout 201 --max-retries 0 -p $x x.x.x.x
```