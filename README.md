# hello_world
My1stRepository
Hello Anil, Welcome to the GitHub_world..!!
This line is edited by Anil..!!!

## Copilot suggested code for system uptime
#!/bin/bash
echo "system uptime information"
uptime
uptime -p  # Suggested a typo here

## Copilot suggestec code for checking the system update using python script

import os
import sys
import platform

def get_uptime():
    """
    Returns the system uptime as a string.
    """
    if platform.system() == "Windows":
        try:
            import ctypes
            from ctypes import wintypes

            GetTickCount64 = ctypes.windll.kernel32.GetTickCount64
            GetTickCount64.restype = ctypes.c_ulonglong
            ms = GetTickCount64()
            seconds = int(ms // 1000)
        except Exception:
            return "Unable to determine uptime on Windows."
    else:
        try:
            with open('/proc/uptime', 'r') as f:
                uptime_seconds = float(f.readline().split()[0])
                seconds = int(uptime_seconds)
        except FileNotFoundError:
            # macOS and BSD fallback
            try:
                import subprocess
                output = subprocess.check_output(['uptime']).decode()
                # macOS uptime output: 15:23  up 8 days,  2:19, 2 users, load averages: 1.65 1.76 1.79
                import re
                match = re.search(r'up (.*), \d+ user', output)
                if match:
                    return f"Uptime: {match.group(1)}"
                return "Unable to parse uptime output."
            except Exception:
                return "Unable to determine uptime on this system."
    days = seconds // (24 * 3600)
    seconds %= (24 * 3600)
    hours = seconds // 3600
    seconds %= 3600
    minutes = seconds // 60
    seconds %= 60
    return f"Uptime: {days} days, {hours} hours, {minutes} minutes, {seconds} seconds"

if __name__ == "__main__":
    print(get_uptime())

