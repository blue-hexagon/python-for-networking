# The `Main` Issue
In this section we will explore the unintended side-effects that arises when main-functions are omitted.
### The issue with not using a main-function
But that is not the proper way to do it because it easily (and most certainly will if your project ever gets big enough) lead to unintended side effects when importing modules (Python code such as functions stored in other .py files).

Instead you should do it like this:

```python
def my_logic():
	# Execute some logic
	pass
	
if __name__ == '__main__':
	print("executing my logic")
	my_logic()
```

Doing it this way is correct and will not cause any of the code to ever be executed when importing the function `my_logic` into another file, unless you explicitly instruct Python to do it somewhere in your code. Alas, it gives you control over the code you execute - while writing Python without the `if __name__ == '__main__':` clause will always execute that code whenever you import the file it is contained in, into another file.

And you can of course run both equally by typing `python main.py` in the terminal - in that way they work identically.

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

if __name__ == '__main__': # It doesn't prevent the error that is about to happend, that we are using a proper main method here!
	print("The current epoch timestamp is: {sniffer.get_epoch_timestamp()}")
```
1. :man_raising_hand: I'm a code annotation! I can contain `code`, __formatted
    text__, images, ... basically anything that can be written in Markdown.
Now what do you think will happend when we run this new file, which additionally has a main-function?

If we inspect the print statements we will see the following thing happending:
```python
>>> [X] Setting up my l33t sniffing tool
>>> [X] Setup completed - intercepter initialized on enet01 interface
```
And from thereon the program will hang indefinitely because it's stuck in the while loop from sniffer.py - but that's not the main issue!
**The main issue is that we wished only to use the get_epoch_timestamp() function in our new file, but instead we ran all the code inside of sniffer.py - not good!**

Alas, aim to never write Python code directly inside a Python file unless you're just testing stuff out.