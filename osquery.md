OSQUERY

:osquery:grr:

# Contents

- [Resources](#Resources)
- [OSquery](#OSquery)
- [Grr - by Google](#Grr - by Google)

# Resources

SQLite-based OS query engine for Mac, Linux & Windows.

[install](https://osquery.io/downloads/official/4.5.1)

[docs](https://osquery.readthedocs.io/en/stable/)

[examples](https://github.com/osquery/osquery)

[query packs](https://github.com/osquery/osquery/tree/master/packs)

[tables schema](https://osquery.io/schema/4.5.1/)

Websites
osquery
https://osquery.io/
osquery documentation
https://osquery.readthedocs.io/en/stable/
File Integrity Monitoring
https://osquery.readthedocs.io/en/stable/deployment/file-integrity-monitoring/
YARA Scanning
https://osquery.readthedocs.io/en/stable/deployment/yara/
Software
osquery
https://github.com/facebook/osquery
example configuration
https://github.com/facebook/osquery/blob/master/tools/deployment/osquery.example.conf
YARA pattern matching
https://virustotal.github.io/yara/
GRR Rapid Response
https://github.com/google/grr
TLS endpoint for osquery configurations
https://github.com/heroku/windmill

# OSquery


Enterprise level tool. You'd need to bring info from it to another visualization tool.

Best works on Mac (works well everywhere). It is a tool from FaceBook.

This tool exposes system information via SQL tables. Basically you work with it as if your system is an SQL db.

OSquery uses a superset of SQLite language
    * [SQL Introduction - osquery](https://osquery.readthedocs.io/en/stable/introduction/sql/).
    * [Query Language Understood by SQLite](https://www.sqlite.org/lang.html).

There is only `SELECT` statement. Other statements do exist but they are only useful if you are creating `VIEW`s.

Familiarize yoruself with the structure by launching `.tables` and `.schema`.

`.mode line` tweaks output format - useful for smaller screens.

JOIN: `SELECT pid, name, path FROM osquery_info JOIN processes USING (pid);`

Main Components:
    1. `osqueryi` interactive tool. It will open a prompt. For queries ad hoc
    2. `osqueryd` for continuous detection, scheduled pre-set queries
        - writes to log (probably off system, like syslog SIEM, splunk, elk)
        - osquery.conf is the main config file
        - get deployment configurations examples from the link below - readthedocs
    3. `osqueryctl`

`select * from startup_items;` the results go into a log file.

There are queries that are general, and queries that are OS specific.

The advantage here is that you would query all systems you have using the same query.

C makes it fast, SQL makes it simple.

You want to look for IoC - changes from the baseline.

Examples:

`select name, path FROM kernel_extensions where name not like 'com.apple%';` display non apple extensions

`select distinct processes.name, listening_ports.port, processes.pid FROM listening_ports JOIN processes USING (pid) WHERE listening_ports.address = '0.0.0.0';` get process name, port and pid for processes listening on all interfaces.

`SELECT name, program || program_arguments AS executable FROM lanchd WHERE (run_at_load = 1 AND keep_alive = 1) AND (program != '' OR program_argumants != '');` every MacOS daemon that launches an executable and keeps running the executable.

Packs:
    * groups are queries that had been found to be useful are listed on osquery.io/docs/packs/..
    * there are queries for compliance and malware signatures

You can use osquery for file integrity monitor.

You can use YARA to identify and classify malware. For scanning and querying.

Basically, you can use this tool to produce logs. Then you need to take those logs somewhere for analysis and presentation.

# Grr - by Google

Grr - tool by google. Also a tool for SOC teams.
