# Build PineTime Firmware in the Cloud with GitHub Actions

![PineTime Firmware Programming vs Fortnite](https://lupyuen.github.io/images/cloud-title.jpg)

Programming the firmware of our gadgets (like [__PineTime Smart Watch__](https://wiki.pine64.org/index.php/PineTime)) has always been cumbersome...

1. Get a proper computer _(Windows tends to be problematic)_

1. Install the right tools and libraries to cross-compile our firmware _(Depends on our operating system)_

1. If the build fails, tweak the build scripts _(It's probably just Windows)_

1. If the build still fails... __We're stuck!__ _(Good Luck!)_

Nowhere as fun as a game like Fortnite!

_Can Firmware Programming be as fun as Fortnite?_

Well Fortnite runs in the Cloud on massive servers...

_Can we build our firmware in the Cloud?_

_In under 2 minutes?_

_Without any computer setup!_

Yes we can!

Today we'll learn [__GitHub Actions__](https://github.com/features/actions) for building [__FreeRTOS Firmware__](https://github.com/JF002/Pinetime) for [__PineTime Smart Watch__](https://wiki.pine64.org/index.php/PineTime) in the GitHub Cloud.

It's __Fully Automated__...

1. __Check in our updated source files__ to GitHub

1. Wait __2 Minutes__

1. Out comes a piping-hot __New Firmware Image__ for testing on PineTime!

_(Feels like a Microwave!)_

We'll make PineTime Programming as enjoyable as Fortnite... But less violent... And in 3D!

# Create a Fork of PineTime Source Files

_(Nope no spoon!)_

1.  __Create a free GitHub Account__ if we haven't got one...

    ▶️ &nbsp; [`github.com`](https://github.com/)

1.  __Browse to the GitHub Repository__ for the PineTime Firmware...

    ▶️ &nbsp; [`github.com/JF002/Pinetime`](https://github.com/JF002/Pinetime)

    Here's the complete Source Code for the FreeRTOS PineTime Firmware.

1.  Click the `Fork` button at top right...

    ![Create a fork](https://lupyuen.github.io/images/cloud-fork.png)

1.  This creates a __Fork__ of the PineTime Repository under our GitHub Account...

    ![Created the fork](https://lupyuen.github.io/images/cloud-fork2.png)

    The URL looks like this...
    
    ```
    https://github.com/ACCOUNT_NAME/Pinetime
    ```

1.  The Fork contains __our own copy__ of the entire Source Code for the PineTime Firmware... Ready for us to make any updates!

    GitHub helpfully __tracks updates to our Fork,__ so that one day we may submit a __Pull Request__ to sync our updates (only the useful ones) back to the original PineTime Repository.

    And we may also __Pull Updates__ from the original PineTime Repository and apply them to our Fork.

    That's how we maintain Open Source Projects!

Read on to learn how we add GitHub Actions to our Fork to build the firmware automagically...

# Add GitHub Actions to our Fork

1.  In our Fork on GitHub, click `Actions`

    ![GitHub Actions](https://lupyuen.github.io/images/cloud-actions.png)

1.  Click `Skip this and set up a workflow yourself`

    ![GitHub Actions](https://lupyuen.github.io/images/cloud-actions2.png)

1.  GitHub brings us to a page to edit `.github/workflows/main.yml`

    ![GitHub Actions](https://lupyuen.github.io/images/cloud-actions3.png)

1.  Open a new web browser tab. 

    Browse to this page...

    [`github.com/pinetime-lab/.github/workflows/main.yml`](https://raw.githubusercontent.com/lupyuen/pinetime-lab/master/.github/workflows/main.yml)
    
    Copy the contents of this page. 

1.  Switch back to the earlier page: `.github/workflows/main.yml`

    Paste and overwrite the contents of the file...

    ![GitHub Actions](https://lupyuen.github.io/images/cloud-actions4.png)

1.  Scroll to the bottom of the page.

    Click `Start Commit`

    ![GitHub Actions](https://lupyuen.github.io/images/cloud-actions5.png)

1.  Click `Commit New File`

    ![GitHub Actions](https://lupyuen.github.io/images/cloud-actions6.png)

We have just created a __Workflow__... An automated job that will be run by GitHub whenever we update our source files.

If we ever need to edit the Workflow, just browse to this URL...

```
https://github.com/ACCOUNT_NAME/Pinetime/blob/master/.github/workflows/main.yml
```

(Change `ACCOUNT_NAME` to our GitHub Account Name)

Let's change a PineTime source file... And trigger our very first PineTime Firmware Build in the Cloud!

# Modify the PineTime Source Code

We shall modify the source code so that the PineTime Watch Face shows our own special message...

1.  Browse to this URL...

    ```
    https://github.com/ACCOUNT_NAME/Pinetime/blob/master/src/DisplayApp/Screens/Clock.cpp
    ```

    (Change `ACCOUNT_NAME` to our GitHub Account Name)

1.  Click the `Edit` icon at the right...

    ![Edit Source File](https://lupyuen.github.io/images/cloud-edit.png)

1.  Look for the line with `"BPM"` (line 71)...

    ![Edit Source File](https://lupyuen.github.io/images/cloud-edit2.png)

1.  `BPM` is the text that's displayed on the PineTime Watch Face.

    Change `BPM` to our own short message, like `LOVE`...

    ![Edit Source File](https://lupyuen.github.io/images/cloud-edit3.png)

1.  Scroll to the bottom of the page.

    Click `Commit Changes`

    ![Edit Source File](https://lupyuen.github.io/images/cloud-edit4.png)

Guess what?

We have just triggered __Our Very First PineTime Firmware Build In The Cloud!__

(Because the Firmware Build is triggered by any file update)

Let's check the result of our Firmware Build in the Cloud...

# Our First PineTime Firmware Build

1.  Click `Actions` at the top.

    Click the first row that appears: `Update Clock.cpp`

    ![Build Result](https://lupyuen.github.io/images/cloud-result.png)

1.  Click `build` at left...

    ![Build Result](https://lupyuen.github.io/images/cloud-result2.png)

1.  We'll see each step of the firmware building process...

    ![Build Result](https://lupyuen.github.io/images/cloud-result3.png)

1.  Click `Make`

    This shows the messages that were generated by the cross-compiler...

    ![Build Result](https://lupyuen.github.io/images/cloud-result4.png)

If we see this error...

```
/home/runner/work/Pinetime/Pinetime/src/drivers/TwiMaster.cpp:1:10: fatal error: sdk/integration/nrfx/nrfx_log.h: No such file or directory
 #include <sdk/integration/nrfx/nrfx_log.h>
          ^~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
compilation terminated.
make[3]: *** [src/CMakeFiles/pinetime-app.dir/drivers/TwiMaster.cpp.o] Error 1
```

Browse to...

```
https://github.com/ACCOUNT_NAME/Pinetime/blob/master/src/drivers/TwiMaster.cpp
```

(Change `ACCOUNT_NAME` to our GitHub Account Name)

Edit the first two lines...

```c
#include <sdk/integration/nrfx/nrfx_log.h>
#include <sdk/modules/nrfx/hal/nrf_gpio.h>
```

To...

```c
#include <nrfx_log.h>
#include <nrf_gpio.h>
```

Click `Commit Changes` to save the file.

This triggers a new Firmware Build, which should succeed now.

# Download and Test Our PineTime Firmware

Now let's download and flash the new firmware to PineTime!

1.  Click `Artifacts` at the top.

    Click `pinetime-app.out`

    ![Build Artifact](https://lupyuen.github.io/images/cloud-artifact.png)

1.  Our web browser will download a ZIP file.

    Extract the PineTime Firmware Image inside: `pinetime-app.out`

1.  Flash `pinetime-app.out` to our PineTime with [__xPack OpenOCD__](https://xpack.github.io/openocd/)

    __File Format:__ ELF

    __Flash Address:__ `0x0`

TODO: How to flash firmware with xPack OpenOCD

_Why is the firmware 6.4 MB in size when the build log shows that the cross-compiler output (`text`) is 238 KB?_

Because `pinetime-app.out` is an [__ELF File__](https://en.wikipedia.org/wiki/Executable_and_Linkable_Format). It contains the firmware image as well as the debugging symbols.

(Useful for a debugger like GDB)

_I have a request..._

If you could... With your kind permission... Please post to Twitter and/or Mastodon a pic of your PineTime with the new firmware.

Tag the post with `#PineTime` so we know that building PineTime Firmware in the Cloud works OK for you. Thanks! :-)

![PineTime shows some LOVE](https://lupyuen.github.io/images/cloud-love.jpg)

_PineTime shows some LOVE_

# How It Works

Let's look at the GitHub Actions Workflow we used for building PineTime Firmware: [`.github/workflows/main.yml`](https://github.com/lupyuen/pinetime-lab/blob/master/.github/workflows/main.yml)

```yaml
# GitHub Actions Workflow to build FreeRTOS Firmware for PineTime Smart Watch
# Based on https://github.com/JF002/Pinetime/blob/master/doc/buildAndProgram.md

# Name of this Workflow
name: Build PineTime Firmware

# When to run this Workflow...
on:

  # Run this Workflow when files are updated (Pushed) in the "master" Branch
  push:
    branches: [ master ]
    
  # Also run this Workflow when a Pull Request is created or updated in the "master" Branch
  pull_request:
    branches: [ master ]
```

Here we see the conditions that will trigger our Workflow...

1. When files are __updated (or Pushed)__ in the `master` Branch

1. When a __Pull Request is created or updated__ in the `master` Branch

[More details](https://docs.github.com/en/actions/reference/events-that-trigger-workflows#pull_request)

Next we specify which Operating System GitHub should use to execute the Workflow Steps...

```yaml
# Steps to run for the Workflow
jobs:
  build:

    # Run these steps on Ubuntu
    runs-on: ubuntu-latest

    steps:
      ...
```

This asks GitHub to allocate a free Virtual Machine to build our firmware, based on Ubuntu 18.04.

We're using Ubuntu, but GitHub supports Windows and macOS as well.

[More details](https://docs.github.com/en/actions/reference/virtual-environments-for-github-hosted-runners)

After that we specify the steps to be executed for our Workflow...

## Install `cmake`

The steps for building PineTime Firmware are based on [this doc](https://github.com/JF002/Pinetime/blob/master/doc/buildAndProgram.md).

We use a popular tool called [`cmake`](https://cmake.org/). (It's like an evolved `make`)

Here's how we install `cmake`...

```yaml
    - name: Install cmake
      uses: lukka/get-cmake@v3.18.0
```

_Why do we need to install build tools like `cmake`?_

Because GitHub only provides bare bones Ubuntu with simple command-line tools like `make`.

For special tools like `cmake`, we'll have to install ourselves.

_What's `get-cmake`?_

That's a GitHub Action provided by the community for [installing `cmake`](https://github.com/marketplace/actions/get-cmake)

[Browse the available GitHub Actions](https://github.com/marketplace?type=actions)

## Check Cache for Embedded Arm Toolchain

Our Ubuntu Virtual Machine in the GitHub Cloud is based on the Intel x64 platform... But we're building firmware for PineTime, which is based on Arm Cortex-M4.

To do that, we need to install a cross-compiler: [__Embedded Arm Toolchain__](https://developer.arm.com/tools-and-software/open-source-software/developer-tools/gnu-toolchain/gnu-rm) `arm-none-eabi-gcc`

We'll install this in the next step, but first we check whether the toolchain is in our cache...

```yaml
    - name: Check cache for Embedded Arm Toolchain arm-none-eabi-gcc
      id:   cache-toolchain
      uses: actions/cache@v2
      env:
        cache-name: cache-toolchain
      with:
        path: ${{ runner.temp }}/arm-none-eabi
        key:  ${{ runner.os }}-build-${{ env.cache-name }}
        restore-keys: ${{ runner.os }}-build-${{ env.cache-name }}
```

_Why cache the Embedded Arm Toolchain?_

The [Embedded Arm Toolchain](https://developer.arm.com/-/media/Files/downloads/gnu-rm/8-2019q3/RC1.1/gcc-arm-none-eabi-8-2019-q3-update-linux.tar.bz2) is a huge 102 MB download (compressed).

Every time GitHub builds our firmware, it creates a fresh new empty Virtual Machine.

(So that our firmware builds may be reproduced consistently... And for security too)

GitHub will take roughly a minute to download and unpack the toolchain... Unless we cache it.

```yaml
    - name: Check cache for Embedded Arm Toolchain arm-none-eabi-gcc
      id:   cache-toolchain
      uses: actions/cache@v2
```

The [`actions/cache`](https://docs.github.com/en/actions/configuring-and-managing-workflows/caching-dependencies-to-speed-up-workflows) GitHub Action lets us cache the toolchain for future builds.

We can have multiple caches. Here's our cache for the toolchain...

```yaml
      env:
        cache-name: cache-toolchain
```

Next we tell GitHub what to cache...

```yaml
      with:
        path: ${{ runner.temp }}/arm-none-eabi
        key:  ${{ runner.os }}-build-${{ env.cache-name }}
        restore-keys: ${{ runner.os }}-build-${{ env.cache-name }}
```

Given these build settings...

```bash
runner.temp    = /home/runner/work/_temp
runner.os      = Linux
env.cache-name = cache-toolchain
```

This means...

-  GitHub shall cache the temporary toolchain folder `/home/runner/work/_temp/arm-none-eabi`

    (We'll download the toolchain to this folder in the next step)

- The unique key for our toolchain cache shall be `Linux-build-cache-toolchain`

- In future builds, GitHub shall attempt to restore the cache for `Linux-build-cache-toolchain` into our toolchain folder `/home/runner/work/_temp/arm-none-eabi`

## Install Embedded Arm Toolchain

Now we download and unpack the Embedded Arm Toolchain into the temporary toolchain folder `/home/runner/work/_temp/arm-none-eabi`...

```yaml
    - name: Install Embedded Arm Toolchain arm-none-eabi-gcc
      if:   steps.cache-toolchain.outputs.cache-hit != 'true'  # Install toolchain if not found in cache
      uses: fiam/arm-none-eabi-gcc@v1.0.2
      with:
        # GNU Embedded Toolchain for Arm release name, in the V-YYYY-qZ format (e.g. "9-2019-q4")
        release: 8-2019-q3
        # Directory to unpack GCC to. Defaults to a temporary directory.
        directory: ${{ runner.temp }}/arm-none-eabi
```

We use the community GitHub Action [`fiam/arm-none-eabi-gcc`](https://github.com/marketplace/actions/arm-none-eabi-gcc) to do this. So easy!

_Why is there a condition for the step?_

```yaml
      # Install toolchain if not found in cache
      if:   steps.cache-toolchain.outputs.cache-hit != 'true'
```

This says that GitHub shall download the toolchain only if the previous step `cache-toolchain` couldn't find an existing cache for the toolchain.

Huge downloads and reinstallation averted... So neat!

## Check Cache for nRF5 SDK

```yaml
    - name: Check cache for nRF5 SDK
      id:   cache-nrf5sdk
      uses: actions/cache@v2
      env:
        cache-name: cache-nrf5sdk
      with:
        path: ${{ runner.temp }}/nrf5_sdk
        key:  ${{ runner.os }}-build-${{ env.cache-name }}
        restore-keys: ${{ runner.os }}-build-${{ env.cache-name }}
```

TODO

## Install nRF5 SDK

_Can we download and install packages into the GitHub Virtual Machine without using a GitHub Action?_

Yes we can, through the Ubuntu command line...

```yaml
    - name: Install nRF5 SDK
      if:   steps.cache-nrf5sdk.outputs.cache-hit != 'true'  # Install SDK if not found in cache
      run:  cd ${{ runner.temp }} && curl https://developer.nordicsemi.com/nRF5_SDK/nRF5_SDK_v15.x.x/nRF5_SDK_15.3.0_59ac345.zip -o nrf5_sdk.zip && unzip nrf5_sdk.zip && mv nRF5_SDK_15.3.0_59ac345 nrf5_sdk
```

This expands to...

```bash
cd /home/runner/work/_temp
curl \
  https://developer.nordicsemi.com/nRF5_SDK/nRF5_SDK_v15.x.x/nRF5_SDK_15.3.0_59ac345.zip \
  -o nrf5_sdk.zip
unzip nrf5_sdk.zip
mv nRF5_SDK_15.3.0_59ac345 nrf5_sdk
```

Here we call `curl` to download the [nRF5 SDK](https://www.nordicsemi.com/Software-and-tools/Software/nRF5-SDK) by Nordic Semiconductor.

We unpack the SDK into `/home/runner/work/_temp/nrf5_sdk`, which is cached by the previous step.

```yaml
      if:   steps.cache-nrf5sdk.outputs.cache-hit != 'true'  # Install SDK if not found in cache
```

Again, GitHub shall download the SDK only if the cache couldn't be found.

GitHub will remove any cache entries that have not been accessed in over 7 days.

## Checkout Source Files

```yaml
    - name: Checkout source files
      uses: actions/checkout@v2
```

TODO

## Show Files

```yaml
    - name: Show files
      run:  set ; pwd ; ls -l
```

TODO

## CMake

```yaml
    - name: CMake
      run:  mkdir -p build && cd build && cmake -DARM_NONE_EABI_TOOLCHAIN_PATH=${{ runner.temp }}/arm-none-eabi -DNRF5_SDK_PATH=${{ runner.temp }}/nrf5_sdk -DUSE_OPENOCD=1 ../
```

This expands to...

```bash
mkdir -p build
cd build
cmake \
  -DARM_NONE_EABI_TOOLCHAIN_PATH=/home/runner/work/_temp/arm-none-eabi \
  -DNRF5_SDK_PATH=/home/runner/work/_temp/nrf5_sdk \
  -DUSE_OPENOCD=1 \
  ../
```

TODO

## Make

```yaml
    - name: Make
      # For Debugging Builds: Remove "make" option "-j" for clearer output. Add "--trace" to see details.
      # For Faster Builds: Add "make" option "-j"
      run:  cd build && make pinetime-app
```

TODO

## Find Output

```yaml
    - name: Find output
      run:  find . -name pinetime-app.out
```

TODO

## Upload Built Firmware

```yaml
    - name: Upload built firmware
      uses: actions/upload-artifact@v2
      with:
        # Artifact name (optional)
        name: pinetime-app.out
        # A file, directory or wildcard pattern that describes what to upload
        path: build/src/pinetime-app.out
```

TODO

```yaml
# Embedded Arm Toolchain and nRF5 SDK will only be cached if the build succeeds.
# So make sure that the first build always succeeds, e.g. comment out the "Make" step.
```

# What's Next?

TODO

editing without the cloud

building without the cloud

Future Bluetooth flashing

FYI our plans for putting in Continuous Integration with GitHub Actions

For maintaining the central PineTime firmware

This is super cool, that makes so much so simple, no hassle with finding the right version of every software!

you can see exactly what steps we use to build firmware in the cloud

and replicate on your own pc

and with actual logs to compare the results

so its super educational yay!

[Check out my RSS Feed](https://lupyuen.github.io/rss.xml)