# Test Results
Python version used: 3.12.3 | Operating system: Linux Mint | Date: 8 Nov 2026.

| # | Input | Expected result | Actual result | Pass/Fail |
|---|-------|-----------------|---------------|-----------|
| 1 | https://www.example.com/login | No listed warning signs | No listed warning signs found. This does NOT prove safety. | PASS |
| 2 | http://192.0.2.10/account | IP address + HTTP | Uses an IP address...; Uses HTTP... | PASS |
| 3 | http://example.com@sample.invalid/login | @ symbol + HTTP | Contains an @ symbol...; Uses HTTP... | PASS |
| 4 | https://a.b.c.d.e.example.invalid/path | Many hostname segments | Contains many hostname segments/subdomains. | PASS |
| 5 | https://xn--example.invalid/ | Punycode-style hostname | Contains a punycode-style hostname. | PASS |

## Bonus checks
| Input | Result |
|-------|--------|
| (empty) | No URL entered. |
| www.example.com | Uses HTTP. HTTPS alone does not prove trust. |
| https://secure-login.example.invalid | No listed warning signs found (tricky name slips through) |
| http://[bad | This text is not a valid URL format. (no crash after Improvement C) |

## Notes
I learned that a URL can be split into parts like the scheme, hostname and path, and that the hostname is the most important part to read. The @ symbol check was interesting because the browser ignores everything before it, so a link can look like one site but go to another. What surprised me was that https://secure-login.example.invalid showed no warning signs even though the name sounds suspicious, so no warnings does not mean a link is safe. I also found that typing http://[bad crashed the program until I added try/except to handle it.