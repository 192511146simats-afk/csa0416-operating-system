Linux Permission:

r = Read
w = Write
x = Execute

Users:
u = Owner
g = Group
o = Others

Example:
-rwxr-xr--

Owner  → rwx
Group  → r-x
Others → r--

Numeric:
r = 4
w = 2
x = 1

rwx = 7
r-x = 5
r-- = 4

Example:
chmod 754 file.txt
