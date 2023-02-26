CLICK
:flask:click:

# Contents

- [References](#References)
- [Tips and Tricks](#Tips and Tricks)

# References

[Welcome to Click — Click Documentation (8.0.x)](https://click.palletsprojects.com/en/8.0.x/)

[Command Line Interface — Flask Documentation (2.0.x)](https://flask.palletsprojects.com/en/2.0.x/cli/)

[Comparing Python Command-Line Parsing Libraries – Argparse, Docopt, and Click – Real Python](https://realpython.com/comparing-python-command-line-parsing-libraries-argparse-docopt-click/)

# Tips and Tricks

Click is a library to create cli interfaces using decorators.

when you separate business logic from interfaces, you can apply click decorators to the imported business logic functions like so:

```
# apply click decorators to imported function
@click.command()
@click.option(...)
def cli_function(flag: bool):
    google_module.function(flag)

# then call it
cli_function()
```
