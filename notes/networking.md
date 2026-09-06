
### **HTTP(S)**: HyperText Transfer Protocol (Secured)

HTTP is the **set of rules** used for communicating with web servers for the transmitting of webpage data, wheter it's HTML, images, videos, etc.

HTTPS is the **secure version** of HTTP. All data sent and received is encrypted, which helps stop people from seeing the data or impersonating the web server being used.

#### URL

**What is a URL? (Uniform Resource Locator)**
A URL is the detailed address used to know how to access a resource on the internet.
  
- **Protocol:** The rules used for communication, such as HTTP, HTTPS or FTP (File Transfer Prototcol)

- **Host/Domain/Subdomain:** The name of the website or server being accessed.

- **Port:** The Port that you are going to connect to, usually 80 for and 443 for HTTPS, but this can be hosted on any port between 1 - 65535.

- **Path:** The file name or location of the resource you are trying to access.

- **Query:** Marks the beginning of the query string using `?`.

- **Parameters:** Extra values sent to the web server, usually in a `key=value` format.

- **Fragments:** Refers to a specific section or part of a webpage using `#`.

![URL Schema](../../Assets/Images/url_schema.png)
#### Making a Request:

It is possible to make a request to a web server with just one line `GET / HTTP/1.1`

>**GET:** Request method
>**"/":** Path/resource being requested
>**HTTP/1.1:** HTTP protocol version

##### Example:

```
GET /login HTTP/1.1

Host: example.com
User-Agent: Mozilla/5.0 Firefox/87.0
Referer: https://example.com/
```

Requests:

```
https://example.com/login
```

- `/` = root page
- `/login` = login page

##### Example Response:

```
HTTP/1.1 200 OK

Server: nginx/1.15.8
Date: Fri, 09 Apr 2021 13:34:03 GMT
Content-Type: text/html
Content-Length: 156
```

```
<html>
<head>
    <title>Example Login</title>
</head>
<body>
    <h1>Login</h1>

    <form action="/login" method="POST">
        <label>Username:</label>
        <input type="text" name="username">

        <label>Password:</label>
        <input type="password" name="password">

        <button type="submit">Login</button>
    </form>
</body>
</html>
```


#### HTTP methods:

- **GET Request**  
  Used for getting information from a web server.  
  *Example: Viewing a news article*

- **POST Request**  
  Used for submitting data to a web server and creating new data.  
  *Example: Creating a new user account*

- **PUT Request**  
  Used for submitting data to a web server to update existing information.  
  *Example: Updating your email address*

- **DELETE Request**  
  Used for deleting information/data from a web server.  
  *Example: Removing a picture uploaded to your account*


#### HTTP Status Codes

![HTTP Status Codes](../../Cheatsheets/HTTP%20Status%20Codes.md)


#### Headers

Headers are additional bits of data you can send to the web server when making requests.

**Common Request Headers**

These headers are sent from the client to the server.

**Host:** 

**User-Agent:**

****
### Network:

```192.168.0.0/16```

//
### Subnet: 

```
192.168.1.0/24
192.168.2.0/24
192.168.3.0/24
```

//


## ICMP

**Internet Control Message Protocol**

It is used to communicate error information or updates between network devices. 
For example `ping` and `traceroute` use ICMP messages to collect latency information or locate the source of a network delay.

ICMP can be exploited to perform DOS (Denial Of Service) attacks. 
Here are some example uses:
- **ping sweep**


- **ping flood**

- **smurf attack** (Attacker spoofs victims IP, sends a huge amount of ICMP echo request messages to a network's broadcast address¹. Many hosts on that network will reply with ICMP echo replies to the target. This huge amount of information will overwhelm the victim with traffic causing a DOS.)

¹*broadcast address: a broadcast address is an IP address used to send a packet to every host on a local subnet at once* 

#### **DNS**: Domain Name System

DNS maps human-readable names to IP addresses.
 `google.com -> 142.250.72.14`

#### Domain structure:

Ex: `mail.google.com`

**TLD** (Top Level Domain): `com`
	**g**TLD = general TLD (.com / .net / .org etc)
	**cc**TLD = country code TLD (.ch / .fr / .ca etc)
**Second-Level Domain**: `google`
**Subdomain**: `mail`

#### DNS Records

##### A Record
Points names to servers (IPv4).
Example:
	`example.com -> 104.26.10.229`
##### AAAA Record
Points names to servers (IPv6).
Example:
	`example.com -> 2606:4700:20::681a:be5`
#### CNAME Record
Resolves to another domain.
Example:
	`store.example.com -> shops.shopify.com`
#### MX Record
MX = Mail Exchange, Resolves to the address of the servers that handle the email for the queried domain.
Example:
	`example.com → alt1.aspmx.l.google.com` | That means Google handles the mail
#### TXT Record
Free text fields where text-based information data can be stored. TXT records have multiple uses, here are some common ones:

- **SPF** (Sender Policy Framework, "These servers are allowed to send emails for my domains.", without it attackers could more easily fake `from: support@yourbank.com`)
	`@ TXT "v=spf1 ip4:192.0.2.0/24 include:_spf.google.com include:amazonses.com ~all"` | Google's mail servers can send emails for this domain
- **DMARC** (Domain-based Message Authentication, Reporting and Conformance, "What should receiving mail servers do if SPF/DKIM checks fail?", works with SPF to help prevent email spoofing and phishing.)
	`_dmarc.example.com TXT "v=DMARC1; p=reject; rua=mailto:dmarc-reports@example.com; adkim=s; aspf=s; pct=100"` | If an email claiming to be from `example.com` fails SPF/DKIM validation reject it completely and send authentication reports to `dmarc-reports@example.com`
- **domain verification** 
  Used to prove ownership of a domain to a service.
- **anti-spam rules**
  TXT records help reduce fake or malicious emails.
- **ownership checks**
  Similar to domain verification.
  

#### What happens when you make a DNS request ?

1. When a request is made the device first checks for local cache to see if the address has been looked up recently. If not, the request is sent to a Recursive DNS Server.
2. The Recursive DNS Server checks its own cache for the requested domain name. If it cannot find the record, it contacts the Root DNS Server.
3. The Root Server directs the resolver to the correct Top Level Domain (TLD) server based on the domain extension (such as `.com`).
4. The TLD server then points the resolver to the domain’s Authoritative Nameserver.
5. The Authoritative Nameserver contains the DNS records for the domain and returns the correct IP address.
6. The Recursive DNS Server caches the result temporarily using the TTL (Time To Live) value and sends the IP address back to the client device.
7. The client device can now use the IP address to connect to the requested website or service.

![DNS Schema](../../Assets/Images/dns_schema.png)

#### Perform DNS requests

You can use the `nslookup` command to query DNS records and retrieve information about a domain.

**Basic Syntax**:
`nslookup --type=TYPE domain`
- `TYPE` = the DNS record type to query (optional)
- `domain` = the target domain name

**Alternative Tool:**
`dig` is another popular DNS lookup tool that provides more detailed output
`dig TYPE domain`
`dig domain`

