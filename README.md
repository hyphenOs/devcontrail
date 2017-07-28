# devcontrail
Inspired by devstack - A devstack like tool to deploy OpenContrail


## Why?

After taking a look at the OpenContrail code that is mainly distributed as [opencontrail-controller](https://github.com/Juniper/contrail-controller) and [opencontrail-vrouter](https://github.com/Juniper/contrail-controller), it is observed that, it's not trivial to deploy OpenContrail. While I believe it's a great Virtual Networking toolkit it does not support 'Works on My Laptop' feature trivially. This to me is a serious limitation to try out, experiment with OpenContrail.

Goal of this project is to make it easy. This is inspired `./stack.sh` from OpenStack DevStack.

## How?

A bit more about how OpenContrail is built - It uses a tool [repo](https://android.googlesource.com/tools/repo), which is a same tool used to build Android. As OpenContrail components are built from different git repositories, there needs to be a mechanism for managing this. The tool `repo` is precisely meant for things like this.

In the OpenContrail documentation, this is not very obvious and a lot of this happens under the hood. We will probably leverage this tool, by writing our own `manifest` file. Our focus will be to start with minimum manifest file and then add components only as needed. We would run this insided a Docker container,so it should be possible for anyone to be able to non-destructively build OpenContrail on their own machine.

OpenContrail makes use of [SCons](http://www.scons.org) tool to build. So this works as follows - at a high level. The repository [opencontrail-build](https://github.com/Juniper/contrail-build) contains the SConstruct file. Through the `repo` tool above, all the required directories are downloaded in the build sandbox and then using scons, the build is fired.

Also, the focus of this is going to be getting individual nodes up in OpenContrail System, so first start with vRouter node (Compute Node Part) and later the controller nodes.

