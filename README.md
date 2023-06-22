# CVE-2023-35840
elFinder < 2.1.62 - Path Traversal vulnerability in PHP LocalVolumeDriver connector

## Description

Path Traversal vulnerability in PHP LocalVolumeDriver connector. This vulnerability can be exploited by allowing untrusted users to write to the local file system.

Vulnerability exists in `target` parameter which contains a base64 encoded path. For exmpample path `pentest` is encoded as:
```
1_cGVudGVzdA==
```

If we skip `l1_` as it looks to be a constant prefix rest can be decoded as:
```
pentest
```

Therefore we can modify it to:
```
pentest/../../
```

And then encode it as:
```
l1_cGVudGVzdC8uLi8uLi8=
```
With `target` parameter set to this value we can write arbitary files to application root folder.


This issue was caused by incomplete validity checking of the supplied request parameters. That problem has been fixed in elFinder Version 2.1.62.

## Affected versions
< 2.1.62

## Advisory
Update elFinder to 2.1.62 or newer.

### References
* https://github.com/Studio-42/elFinder/security/advisories/GHSA-wm5g-p99q-66g4
* https://nvd.nist.gov/vuln/detail/CVE-2023-35840
