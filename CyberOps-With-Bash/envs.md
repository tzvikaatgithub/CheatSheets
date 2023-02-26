ENVS
:bash:env:

`#!/bin/bash` tells the script what executable to use. Assuming bash is in //bin/
`#!/usr/bin/env bash` - tries to solve portability issues. here `env` is used to look up the location of bash. Assuming env is in /usr/bin/
