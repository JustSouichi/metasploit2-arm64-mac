# Metasploitable 2 on Mac M1 with UTM

This guide provides step-by-step instructions to download, convert, and run **Metasploitable 2** on a **Mac M1/M2** using **UTM**.

## Prerequisites

- Mac with Apple Silicon (M1/M2)
- [UTM](https://mac.getutm.app/) installed on your Mac
- [QEMU](https://www.qemu.org/) installed via Homebrew
- Internet connection to download Metasploitable 2

## Step 1: Download Metasploitable 2

1. Visit [https://sourceforge.net/projects/metasploitable/files/Metasploitable2/](https://sourceforge.net/projects/metasploitable/files/Metasploitable2/)
2. Download the `Metasploitable2-Linux.zip` file.
3. Extract the `.zip` file to get `Metasploitable.vmdk`.

## Step 2: Convert VMDK to QCOW2

Since UTM uses QEMU, we need to convert the `.vmdk` file into a compatible format (`.qcow2`).

1. Install QEMU if you haven't already:
   ```sh
   brew install qemu
   ```
2. Navigate to the folder containing `Metasploitable.vmdk`:
   ```sh
   cd /path/to/Metasploitable2
   ```
3. Convert the `.vmdk` file to `.qcow2`:
   ```sh
   qemu-img convert -O qcow2 Metasploitable.vmdk Metasploitable.qcow2
   ```

## Step 3: Create a UTM Virtual Machine

1. Open **UTM**.
2. Click **Create a New Virtual Machine**.
3. Select **Linux** as the operating system.
4. In the **Storage** section, choose **Import Drive** and select `Metasploitable.qcow2`.
5. Set the following configurations:
   - **CPU**: 1-2 cores
   - **Memory**: 512MB - 1GB
   - **Network**: Use **Bridged** or **Emulated VLAN** to interact with the host.
6. Click **Save** and start the VM.

## Step 4: Log into Metasploitable 2

Once the VM boots up, log in with the default credentials:

```
Username: msfadmin
Password: msfadmin
```

## Step 5: Network Configuration

To ensure that the Metasploitable 2 machine is accessible on your local network:

1. Run:
   ```sh
   ifconfig
   ```
   to get the assigned IP address.
2. Use this IP address to connect from your Mac via SSH:
   ```sh
   ssh msfadmin@<Metasploitable_IP>
   ```

## Notes

- Metasploitable 2 is intentionally vulnerable. **Do not expose it to the internet**.
- Use a separate virtual network or an isolated network setup for security.
- If using UTM's **NAT mode**, you may need to configure port forwarding for remote access.

## References

- [Metasploitable 2 Official Download](https://sourceforge.net/projects/metasploitable/files/Metasploitable2/)
- [UTM for macOS](https://mac.getutm.app/)
- [QEMU Documentation](https://www.qemu.org/docs/)

---

You are now ready to use Metasploitable 2 for ethical hacking and penetration testing on your **Mac M1 with UTM**. 🎯

