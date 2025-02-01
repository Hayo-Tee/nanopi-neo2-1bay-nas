## Running OpenWrt/ImmortalWrt on NanoPi NEO2 with 1-Bay NAS Kit

I have a **NanoPi NEO2** and a **1-Bay NAS Kit**. Unfortunately, I couldn't find any online guides on how to make my NAS Kit work with OpenWrt or ImmortalWrt. After some research and help from ChatGPT, I discovered a simple solution: modifying the Device Tree Source (DTS) to enable the required USB and other ports.

### Solution: Modifying the DTS

By default, some USB and other ports are disabled in the DTS file. Changing them to "okay" allows the system to detect and use the NAS hardware properly.

### Steps to Build and Modify the Device Tree

1. **Obtain the DTS file** on another PC:
   ```bash
   dtc -I dtb -O dts -o my_device.dts my_device.dtb
   ```

2. **Edit the DTS file**:
   - Open `my_device.dts` in a text editor.
   - Locate the USB and SATA (if applicable) sections.
   - Change `status = "disabled";` to `status = "okay";` where needed.

3. **Compile the modified DTS back to DTB**:
   ```bash
   dtc -I dts -O dtb -o my_device.dtb my_device.dts
   ```

4. **Copy the new DTB file to a bootable storage device** (e.g., an SD card or USB drive).

5. **Insert the storage device into the NanoPi NEO2**, ensuring it is correctly connected.

6. **Boot the NanoPi NEO2 with the updated DTB file**, allowing the system to detect the changes.

### Conclusion

With this simple DTS modification, my NanoPi NEO2 NAS Kit now works correctly with OpenWrt/ImmortalWrt. Hopefully, this helps others facing similar issues!

P.S. I will later add the modified DTB file for ImmortalWrt.

