# How to unlock Bootloader?

It is easy to unlock bootloader. The steps is as follows.

1. Please check your environment first.

   ```shell
   fastboot devices
   ```

   If it fails or the command is not recognized, please look at this [article](https://blog.csdn.net/tq501501/article/details/117471016).

2. Connect to network and log in Google account on your device.

3. Enable OEM unlocking and USB Debugging.

   - Enable OEM: 

     Settings -> About Phone -> Tap on Build Number several times -> Go back to Settings -> System -> Developer Options -> enable OEM unlocking

   - USB Debugging: 

     Settings -> About Phone -> Tap on Build Number several times -> Go back to Settings -> System -> Developer Options -> USB Debugging

4. Here are the commands. Please execute one by one.

   ```shell
   adb reboot bootloader
   fastboot flashing unlock
   fastboot reboot
   ```
