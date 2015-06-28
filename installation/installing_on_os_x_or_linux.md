# Installing on OS X or Linux

Installing on OS X and Linux is pretty simple; after having all of the dependencies installed, building is as easy as:

```sh
$ mkdir build-orange && cd build-orange 
$ cmake ../orange
$ make all install
```

To test your installation, run `orange test` from the root Orange directory or one of its subdirectories (like the `build-orange` folder you're currently in). If everything goes well, all of the tests should run.