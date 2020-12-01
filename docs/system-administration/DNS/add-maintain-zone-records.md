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

### Updating a Reverse Zone record.
#### Sample reverse file.

This example will assume that your zone file is db.192.168.11

```
$TTL	86400
@	IN	SOA	ns1.example.com. root.example.com. (
	                 2020112201		; Serial
			             604800		; Refresh
			              86400		; Retry
			            2419200		; Expire
                          86400 )  	; Negative Cache TTL

; Name servers
    IN	NS	  ns1.example.com.
    IN	NS	  ns2.example.com.

; Reverse zone records.
1   IN      PTR     router.example.com.

10  IN      PTR     ns1.example.com.
20  IN      PTR     ns2.example.com.

35  IN      PTR     hassio.example.com.
40  IN      PTR     printer.example.com.
```

#### Updating the serial.
Following the steps given before we will update the serial number.
Replace `2020112201` with the new date. For the purposes of this example I will assume the date is Dec 1st, 2020. Change the serial to `2020120101`. End in `01` as this is the first edit of the day.

#### Hosts to be added.
Next add your new records.

1. iphone1 has an address of 192.168.11.31
2. iphone2 has an address of 192.168.11.32

#### Your final file should look something like below.

!!! note "Ordering"
    As a general rule. Devices are listed by IP Address with a space provided between address blocks.

```
$TTL	86400
@	IN	SOA	ns1.example.com. root.example.com. (
	                 2020120101		; Serial
			             604800		; Refresh
			              86400		; Retry
			            2419200		; Expire
                          86400 )  	; Negative Cache TTL

; Name servers
    IN	NS	  ns1.example.com.
    IN	NS	  ns2.example.com.

; Reverse zone records.
1   IN      PTR     router.example.com.

10  IN      PTR     ns1.example.com.
20  IN      PTR     ns2.example.com.

30  IN      PTR     iphone1.example.com.
31  IN      PTR     iphone2.example.com.

35  IN      PTR     hassio.example.com.
40  IN      PTR     printer.example.com.
```

### Updating a Forward Zone record.
#### Sample Forward file.
```
$TTL	604800
@	IN	SOA	ns1.example.com. root.example.com. (
		                    2020112201		; Serial
			                    604800		; Refresh
			                     86400		; Retry
			                   2419200		; Expire
			                    604800 )  	; Negative Cache TTL


                        IN  NS  ns1.example.com.
                        IN  NS  ns2.example.com.

ns1.example.com.        IN  A   192.168.11.10
ns2.example.com.        IN  A   192.168.11.20

hassio.example.com.     IN  A   192.168.11.35
printer.example.com.    IN  A   192.168.11.40

; External Servers/Services
blog.example.com.       IN  CNAME   ghs.google.com.
bogus.example.com.      IN  A   203.X.X.X
```

#### Updating the serial.
Following the steps given before we will update the serial number.
Replace `2020112201` with the new date. For the purposes of this example I will assume the date is Dec 1st, 2020. Change the serial to `2020120101`. End in `01` as this is the first edit of the day.

#### Hosts to be added.
Next add your new records.

1. iphone1 has an address of 192.168.11.31
2. iphone2 has an address of 192.168.11.32

#### Your final file should look something like below.

```
$TTL	604800
@	IN	SOA	ns1.example.com. root.example.com. (
		                    2020120101		; Serial
			                    604800		; Refresh
			                     86400		; Retry
			                   2419200		; Expire
			                    604800 )  	; Negative Cache TTL


                        IN  NS  ns1.example.com.
                        IN  NS  ns2.example.com.

ns1.example.com.        IN  A   192.168.11.10
ns2.example.com.        IN  A   192.168.11.20

; Using a short cut. See note below.
iphone1                 IN  A   192.168.11.31
iphone2                 IN  A   192.168.11.32

hassio.example.com.     IN  A   192.168.11.35
printer.example.com.    IN  A   192.168.11.40

; External Servers/Services
blog.example.com.       IN  CNAME   ghs.google.com.
bogus.example.com.      IN  A   203.X.X.X
```

!!! note "Short cut in forward zone records."
    This only works for forward zone records and you should take care to always include a terminating period (.) if you are not using this method.

    How does this work?

    In the zone configuration you have created a zone file reference.

    ```
    zone "example.com" {
    ```

    This is used and automatically appended to your host record.

## Adding a new zone file to your servers.


!!! note "Adding a new zone record."
    1. You will need to update all name servers. Starting with NS1.
    2. You only need to create the actual zone file on NS1.
    3. Set the serial record :)

!!! warning
    These steps are only done on your primary name server (NS1)

### Forward Zone Record.

### Reverse Zone Record.
