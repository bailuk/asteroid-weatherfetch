# AsteroidOS Weather Fetch App

This app uses an internet connection from the watch to fetch weather forecast data to be used for the Weather app in [AsteroidOS](http://asteroidos.org/)

## GUI version

The GUI version allows the user to directly enter locations on the watch or manipulate the order by drag-and-drop.

![Screenshot 1](./screenshot20250131_145414.jpg)

The rest of the GUI screen looks like this:

![Screenshot 2](./screenshot20250131_145515.jpg)

## Command-line version

There is also a command-line version called `weatherfetch_cli` which is intended to be used from a command line.  On the watch command line as the `ceres` user, one can run the command with no arguments to fetch the weather forecast for the previously configured location.

If the user would like to temporarily add a new location and fetch weather for that location:

```
weatherfetch_cli -cl --add 50.812375,4.380734,"Université libre de Bruxelles"
```

In the following, TOL means Top-Of-List and BOL means Bottom-Of-List.  These refer to the saved location list.  Here are the possible commands


| Short   | Long      | Args          | Description
|---------|-----------|---------------|-----------------------------------------------
| -a      | --add     | lat,lng,name  | add the location to top of list (TOL)
| -c      | --config  |               | manipulate the list but don't fetch weather
| -d      | --delete  |               | delete bottom of list (BOL)
| -l      | --list    |               | list all current locations
| -r      | --rotate  |               | rotate the list to put TOL at BOL

These should always execute in the order `rotate`, `delete`, `add`, `list`, `config` no matter their order on the command line. The (admittedly weak) reasoning for this order is that one can do simple testing with something like this:

```bash
weatherfetch_cli -rdlc --add 50.812375,4.380734,"Université libre de Bruxelles"
```

And the effect is that each time it is run, it will rotate the top entry to the bottom, delete it, add the new entry to the top, and then list the result, all without actually fetching the weather (that's the -c) and annoying or abusing that service during testing.

## Build

The preferred method to build and install this software is to use `bitbake` or `devtool`.  See https://wiki.asteroidos.org/index.php/OpenEmbedded for detailed information on how to do this.
