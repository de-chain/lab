[Rclone official site](https://rclone.org/)  
Rclone is a command-line program to manage files on cloud storage. It is a feature-rich alternative to cloud vendors' web storage interfaces.<br>
Users call rclone "The Swiss army knife of cloud storage".

Rclone really looks after your data. It preserves timestamps and verifies checksums at all times. Transfers over limited bandwidth; intermittent connections, or subject to quota can be restarted, from the last good file transferred. You can check the integrity of your files. Where possible, rclone employs server-side transfers to minimise local bandwidth use and transfers from one provider to another without using local disk.

Virtual backends wrap local and cloud file systems to apply encryption, compression, chunking, hashing and joining.

Rclone mounts any local, cloud or virtual filesystem as a disk on Windows, macOS, linux and FreeBSD, and also serves these over SFTP, HTTP, WebDAV, FTP and DLNA.
[Rclone drive](https://rclone.org/drive/)

[own  Drive id](https://rclone.org/drive/#making-your-own-client-id)

## Comandi rclone

   1.`rclone config`<br>
Current remotes:

Name                 Type<br>
====                 ====<br>
gdrivef10            drive

e) Edit existing remote  
n) New remote  
d) Delete remote  
r) Rename remote  
c) Copy remote  
s) Set configuration password  
q) Quit config  
e/n/d/r/c/s/q> d

Select remote.  
Choose a number from below, or type in an existing value.  
 1 > gdrivef10  
remote> 1

  2. `rclone listremotes`
  3. `rclone ls <mydrive:>` lista di tutti i file  
  4. `rclone lsd <mydrive:>`
  5. `rclone about gdrivef10:`
  6. montare cartella mydrive  
  `sudo apt install fuse`  
  `rclone mount mydrive: ~/mydrive --daemon`  
  daemon monta cartella in background
  Variabili>  
    * `rclone mount mydrive: ~/mydrive --vfs-cache-mode full` migliora velocit' di caching  
    * `rclone mount mydrive: ~/mydrive --vfs-cache-mode full --daemon`
   7. `fusermount -u ~/mydrive` smontare filesystem






 