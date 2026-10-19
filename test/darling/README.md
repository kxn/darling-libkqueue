# Darwin ABI receipt regression

`receipts.c` runs against Darling's public Darwin `kevent` and `kevent64` APIs.
It needs a Darwin SDK and a complete Darling runtime; it is not a Linux-native
libkqueue test. The Linuxcode source attachment provides the Linux-side build
and execution driver in `scripts/test-kqueue-receipts.py`.

The checks cover successful EV_RECEIPT changes without an event buffer, applying
all changes when receipt slots run out, immediate buffered receipts with spare
slots, real ENOENT/EINVAL failures, returned error receipts, opaque user data,
read/write readiness, deleting watches, and the 64-bit event API. A process alarm
rejects a wait for unrelated events after returning a registration receipt.
