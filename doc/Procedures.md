
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

### 4. Collect tree configuration

By reading all the `package.json` files from every package in the dependency tree.

 * Update `PATH` and `LD_LIBRARY_PATH` environment variables in order to include the binary and library files from the package. Optionally update the appropriate variables for python, perl and other utilities.
 * Create a copy-on-write 


(Document in progress)
