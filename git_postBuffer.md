## `git push` got error message <br><br>

```diff
- git push
```

```diff
! Enumerating objects: 18, done.
! Counting objects: 100% (18/18), done.
! Delta compression using up to 4 threads
! Compressing objects: 100% (12/12), done.
! error: RPC failed; HTTP 400 curl 22 The requested URL returned error: 400
! send-pack: unexpected disconnect while reading sideband packet
! Writing objects: 100% (13/13), 2.92 MiB | 5.28 MiB/s, done.
! Total 13 (delta 7), reused 0 (delta 0), pack-reused 0 (from 0)
! fatal: the remote end hung up unexpectedly
! Everything up-to-date
```
### The Issue
The default maximum size of the buffer used when sending data to a remote Git repository over HTTP(S) is 1 MB (1048576 bytes), it was controled by the `http.postBuffer`
 setting. So if your push includes large files, Git may reject the request.<br>

### FIX
```diff
+ git config --global http.postBuffer 52428800 
```
<br>
This will set the buffer size to 50MB and fix the issue.
