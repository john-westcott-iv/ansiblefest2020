## Downloading AWX

To start, we will look at the layout of the collection. The code for the collection is housed alongside the AWX code. We will begin by cloning the AWX GitHub repository into our current directly with the commands:

```
[student1@ansible-1 ~]$ cd ~
[student1@ansible-1 ~]$ git clone https://github.com/ansible/awx.git
Cloning into 'awx'...
remote: Enumerating objects: 253666, done.
remote: Total 253666 (delta 0), reused 0 (delta 0), pack-reused 253666
Receiving objects: 100% (253666/253666), 230.27 MiB | 46.20 MiB/s, done.
Resolving deltas: 100% (195893/195893), done.
```

It will take a moment to clone this repository to your workstation for the first time. When the cloning is done, you will have an `awx` folder in your home directory. Enter that directory with the command:

```
[student1@ansible-1 ~]$ cd awx
[student1@ansible-1 awx]$ ls
```

You will see many files and directories in the source code. For the purposes of this lab the two important ones will be the Makefile and the `awx_collection` directory. The Makefile will allow us to run make commands to do things like install and test the collection; we will use this in the next section to install the development version of the collection. The `awx_collection` is the root of the collections source code and will be discussed after we install the `devel` version of the collection.
