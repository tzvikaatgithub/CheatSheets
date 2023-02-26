## Totaling Numbers in Data

The goal here is to identify hosts that have transferred unusually large amounts of data compared to other hosts. Which can mean data theft and exfiltration. Once such host is identified, the next step is to review the specific pages and files accessed by it, to classify the behavior as malicious or benign.

To sum up the amount of data requested and received by an IP address, you only need a few small changes to 07-countem.sh:
* tweak `cut` to provide more columns (and include the byte count)
* change `let cnt[$id]++` from simple increment to `let cnt[$id]+=$data` to sum up the bytes

`cut -d' ' -f1,10 access.log | bash 08-summer.sh | sort -k 2.1 -rn`
