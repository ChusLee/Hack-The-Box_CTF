<img width="856" height="372" alt="image" src="https://github.com/user-attachments/assets/d368d1ab-55bb-4f79-afcc-7a9bbfac8df2" />



# Scope

Planning is a Linux machine that involves web enumeration, subdomain fuzzing, and exploitation of a vulnerable Grafana instance (CVE-2024-9264).
After gaining initial access to a Docker container, an exposed password allows lateral movement to the host system due to password reuse.
Finally, a custom Crontab UI management application running with root privileges can be leveraged to achieve full system compromise.

# Index
- [Enumeration](Enumeration.md)
- [Fuzzing](Fuzzing.md)