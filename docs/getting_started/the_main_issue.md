# The `Main` Issue
In this section we will explore the unintended side-effects that arises when main-functions are omitted.
### The issue with not using a main-function
So far we have learned that you can write Python code directly in a file and execute with Python, but that is not the proper way to do it because it will most certainly lead to unintended side effects if your program ever grows sufficiently. The problem arises when you will later on be writing modules which you import (and call) from other Python files.

Instead you should do it like this:

```python
def my_logic():
	# Execute some logic
	pass
	
if __name__ == '__main__':
	print("executing my logic")
	my_logic()
```

Doing it this way is correct and will not cause any of the code to ever be executed when importing the function `my_logic` into another. Alas, it gives you control over the code you execute - while writing Python without the `if __name__ == '__main__':` clause will always execute that code whenever you import the file it is contained in, into another file.

Both methods are equally run by typing `python main.py` in the terminal (assuming the filename is identical for the purpose of the explanation).

## Furhter illustration
Below we have a file - let's give it some name, say: sniffer.py
```python title="sniffer.py"
import time


def get_epoch_timestamp():
    """Returns the current epoch timestamp in seconds."""
    return int(time.time())  # Convert float to int for whole seconds


print("[X] Setting up my l33t sniffing tool")
configure_scapy()
shutdown_os_ports()
setup_evasion()
intercepter = NetworkSniffer(interface="enet01").listen_from_attached_network_hub()
print("[X] Setup completed - intercepter initialized on enet01 interface")

while True:
    print("[X] Listening for and intercepting traffic")
    intercepter.listen(save_to=f"intercepted_traffic__{get_epoch_timestamp()}.pcap")
```

### The problem!
Now we have another file where we wish to use the `get_epoch_timestamp()` from earlier:
```python hl_lines="1"
import sniffer # imports sniffer.py

if __name__ == '__main__': # (1)
	print("The current epoch timestamp is: {sniffer.get_epoch_timestamp()}")  # (2)
```

1.  ⚠️ The fact that we are using a main-function here, doesn't prevent the error that is about to happen.
2.  ℹ️ This is an f-string, you'll learn about those later - for now it's sufficient to know that f-strings lets you call functions and retrieve their return values inside of strings.
Now what do you think will happend when we run this new file, which additionally has a main-function?

If we inspect the print statements we will see the following thing happending:
```python
>>> [X] Setting up my l33t sniffing tool
>>> [X] Setup completed - intercepter initialized on enet01 interface
```
!!! danger 
    And from thereon the program will hang indefinitely because it's stuck in the while loop from `sniffer.py` - but don't mistake that for the actual issue.
    **The real issue is that we wished only to use the `get_epoch_timestamp()` function in our new file, but instead we ran all the code inside of `sniffer.py` which in this case just co-incidentally caused us to be stuck in a while loop.**

Alas, aim to never write Python code directly inside a Python file unless you're just testing stuff out. But even then, you can avoid this entire thing by just typing `if __name__ == '__main__:` and voila, you won't ever have any issues.