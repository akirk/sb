# sb
Utility to quickly sandbox and unsandbox a host.

# Demo

```
~ ❯ sb
No hosts currently sandboxed.
Usage sb [option] <host> ...

	<host>             toggle specified host (set to 1.2.3.4)
	add <host> <ip>    add the specified host (set to 1.2.3.4 or to <ip>)
	rm <host>          remove the specified host

	activate <host>    activate (or add) the specified host (set to 1.2.3.4)
	deactivate <host>  deactivate specified host

You can use paritial hostnames to match multiple entries.
~ ❯ sb demo
demo does not exist. Shall we point it to 1.2.3.4 (y/n)? y
added: 1.2.3.4 demo
~ ❯ sb
Active hosts
============
demo
~ ❯ sb demo
deactivated: 1.2.3.4 demo
~ ❯ sb
No hosts currently sandboxed.
~ ❯ sb hello
hello does not exist. Shall we point it to 1.2.3.4 (y/n)? y
added: 1.2.3.4 hello
~ ❯ sb demo
activated: 1.2.3.4 demo
~ ❯ sb
Active hosts
============
demo
hello
~ ❯ sb
Active hosts
============
demo
hello
~ ❯ sb hel
deactivated: 1.2.3.4 hello
~ ❯ sb
Active hosts
============
demo
~ ❯ 
```
