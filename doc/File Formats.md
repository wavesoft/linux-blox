
# `.blox` file

The `.blox` file is a software package block. Each `.blox` is a directory with the folowing structure:

    <package>.blox/
    |-- package.json
    |-- contents/
    |   |-- bin/
    |   |-- lib/
    |   |-- etc/
    |   |-- var/
    |   `-- man/
    |-- services/
    |   |-- <service>/
    |  ...  |-- hooks/
    |       |   |-- on_setup
    |       |   |-- on_start
    |       |   |-- on_stop
    |       |   |-- on_check
    `-- hooks/
        |-- on_register
        |-- on_unregister
        |-- on_test
        `-- on_check

## `package.json` file

This json configuration contains the information required for identifying the package and it's dependencies. It's structure is the following:

```json
{
    /* Basic package information */
    "name": "Package_Name",
    "version": "X.X.X.XXXX",
    /* Visual information/package details */
    "about": {
        "displayName": "Human-Readable Name",
        "description": "Human-Readable short description",
        "author": "Package author",
        "website": "Package website"
    },
    /* Components imported by other blocks */
    "imports": {
        /* Package imports */
        "package": [
            "[package]",
            "[package]=[version]",
            "[package]>=[version]",
            "[package]<=[version]"
        ],
        /* Service imports */
        "service": [
            "[service]": {
                [configuration matching],
                ...
            }
            "[service]=[version]": { .. },
            "[service]>=[version]": { .. },
            "[service]<=[version]": { .. },
        ],
    },
    /* Components exported by this block */
    "exports": {
        /* Service exports */
        "service": {
            "[service]": {
                "version": "X.X.X.XXXX"
            }
        }
    }
}
```

# `.state` file

The `.state` file contains the configuration parameters for a `.blox` file. The directory structure inside the `.state` file is the following:

    <package>.state
    |-- info.json
    |-- contents
    |   |-- etc
    |   |-- var
    |   |-- tmp

