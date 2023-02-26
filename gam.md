Google Apps Management (?)
:google:gam:

# Contents

- [Intro](#Intro)
- [References](#References)
- [Examples of GAM commands](#Examples of GAM commands)

# Intro

GAM is a 3rd party, cross-platform tool, that can be downloaded on GitHub https://github.com/jay0lee/GAM
    * needs to be installed and authorized

Almost everything that you can do in GSuite can be done with GAM.

[Overview and installation - Eric Curts](https://docs.google.com/document/d/1Z7OONOFR9qhTiw3te3PgwNy-ZwrOvc1Na6un53CvQc0/edit#)

# References

[GAM Wiki · GitHub](https://github.com/jay0lee/GAM/wiki)
    * [GAM Bulk Operations](https://github.com/jay0lee/GAM/wiki/BulkOperations)

[GAMADV-XTD3](https://sites.google.com/jis.edu.bn/gam-commands/home) This is a collection of GAM commands I use or have kept, waiting for the time they "save the day".
    * [users](https://sites.google.com/jis.edu.bn/gam-commands/people/users#h.covt6f8l9r5k)
    * [Groups](https://sites.google.com/jis.edu.bn/gam-commands/people/groups?authuser=0#h.vyreao5vxxb9)
    * Python stuff [GitHub - taers232c/GAM-Scripts3: Scripts for use with GAM - Python 3.6+](https://github.com/taers232c/GAM-Scripts3)



# Examples of GAM commands

    * `gam create user manual.gam.01@tech-realm.co firstname "Manual" lastname "GAM 01" password thisisapassworddontuseme changepassword on org /Projects` create user, specifying domain (if you have multiple domains), set password, policy, and org
    * `gam create user manual.gam.02 firstname "Manual" lastname "GAM 02" password thisisapassworddontuseme changepassword on org /Projects` create user without specifying domain
    * `gam csv users.csv gam create user ~Email firstname ~FName lastname ~LName password ~Pass changepassword on org ~OU` create users via CSV file
        * load CSV file into the next command
        * `~FieldName` field name from the CSV file
