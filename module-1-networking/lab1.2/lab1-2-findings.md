# Lab 1.2 Findings

## TLS Certificate Analysis
- **Subject:** C = IN, ST = Karnataka, L = Bangalore, O = InstaSafe Lab, CN = 92.4.73.213
- **Issuer:** C = IN, ST = Karnataka, L = Bangalore, O = InstaSafe Lab, CN = 92.4.73.213
- **Validity (Expiry):** 365 days from generation
- **Public Key Algorithm:** rsaEncryption (RSA-2048)
- **Signature Algorithm:** sha256WithRSAEncryption

## Explanation

### Why does `curl` without `-k` fail against this server?
When the https connection is being started, curl checks the servers SSL/TLS certificate so as to confirm its identity. The certificate on my Nginx server is self-signed, and not igned by any cryptographical method by a recognised legitimate Certificate Authority (CA). This leads to curl command not being able to establish a chain of trust. So, to prevent any Man in Middle attacks, the connection is immediately stopped. In this scenario, the -k flag tells curl to ignore this problem and proceed with the unsafe encrypted connection anyway.

### What would need to change to make it succeed without `-k`?
If I want to succeed without using -k, i would have to use one of two methods:
- Either register a legitimate domain name and bind and point it to my VM's IP (92.4.73.213)
- Or get a proper legitimate certificate from a recognised CA which is properly issued and automatically configured with a globally recognised cryptographic signature.
