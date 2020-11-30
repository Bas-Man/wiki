---
title: Adding and Maintaining Zone Records
summary: A guide to adding and maintaining zone records.
date: 2020-12-01
authors:
  - Adam Spann
---

This is a quick guide on how to update/maintain your zone records or how to add a new zone if needed.

## Updating existing zone records.

!!! note "Updating existing zone records."
    1. You only need to update your primary name server (NS1)
    2. Always update the serial number. If you forgot to do this. You will have issues.

### The basic steps.

  1. Update the serial number.
  2. Update your zone records.
  3. Trigger the reload.

## Adding a new zone file to your servers.

!!! note "Adding a new zone record."
    1. You will need to update all name servers. Starting with NS1.
    2. You only need to create the actual zone file on NS1.
    3. Set the serial record :)

!!! warning
    These steps are only done on your primary name server (NS1)

### Forward Zone Record.

### Reverse Zone Record.
