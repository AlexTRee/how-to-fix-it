- Error in **if (nzchar(SHLIB_LIBADD)) SHLIB_LIBADD else character() : argument is of length zero**

> This happens mostly with vitualenv or with conda, the issue is /home/$user/.conda/lib/R/etc/Makeconf is empty.
```
Fix:

cp /home/$user/.conda/pkgs/r-base-3.6.1-hce969dd_0/lib/R/etc/Makeconf /home/$user/.conda/lib/R/etc/Makeconf
```
