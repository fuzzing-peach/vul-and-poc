# CVE Collection

| target  | BUG/CVE                                                | type        | findBy                         |
| ------- | ------------------------------------------------------ | ----------- | ------------------------------ |
| wolfssl | [CVE-2022-38152](wolfssl/CVE-2022-38152)               | SEG         | tlspuffin                      |
| wolfssl | [CVE-2022-38153](wolfssl/CVE-2022-38153)               | DOUBLE FREE | tlspuffin                      |
| wolfssl | [CVE-2022-39173](wolfssl/CVE-2022-39173)               | BUF         | tlspuffin                      |
| wolfssl | [CVE-2022-39173](wolfssl/CVE-2022-39173)               | BUF         | tlspuffin                      |
| wolfssl | [CVE-2022-42905](wolfssl/CVE-2022-42905)(9.1 critical) | BUF         | [tlspuffin](tlspuffin-wolfssl) |
| openssl | [CVE-2021-3449]()                                      |             |                                |
| unzip   | [CVE-2021-4217](unzip/CVE-2021-4217)                   | SEG         |                                |


openssl 的 cve 主要集中在字段解析、外部文件（证书、公钥）载入时遇到的 malformed content 导致的 mem corruption。

[tlspuffin-wolfssl]: https://blog.trailofbits.com/2023/01/12/wolfssl-vulnerabilities-tlspuffin-fuzzing-ssh/ "wolfssl-vulnerabilities-tlspuffin-fuzzing-ssh"

![wolfssl-vulnerabilities-tlspuffin-fuzzing-ssh](https://picgo.kendrickzou.com/images/202411071714229.png)