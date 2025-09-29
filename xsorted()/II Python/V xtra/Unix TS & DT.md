Seconds since January 1st, 1970 00:00:00 UTC { the epoch }
```python
import time
from datetime import datetime

# current timestampt as a float with microseconds
now = time.time()

# whole seconds
now_int = int(time.time())

# pause for x sexonds
time.sleep(2.5)

# time something
start = time.time()
# . . . do something . . .
elapsed = time.time() - start # seconds elapsed
```

By default and in the raw, Unix timestamps are in a non-readable integer format.
i.e.: 1759122137.2139218
	*It can be converted to readable formats with datetime but the raw format is immune to distortion through timezone changes of the client or host.*
```python
import time
from datetime import datetime

now = time.time()

date = datetime.fromtimestamp(now)
print(date) # 2025-09-29 01:05:40.530998

print(date.strftime('%m-%d-%Y')) # 09-29-2025
print(date.strftime('%m/%d/%Y')) # 09/29/2025
print(date.strftime('%B %d, %Y')) # September 29, 2025
print(date.strftime('%Y%m%d.%H%M%S')) # 20250929.011145
print(date.strftime('%Y.%m.%d_%H.%M.%S')) # 2025.09.29_01.11.03

# revert to timestamp
og_timestamp = date.timestamp() # 1759122784.576293
```

Add. formatting & syntax's:
```python
%Y - 4 digits; 2024
%y - 2 digits; 24
%m - month as a digit 1 - 12
%B - month as its full name; September
%b - month as abreviated name; Sep
%d - day 1 - 31
%H - 24 hour time
%h - 12 hour time
%M - minute 1 - 59
%S - second 1 - 59
%p - AM / PM
```