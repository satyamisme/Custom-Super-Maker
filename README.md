# Custom ROM Your New Samsung Laggy Budget Devices NOW

Tired of your Samsung budget phone lagging like it's stuck in molasses? This GitHub Actions workflow is your ticket to breathing new life into devices like the Samsung Galaxy A04s, A05, A05s, A06, A16, or any Samsung with a **super partition** and **Project Treble support** (sorry, A12 users, you’ll need to confirm compatibility). It’s the easiest way to replace the bloated stock system with a custom ROM, creating a repacked `super.img` that can make your phone feel snappy again. No complex setup, no endless terminal commands—just a few clicks and some URLs.

## How to Use
0.1. Why custom ROM for new device is so complex? What is super partition? Just use twrp bruh? 
Well, thank to Google introduce something call Super partition to replace the old single system partition, why? just search google.
0.2. Twrp usually dont work well with Super partition and also it very rare to those laggy get a twrp offical.
1. **Fork or Clone This Repository**: Make sure this repo is in your GitHub account.
2. **Go to the Actions Tab**: In your GitHub repo, click the "Actions" tab.
3. **Select the Workflow**: Choose "Android Super Partition Repack (Build-Only)".
4. **Run the Workflow**:
   - Click "Run workflow" and fill in the required fields:
     - **Stock Firmware URL**: A direct download link to your phone’s official Samsung firmware (e.g., from SamMobile, SamFrew, or MEGA.nz). See the `how to get link` below for more detail 
     - **Custom System URL**: A link to a custom ROM (`.img`, `.img.xz`, `.img.gz`, or `.zip` with a `system.img` inside). Look for a Treble-compatible GSI (Generic System Image) like LineageOS or Pixel Experience or Miku UI. Also please flash a rom have android version equal or higher than your stock ROM.
     - Optional settings:
       - **Empty Product/System_ext**: Check these to use empty `product.img` or `system_ext.img` for compatibility.
       - **Silent Mode**: Enabled by default to reduce log noise.
       - **Writable Partitions**: Check to make partitions writable (kinda useless if you not edit fstab).
       - **Purge All**: Enabled by default to clean up temporary files and save space.

You dont need to do anything with the setting here, just keep it as default.

5. **Wait and Download**: The workflow takes 10-20 minutes depending on file sizes. Once done, download the `repacked_super.zip` from the workflow’s "Artifacts" section.
6. **Flash the Output**: Use a tool like Odin or Heimdall to flash the `repacked_super.img` to your phone’s super partition. **Backup your data first**—flashing can wipe your device!
6.1. **For Odin user**: Choose AP, open your repack_super.tar and flash
6.2. **For heimdall, you can use the `heimdall_flash.sh`
8. **Reboot to Recovery Mode**: Please keep your phone use cable still connect to your PC, reboot by holding Vol DOWN + Power Button then hold Vol UP + Power Button to enter Recovery Mode, Format your phone data (why? it you not format it you will get stuck or unable to boot.

## Features
- **Works with Samsung Budget Devices**: Designed for models like A04s, A05, A05s, A06, A16, and others with a super partition and Treble support.
- **Supports Multiple File Formats**: Handles custom ROMs in `.img`, `.img.xz`, `.img.gz`, or `.zip` formats.
- **Saves Your Laggy Samsung**: Replaces the sluggish stock `"LaggyUI"` with a lightweight custom ROM.
- **Disk Space Management**: Automatically clears space on GitHub runners to avoid errors.
- **Caching for Speed**: Remembers stock firmware to skip redundant downloads.
- **Customizable Options**: Tweak settings like silent mode, empty partitions, or writable partitions.
- **No Local Setup Needed**: Runs entirely on GitHub’s servers—no need to install tools on your PC.

## Requirements
- A Samsung device with a **super partition** and **Project Treble support** (e.g., A04s, A05, A05s, A06, A16). Check your model’s specs if unsure.
- A `repacksuper.sh` script in the repo (included or provided by you) that supports the required flags.
- Direct download links for both stock firmware and custom ROM.
- Basic knowledge of flashing Android devices (you’ll need Odin or Heimdall to flash the output).

## Why This Is the Easiest Way to Fix Your Samsung
Samsung’s budget phones often come with bloated software that slows them down. This workflow lets you swap out the laggy stock system for a clean, fast custom ROM without needing to be a tech wizard. No local setup, no manual extraction—just provide two URLs, click a button, and get a ready-to-flash `super.img`. It’s the only automated solution tailored for Samsung’s super partition devices, making it dead simple to revive your phone.

## How It Works
This workflow automates the process of repacking a super partition, which combines multiple partitions (like `system`, `product`, and `system_ext`) into one `super.img`. Here’s the step-by-step:

1. **Grabs Your Files**:
   - Downloads the stock firmware from your provided URL (HTTP or MEGA.nz).
   - Extracts the `super.img` from the firmware’s `AP_*.tar.md5` file.
   - Downloads and prepares your custom ROM, converting it to a raw `system.img` if needed.

2. **Cleans Up Space**:
   - Clears out unnecessary files on the GitHub runner to avoid running out of disk space.
   - Uses multiple cleanup methods to ensure enough room for large firmware files.

3. **Runs the Magic Script**:
   - Executes `repacksuper.sh`, which merges your custom `system.img` into the stock `super.img`.
   - Applies your chosen settings (e.g., empty partitions, writable mode) via flags.

4. **Packages and Delivers**:
   - Verifies the repacked `super.img` was created successfully.
   - Creates a tarball (`repacked_super.tar`) for easy downloading.
   - Uploads both files as artifacts, ready for you to flash.

5. **Keeps Things Tidy**:
   - Optionally purges temporary files to save space.
   - Caches the stock firmware for faster future runs.

## Troubleshooting
- **"No space left on device"**: The workflow aggressively frees space, but huge firmware files can still cause issues. Check logs or try a smaller firmware.
- **"AP file not found"**: Ensure your stock firmware has an `AP_*.tar.md5` file with a `super.img*.lz4` inside.
- **"Unsupported file type"**: Your custom ROM must be a `.img`, `.img.xz`, `.img.gz`, or `.zip` with a `system.img` or `system.raw.img`.
- **ROM Compatibility**: Make sure your custom ROM is a Treble-compatible GSI that matches your device’s architecture (e.g., arm64-ab).

## License
This workflow (github action) is licensed under the [GPL v3 License](LICENSE). Original repacksuper script by Uluruman



## Special thank Uluruman for the repack script

## Contributing
Got ideas to make this even better? Submit a pull request or open an issue on GitHub. Let’s make laggy Samsungs a thing of the past!

## Disclaimer
Flashing custom ROMs can brick your device or void your warranty. Always back up your data and proceed at your own risk. The authors are not responsible for any damage to your device.
