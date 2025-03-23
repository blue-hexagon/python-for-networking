## Installing Python

Go to Python's Official Website and navigate into version 3.13.2 [by clicking here](https://www.python.org/downloads/release/python-3132/)
and download and install Windows 64-bit installer under the files section.

## Installing an IDE

Go this website and download and install [PyCharm Community Edition](https://www.jetbrains.com/pycharm/download/?section=windows)

## Setup a bare-bones Python Application in PyCharm

Then open PyCharm and create a new pure Python project and create a new file named main.py.

Write the following inside the file:

```python title="main.py"
print("Hello World!")
```

Open up the terminal and type `python main.py` and press enter.

## Global-scope Code

By default, Python allows you to type code directly into a file and run it, you won't get an error for that - but you won't get a high grade
either!

Here I've written a function for looking up saved SSIDs (and their stored passwords) on Windows computers. The example illustrates how
Python is called without using a main-function as an entry point.
This method has serious issues though, and we'll explore this further in the coming chapter.

```python title="ssid_snitch.py"
import platform
import subprocess
from pprint import pprint
from typing import Any, Dict


def get_ssid_store() -> Dict[Any, Any]:
    """  
    Reads all saved WLAN profiles for the user running this script,
    and returns a mapping of `ssid:ssid_password` for each stored WLAN profile found.
    """
    if not platform.uname().system.lower() == "windows":
        raise OSError("Requires the Windows operating system")
    ssid_pw_map: Dict[Any, Any] = {}
    data = subprocess.check_output(["netsh", "wlan", "show", "profiles"]).decode("utf-8").split("\n")
    profiles = [i.split(":")[1][1:-1] for i in data if "All User Profile" in i]
    for ssid in profiles:
        results = (
            subprocess.check_output(["netsh", "wlan", "show", "profiles", ssid, "key=clear"])
            .decode("utf-8")
            .split("\n")
        )
        results = [b.split(":")[1][1:-1] for b in results if "Key Content" in b]
        try:
            ssid_pw_map.setdefault(ssid, results[0])
        except IndexError:
            ssid_pw_map.setdefault(ssid, "N/A")
    return ssid_pw_map


pprint(get_ssid_store())
print("Any Python is valid here!")
```