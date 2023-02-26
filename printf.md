PRINTF
:printf:

`printf -v TODAY 'scan_%(%F)T' -1`   # e.g., scan_2017-11-27

`-v` save output to var (newer bash)

`%()T` format specifiers for printing date and time values, same as in `strftime` sys lib call
    `%F` year-month-day

`-1` now
