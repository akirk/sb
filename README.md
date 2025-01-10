# sb
Utility to quickly sandbox and unsandbox a host.

# Demo

```
~ ❯ sb
No hosts currently sandboxed.
Usage sb <command> <host> ...

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

# Autocomplete

You can add this to your ``.zshrc` file to get autocompletion support in ZSH:

```zsh
_sbc() {
	local -a _descriptions _values hosts=() inactive_hosts=() hostname
	hosts=($(awk '/^([0-9]{1,3})[.]([0-9]{1,3})[.]([0-9]{1,3})[.]([0-9]{1,3}) *([^ ]+)/ {print $2 "_" $3}' /etc/hosts))
	inactive_hosts=($(awk '/^# *([0-9]{1,3})[.]([0-9]{1,3})[.]([0-9]{1,3})[.]([0-9]{1,3}) *([^ ]+)/ {print $3 "_" $4}' /etc/hosts))

	for host in "${inactive_hosts[@]}"; do
		hostname=$(echo $host | cut -d_ -f1)
		_values+=("$hostname")
		host=$(echo "$host" | tr _ ' ')
		_descriptions+=($'\033[31m'$host$'\033[0m-- disabled')
	done

	for host in "${hosts[@]}"; do
		hostname=$(echo $host | cut -d_ -f1)
		_values+=("$hostname")
		host=$(echo "$host" | tr _ ' ')
		_descriptions+=($'\033[32m'$host$'\033[0m-- enabled')
	done

	compadd -l -d _descriptions -a _values
}
compdef _sbc sb
```
