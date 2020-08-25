# Uninteruptible sleep

There are cetain system calls like `mkdir` which cannot be interrupted. If something happens to block them, they will persist until a reboot because they cannot be killed.

When running `top`, you might see a process whose status is `D`, which means uninterruptible sleep.

https://eklitzke.org/uninterruptible-sleep#:~:text=One%20of%20the%20curious%20features,until%20the%20system%20call%20completes
