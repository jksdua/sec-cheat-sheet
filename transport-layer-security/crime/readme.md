TLS CRIME Vulnerability
=======================

Related to SSL compression

### Background

- [ ] Add reading material here

- <http://en.wikipedia.org/wiki/CRIME_%28security_exploit%29>

### Nessus Plugin:
<http://www.tenable.com/plugins/index.php?view=single&id=62565>

A Nessus output related to CRIME looks like below.

![Nessus output](./nessus-1.PNG)

Make sure you look for the reason to check whether it is SPDY or SSL compression that is the problem.

![Nessus output](./nessus-2.PNG "Reason")

### Verifying the finding

The vulnerability can be verified by using the OpenSSL library. Make sure you run both tests mentioned below since I've run into situations in the past where OpenSSL comes back with `Compression: NONE` but the server still sends back a compressed payload in test 2.

#### Test 1

Connect to the host using OpenSSL using `openssl s_client -connect  <HOST>:<PORT>`. Look for the line which starts with compression. If the website is not vulnerable, this value should be *NONE*. A sample output is shown below.

![OpenSSL Check 1](./openssl-check-1.PNG)

What you will notice is that OpenSSL creates an active connection with the host. At this point, try the second check.

#### Test 2

Go to this awesome blog for the second test - <https://scottlinux.com/2012/09/13/enable-or-disable-compression-in-apache/>

If the link doesn't work, use the one stored in the [archive](__link_archive/scottlinux.com _ Linux Blog - Enable or Disable Compression in Apache.htm)
