link: https://www.netmeister.org/blog/infosec-competencies.html
name: (Technical) Infosec Core Competencies
topic: 
author:
tags:

1.  How to read a [CVE](https://en.wikipedia.org/wiki/Common_Vulnerabilities_and_Exposures) announcement and assess the impact based on its [CWE](https://en.wikipedia.org/wiki/Common_Weakness_Enumeration) / [CVSS](https://en.wikipedia.org/wiki/Common_Vulnerability_Scoring_System) score and description. Understand that CVSS scores are relative and impact in _your_ environment may be different.
2.  How to read a hyped, name- and logo branded, corporation backed vulnerability announcement -- as well as the relevant RFCs and actual research paper, if any, instead of just the breathless webpage -- and distill the actual, realistic threat to your environment.
3.  The difference between a vulnerability, a threat, risk, an exploit, and attack surface; the likelihood of an exploit based on an adversary's motivation, goals, and capabilities; being able to ballpark the cost of defense within a given scope.
4.  The difference between [authentication](https://en.wikipedia.org/wiki/Authentication) (_authN_) and [authorization](https://en.wikipedia.org/wiki/Authorization) (_authZ_); between secrecy and authenticity; between authenticity and integrity. Be able to translate these concepts across different contexts.
5.  The difference between [symmetric](https://en.wikipedia.org/wiki/Symmetric-key_algorithm) or _private_ and [asymmetric](https://en.wikipedia.org/wiki/Public-key_cryptography) or _public_ key cryptography; between encryption and hashing; between a [key derivation function](https://en.wikipedia.org/wiki/Key_derivation_function) and an [HMAC](https://en.wikipedia.org/wiki/HMAC) used for message authentication.
6.  You don't need to be cryptographer, but you should know roughly what the [cryptographic right answers](https://latacora.micro.blog/2018/04/03/cryptographic-right-answers.html) for your developers' questions are -- and why.
7.  The difference between encryption in transit and encryption at rest.
8.  Know to use TLS >= 1.2, but you don't need to know the details of all the ciphers and algorithms. But you should understand mTLS and client cert validation vs. server cert validation conceptually.
9.  Understand the [x509 PKI concepts](https://en.wikipedia.org/wiki/X.509), [trusted CA bundles](https://twitter.com/jschauma/status/1220904655753969664), cert chains, and common client behavior.
10.  Know [how to use](https://www.madboa.com/geek/openssl/) 'openssl s_client' and 'openssl x509' to troubleshoot TLS connections, including STARTTLS.
11.  HTTP basics: be able to make manual HTTP requests via telnet(1) / openssl s_client; know enough [HTTP headers](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers) and the general concepts of [CSP](https://developer.mozilla.org/en-US/docs/Web/HTTP/CSP); be able to use in-browser developer tools to troubleshoot, debug, and replay requests.
12.  Enough of the [JavaScript and HTML DOM](https://www.w3schools.com/js/js_htmldom.asp) to understand the different XSS attack types conceptually.
13.  How to use curl(1) to post data to and pull information from an API; use jq(1) to [manipulate JSON](https://stedolan.github.io/jq/tutorial/).
14.  Be [able to use](https://danielmiessler.com/study/tcpdump/) tcpdump(1) to at least get the gist of what's going on on the wire. I.e., protocol, type, port, TCP S/R/P/F/., sequence numbers, payload...
15.  Be able to use e.g., [Wireshark](https://www.wireshark.org/) to drill down into specific flows, filter and pick outliers out of the noise, debug TLS with [logged pre-master secret](https://twitter.com/jschauma/status/1227973307376504832).
16.  Be aware of the [different ICMP types](http://shouldiblockicmp.com/) beyond echo request/reply: time exceeded, fragmentation required, destination unreachable...
17.  Be able to spot certain CIDRs. E.g., for IPv4: 127/8, 169.254/16, 224/4, 240/4, RFC1918; for IPv6: ::1, fc00::/7, fe80::/10, ff00::/8
18.  Understand that RFC1918 does not imply the host cannot be reached from the internet; internalize that [NAT is not](https://security.stackexchange.com/questions/8772/how-important-is-nat-as-a-security-layer) a [security control](https://security.stackexchange.com/questions/44065/with-ipv6-do-we-need-to-use-nat-any-more/44068#44068).
19.  How to send arbitrary packets between two hosts, e.g., via nc(1) or bash /dev/tcp.
20.  The difference between "Connection refused", "Connection timed out", and "Name or service not known/host not found".
21.  Be able to use dig(1), nslookup(1) and host(1) and understand why they don't care about what you put into /etc/hosts.
22.  Understand [basic DNS resolution](https://youtu.be/z55ULZcKP8A). I.e., lookups from client->stub resolver->resolver and resolvers<->auths.
23.  Understand domain registration, NS records, TTLs, and zone delegation. Grasp the [difference in threat model between plain DNS, DoH, and DNSSEC](https://www.netmeister.org/blog/doh-dot-dnssec.html).
24.  Understand cache poisoning as a concept and as applied to different protocols, such as ARP, DNS, HTTP Proxy, ...
25.  Have a general awareness of the [physical internet](https://youtu.be/4YrHdD1uIxs), [peering, ASNs](https://youtu.be/OOq7jGlhBjY), BGP hijacking, and how (and when) governments can (and do) censor or intercept/inspect (parts of) the internet for their jurisdiction.
26.  [How to use](https://www.baeldung.com/linux/strace-command) ktrace(1) / strace(1) / dtrace(1) to figure out just [what files or sockets](https://opensource.com/article/19/10/strace) a program is accessing.
27.  Be [able to use](https://bytexd.com/how-to-use-nmap/) nmap(1) to [identify a host's open ports and fingerprint](https://www.yeahhub.com/top-30-basic-nmap-commands-beginners/) them.
28.  Be able to [use SSH port forwarding](https://www.cyberciti.biz/faq/linux-unix-ssh-proxycommand-passing-through-one-host-gateway-server/), SSH pubkey options (from=, command= / ForceCommand), ProxyCommand, and use of [SSH agents](http://unixwiz.net/techtips/ssh-agent-forwarding.html).
29.  [Basic Unix skills](https://missing.csail.mit.edu/2020/data-wrangling/), pipes and common tools: grep(1), sed(1), awk(1), sort(1), uniq(1), diff(1), comm(1), tr(1), ...
30.  Know how to use [screen(1)](https://youtu.be/vxTXXaCr4s8) / [tmux(1)](https://danielmiessler.com/study/tmux/) to keep long sessions uninterrupted, to resume if needed, to juggle multiple remote terminals in a single window.
31.  _Really_ understand the [Unix permissions model](https://youtu.be/YlcF3ncTQpo): owner, group, others; permissions on directories (e.g., 1777, 0711), Unix groups; su(1) and sudo(1); how setuid/setgid works.
32.  Understand TOCTOU attacks, [mktemp(3), and umask(2)](https://www.netmeister.org/blog/mktemp.html).
33.  Be able to convert timestamps between formats and know to look for UTC offset when correlating log entries.
34.  Enough [shell scripting](https://bash.cyberciti.biz/guide/Main_Page) to automate the execution of repeated commands, including flow control using loops, functions, and variable expansion.
35.  Enough Python, Perl, PHP, C, Go, Java, and JavaScript to be able to read all the random code you come across and at least make some sense of it.
36.  Enough C to understand how a [buffer overflow works](http://phrack.org/issues/49/14.html) and how to spot one. (90% of the time a sprintf(3) of a user-generated string into a fixed-size buffer.)
37.  [Enough SQL](https://www.w3schools.com/sql/) to be able to explain [Little Bobby Tables](https://xkcd.com/327/) and to pull records from multiple tables.
38.  Enough input- and shell meta-characters escaping to detect, abuse, and fix unsanitized system(3) / popen(3) [command](https://owasp.org/www-community/attacks/Command_Injection)-[injections](https://www.cs.rutgers.edu/~pxk/419/notes/cmd-injection.html) (in the various languages).
39.  Be able to efficiently use your preferred packaged manager to identify file/package ownership, dependencies, package integrity. Be able to create a package in your commonly used package manager format (.deb, .rpm, ...) for a non-trivial piece of software to understand packaging, install scripts, signatures, validation etc.
40.  [Enough AWS](https://docs.aws.amazon.com/cli/latest/userguide/cli-chap-configure.html)* to be able to spin up an instance when needed. Grok the difference between NACLs and Security Groups. Be able to manage simple IAM resources and to inspect and [lock down an S3 bucket](https://securingthe.cloud/aws/how-to-secure-aws-s3-latest-best-practices/).  
    *Azure, GCP, whatever, although, honestly, AWS remains the 600 lb gorilla, so...
41.  Enough [Kerberos](https://twitter.com/jschauma/status/643444266300239873) to understand the [concept of client authentication versus service authorization](https://www.roguelynn.com/words/explain-like-im-5-kerberos/) and [replay attacks](https://web.mit.edu/kerberos/dialogue.html).
42.  [Enough PGP](https://gnupg.org/gph/en/manual.html) to be able to send/receive, [encrypt/decrypt, and sign/verify](https://www.devdungeon.com/content/gpg-tutorial) encrypted and signed messages.
43.  Understand [SMTP basics](https://youtu.be/Ai8rjqelwsI), email headers, etc. Know enough about [SPF/DKIM/DMARC](https://youtu.be/KwCmv3GHGfc) to identify those headers and understand what they are telling you.
44.  Shamir's 3 Laws of Cryptography:
    -   Absolutely secure systems do not exist
    -   To halve your vulnerability, you have to double your expenditure
    -   Cryptography is typically bypassed, not penetrated
45.  Schneier's Law (_Any person can invent a security system so clever that she or he can't think of how to break it._) and not to attempt to invent your own cryptographic protocol.
46.  Be able to explain core concepts like Zero Trust, Defense in Depth, Least Privilege, Failing Closed, and Kerckhoff's Principle vs. Security by Obscurity.
47.  How containers are different from virtual machines, and what their respective trust- and control boundaries are.
48.  How to file [an actionable, useful bug report](http://infiniteundo.com/post/36678096413/how-to-write-a-bug-report). Know how to [manage](https://twitter.com/jschauma/status/1237578053456293888) your own [ticket queue](https://twitter.com/jschauma/status/1007075536202620928).
49.  When to seek input from others: there's not just domain specific, but plenty of general security expertise outside of the information security team.
50.  Nothing, absolutely nothing about cryptocurrencies. "Crypto" means "cryptography". That's all you need to know.

[![Screenshot from Wikipedia's page on
Cryptosporidiosis, noting that 'crypto is a parasitic
disease'](https://www.netmeister.org/blog/images/crypto-disease.png "Crypto is a parasitic disease, alright.")](https://en.wikipedia.org/wiki/Cryptosporidiosis)