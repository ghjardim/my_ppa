# Editing a package
If you did something wrong while packaging and want to fix it, you can
easily unpack the package with:

```
mkdir /tmp/packaging/
cd /tmp/packaging/
mv <path/to/helloworld_1.0-1.deb> .
dpkg-deb -R helloworld_1.0-1.deb helloworld_1.0-2
```

Then edit `helloworld_1.0-1/DEBIAN/control` to change `-1` to `-2`,
updating the package revision.

Edit whatever more you want and repackage.

