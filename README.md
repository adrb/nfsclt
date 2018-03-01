
It's a simple user space NFS client. Currently supports only NFSv3,
but it has capacity to further NFSv4 implementation.

So how it happend that I made nfsclt?
Latelly just want to do some tests with nfssshell [1]. But as it turned out,
nfsshell is broken on many levels. Perhaps most horrific thing is nfsshell
handle copying functions, which just copy data to some random memory locations :)

And as I said, it's not the only problem there. Moreover nfsshell is obviously dead,
so no point in making patches. I just decided to start from scratch and make
new client inspired by nfsshell.

So there you have it - nfsclt

## Compilation

You may need to install some non-standard packages:

  - Debians: libreadline-dev libcap-dev
  - RedHats: readline-devel libcap-devel

```
$ make
```

## Usage:

```
# ./nfsclt
nfs> set host localhost
nfs> exports
Establishing new TCP connection... connected (127.0.0.1:1023 --> 127.0.0.1:48815)
/srv/nfs 127.0.0.1
nfs> mount /srv/nfs
nfs3 fh: (28) 01000700f5876e0000000000fffffffffffffffffffa427f5610093c
nfs> help
List of available commands printed below.
Use 'help command' to display detailed description

exports         mount           umount          ls              cd
lcd             lpwd            cat             get             put
rm              chmod           chown           mkdir           rmdir
mv              ln              mknod           stat            df
handle          set             help            ?               quit

nfs> help ls
ls      [-l] [PATH]

        Print current directory entries

        -l      print also file atributes
        PATH    optional path to directory

nfs>
```

Commands history is saved to .nfshistory file if it exists.

-- 
[1] https://github.com/NetDirect/nfsshell

