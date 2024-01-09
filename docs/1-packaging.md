# Simple packaging tutorial
This is a simple packaging tutorial that I've found in
https://ubuntuforums.org/showthread.php?t=910717 .

## Download the program
The first step consists in downloading the git repository for your
program. Just do
```
git clone <repo-uri>
```

Figure out the version of the software you want to package.

## Set up packaging environment

Then do `mkdir -p /tmp/packaging/<project>_<major version>.<minor
version>-<package revision>`.

For example, in this tutorial it could be `helloworld_1.0-1`.

## Compile the program
Compile with:
```
make install DESTDIR=/tmp/packaging/helloworld_1.0-1
```

Make sure that it doesn't go to `usr/local/`. If so, move everything to
`usr/`. For example:

```
/tmp/packaging/helloworld_1.0-1/usr/local/bin/helloworld #wrong!
/tmp/packaging/helloworld_1.0-1/usr/bin/helloworld #right!
```

This `usr` directory may have directories like `bin`,
`share/doc/helloworld`, `share/man/man1`.

## Create package metadata
Then create:
```
mkdir /tmp/packaging/helloworld_1.0-1/DEBIAN/
```

This directory will contain a file called `control`, with information
such as:
```
Package: helloworld
Version: 1.0-1
Section: base
Priority: optional
Architecture: i386
Depends: libsomethingorrather (>= 1.2.13), anotherDependency (>= 1.2.6)
Maintainer: Your Name <you@email.com>
Description: Hello World
 When you need some sunshine, just run this
 small program!
 
 (the space before each line in the description is important)
```

## Build the package
Go one directory above and run:
```
dpkg-deb --build helloworld_1.0-1
```

This will create the package.
