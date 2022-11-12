# How to download AOSP?

If you want to download android-12.1.0_r2 on Ubuntu 20.04.4 LTS. The steps is as follows:

1. Create a directory to place the source code.

   ```shell
   mkdir android-12.1.0-r2
   ```

2. Download the repo script and save it to `~/bin/repo`.

    ```shell
    curl https://storage.googleapis.com/git-repo-downloads/repo > ~/bin/repo
    ```

3. Change the mode of `~/bin/repo`.

   ```shell
   chmod a+x ~/bin/repo
   ```

4. Initialize the directory with Repo command：

   ```shell
   # If you can visit android.googlesource.com:
   repo init -u https://android.googlesource.com/platform/manifest -b android-12.1.0_r2
   
   # If not:
   repo init -u https://mirrors.tuna.tsinghua.edu.cn/git/AOSP/platform/manifest -b android-12.1.0_r2
   ```

   The parameter followed by `-b` is a version. If you don't know how to choose a version, please visit [Codenames, Tags, and Build Numbers](https://source.android.com/setup/start/build-numbers#source-code-tags-and-builds). Same thing as above, you can download `android-11.0.0_r48` source code with Repo command:

   ```shell
   # If you can visit android.googlesource.com:
   repo init -u https://android.googlesource.com/platform/manifest -b android-11.0.0_r48
   
   # If not:
   repo init -u https://mirrors.tuna.tsinghua.edu.cn/git/AOSP/platform/manifest -b android-11.0.0_r48
   ```

5. Sync code now. It takes about 4~5 hours (depends on your network) to wait for synchronization to complete.

   ```shell
   repo sync -c
   ```

> Android Source Code: https://source.android.com/docs/setup/build/downloading

# Reflash a build to devices

Please using the  [Android Flash Tool](https://flash.android.com/preview/dp1) for Pixel.



