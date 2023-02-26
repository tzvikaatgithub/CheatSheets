## Sorting and Arranging Data

Look at the extremes, things that occurred most or least frequently (ex: high number of page request can indicate scanning activity, or a DDoS). Smallest or largest data transfers (high number of bytes downloaded by a host can indicate site cloning or data exfiltration).

Append to the pipe `| sort -k 2.1 -rn | head -15` reverse numeric sort by key
