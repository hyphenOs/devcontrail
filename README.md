# devcontrail
Inspired by devstack - A devstack like tool to deploy OpenContrail


## Why?

After taking a look at the OpenContrail code that is mainly distributed as [opencontrail-controller](https://github.com/Juniper/contrail-controller) and [opencontrail-vrouter](https://github.com/Juniper/contrail-controller), it is observed that, it's not trivial to deploy OpenContrail. While I believe it's a great Virtual Networking toolkit it does not support 'Works on My Laptop' feature trivially. This to me is a serious limitation to try out, experiment with OpenContrail.

Goal of this project is to make it easy. This is inspired `./stack.sh` from OpenStack DevStack. There actually exists a repository called [contrail-installer](https://github.com/Juniper/contrail-installer), which does something exactly identical, hence there is no point in duplicating the effort. What I am instead going to do is - fork that repository and fix issues in that repository, because likely someone would have tested that.

## How?

We will just fix the above repo, to make it 'really' possible to work with `./contrail.sh`. We'll first try to support Ubuntu 16.04 as the previous versions look like supported in the original.

Also, the focus of this is going to be getting individual nodes up in OpenContrail System, so first start with vRouter node (Compute Node Part) and later the controller nodes.

Look at NOTES.md for the current approach (this more likely going to get shelved).


~A bit more about how OpenContrail is built - It uses a tool [repo](https://android.googlesource.com/tools/repo), which is a same tool used to build Android. As OpenContrail components are built from different git repositories, there needs to be a mechanism for managing this. The tool `repo` is precisely meant for things like this.~

~In the OpenContrail documentation, this is not very obvious and a lot of this happens under the hood. Initially, the idea was to start with writing `manifest` files for the repo utility, but instead, trying with 'git submodule' that's probably a right choice here. What we are going to do is - create our branch `devcontrail` (branching off from master and periodically merging). Initially we'd only update the SConscript, later on we can decide what course to take.~

~To start with, we are creating directory structure like the ['build system'](https://github.com/Juniper/contrail-vnc).~

~OpenContrail makes use of [SCons](http://www.scons.org) tool to build. So this works as follows - at a high level. The repository [opencontrail-build](https://github.com/Juniper/contrail-build) contains the SConstruct file. Through the `repo` tool above, all the required directories are downloaded in the build sandbox and then using scons, the build is fired.~


