# HTML Injector

This Python script demonstrates HTML injection by intercepting HTTP requests and responses using a Netfilter queue and modifying the content of HTTP responses to include custom scripts. This is useful for educational purposes to understand how attackers manipulate HTTP traffic to inject malicious code.

## Features

- Intercepts HTTP traffic using a Netfilter queue.
- Modifies HTTP responses to inject custom HTML or JavaScript code.
- Demonstrates the basics of HTTP response manipulation with Scapy and Netfilter.

## Prerequisites

- Python 3.x
- Linux-based operating system
- `scapy` library (for handling network packets)
- `netfilterqueue` library (for working with Netfilter queues)

## Installation

Clone the repository to your local machine:

```bash
git clone https://github.com/yourusername/html_injector.git
cd html_injector
```

Install the required libraries:

```bash
pip install scapy netfilterqueue
```

## Usage

Run the script with superuser privileges to enable HTTP injection.

```bash
sudo python3 html_injector.py
```

### Notes:

- The script is designed to inject a JavaScript alert (`<script>alert('test');</script>`) into every HTTP response.
- Modify the `injection_code` variable in the script to include your desired HTML or JavaScript code.
- Ensure that the appropriate Netfilter rules are applied to redirect HTTP traffic to the Netfilter queue.

### Setting Up Netfilter Rules:

Use the following command to redirect HTTP traffic to the Netfilter queue:

```bash
sudo iptables -I FORWARD -j NFQUEUE --queue-num 0
```

If you are testing on your own machine, use:

```bash
sudo iptables -I OUTPUT -j NFQUEUE --queue-num 0
sudo iptables -I INPUT -j NFQUEUE --queue-num 0
```

### Stopping the Script:

When you are done, reset the iptables rules:

```bash
sudo iptables --flush
```

## Example:

Run the script to intercept HTTP responses and inject the JavaScript code:

```bash
sudo python3 html_injector.py
```

Output:

```
[+] Request
[+] Response
<scapy.packet.Packet object at 0x...>
```

The script will inject the JavaScript alert into all HTTP responses that contain a `</body>` tag.

## Notes:

- This script is for educational purposes only. Use it responsibly and only in environments where you have permission to perform testing.
- HTML injection is illegal and unethical if performed without authorization.

## Troubleshooting:

- Ensure you have the required libraries installed.
- Verify that the Netfilter rules are applied correctly.
- Make sure to run the script with `sudo` or as root to access network packets.
- Test the script in a controlled environment with HTTP traffic.

## License

This project is licensed under the MIT License.

## About

This script is part of the course [Learn Python & Ethical Hacking from Scratch](https://www.udemy.com/course/learn-python-and-ethical-hacking-from-scratch/) on Udemy. The course covers Python scripting and its application in ethical hacking, network security, and more.
