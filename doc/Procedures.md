
# Procedures

In this document I am going to describe all the usual procedures someone performs in a classic linux distribution, and how they are orchestrated in a *LinuxBlox* distribution.

## Running an application

Let's take the example of a simple linux service, for example `ntpd`.

While trying to start the application, the *LinuxBlox* framework is going to execute the following operations:

### 1. Download package if missing

Since every package is well-defined, the framework will try and locate the specified blox. Either from the local repositories or from the on-line repositories. By the end of this process, the framework is going to download and place the blox in the appropriate directory.

In our case, since we haven't specified a version for the ntpd package, it's going to download the latest version (let's say `4.2.6p5`). The file will be placed in `/blox/ntpd-4.2.6p5.blox`.

### 2. Validate package integrity

According to the appropriate restrictions of every package, the framework is going to check wheter or not the environment and the application can run without any issues.

This involves checking for binary compatibility, checks against tampered binary or confiuration files, checks for network configuration etc.

### 3. Build dependency tree

The framework will read the `/imports/packages` section from the `package.json` of the `ntpd-4.2.6p5.blox` and for every package try to:

 * Download package if it's missing
 * Validate integrity of the package
 * Store the package in a dependency tree in memory

### 4. Collect environment configuration

Collect the different kind of `environments` that we will have to satisfy in order to complete the dependency resolution, and initialize the resolution subsystem for each one of them. For example:

 * __binary__ environment provides system-wide binaries. In order to satisfy this environment you will need to append in the `PATH` environment variable the path to the folder that contains the binaries.
 * __library__ environment provides system-wide libraries. In a simmilar manner with the binary environment, you just have to append the library directory in the `LD_LIBRARY_PATH` environment variable.
 * __py-lib__ environment provides a library for the python interpreter. The environment variable that should be updated is `PYTHONPATH`.
 * __perl-lib__ enviromnent provides a library for the perl interpreter. The environment variable that should be updated is `PERLLIB`.

### 5. 

By reading all the `package.json` files from every package in the dependency tree.

 * Update `PATH` and `LD_LIBRARY_PATH` environment variables in order to include the binary and library files from the package. Optionally update the appropriate variables for python, perl and other utilities.
 * Create a copy-on-write 

(Document in progress)
