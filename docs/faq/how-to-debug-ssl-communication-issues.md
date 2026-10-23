# How to debug SSL communication issues?

| Date       | Category    |
|------------|-------------|
| 2023-10-24 15:55:24 | Simulation Troubleshoot |




# How to debug SSL communication issues?

Users operating within corporate networks, through a VPN, or behind a proxy server may sometimes encounter SSL errors when running the `tidy3d` python client in their local machines. **Note you can always use the python client with [our cloud-hosted notebook server](https://tidy3d.simulation.cloud/).**

These errors can occur because the corporate network's security measures, intercepts, and re-encrypts HTTPS traffic.

A common error message looks like this:

```bash
requests.exceptions.SSLError: HTTPSConnectionPool(host='tidy3d-api.simulation.cloud', port=443): Max retries exceeded with url: ... (Caused by SSLError(SSLCertVerificationError(1, '[SSL: CERTIFICATE_VERIFY_FAILED] certificate verify failed: unable to get local issuer certificate ...')))
```

Note that sometimes, SSL errors can also manifest as authentication errors, or communication timeout errors.

In this FAQ, we will overview some steps to help you debug and resolve this issue.

## Step 0: Windows quick fix
Sometimes on Windows running the following will resolve the problem right away. Try this first:
```bash
pip install pip-system-certs
```
If this doesn't work, proceed with the rest of this guide.

## Step 1: The Recommended & Most Secure Solution

The most robust and secure solution is to make sure your system trust store includes the root certificate that our servers use. This allows your machine to verify our servers' identity correctly without disabling security features.

**Action**: Please ask your network administrator to whitelist the API endpoint `https://tidy3d-api.simulation.cloud` and make sure the system trust store includes the root certificate it chains to, Amazon Root CA 1: [https://www.amazontrust.com/repository/AmazonRootCA1.pem](https://www.amazontrust.com/repository/AmazonRootCA1.pem)

If your network inspects HTTPS traffic, your IT team must also install the network's own inspection root certificate. Then point Python at a bundle that contains it by setting `REQUESTS_CA_BUNDLE` to the bundle path.

**If you followed an earlier version of this FAQ:** it linked to a full certificate bundle (`cacert.pem`) from the `tidy3d` repository. That bundle is an old copy of the `certifi` package and trusts certificate authorities that are no longer trusted, including emSign ECC Root CA - G3. Please remove that bundle from any system trust store and trust Amazon Root CA 1 instead. We also recommend updating certifi in each Python environment where you use Tidy3D:

```bash
python -m pip install --upgrade "certifi>=2026.10.19"
```

If these steps do not resolve your issue, please contact our support team and provide the logs from the commands you have tried.


## Step 2: Verify Your Environment and Connectivity

Before changing any settings, let's make sure you can reach the Tidy3D servers.

**Test connectivity using `ping`**. This helps confirm if the issue is with SSL verification or basic network access. You should run these commands from your command line (Terminal, PowerShell, or the Anaconda Prompt). 

* Test connection to the web server:

  ```bash        
  ○ → ping -c 3 tidy3d.simulation.cloud
  PING tidy3d.simulation.cloud (3.160.231.60) 56(84) bytes of data.
  64 bytes from server-3-160-231-60.mad53.r.cloudfront.net (3.160.231.60): icmp_seq=1 ttl=245 time=58.7 ms
  64 bytes from server-3-160-231-60.mad53.r.cloudfront.net (3.160.231.60): icmp_seq=2 ttl=245 time=77.9 ms
  64 bytes from server-3-160-231-60.mad53.r.cloudfront.net (3.160.231.60): icmp_seq=3 ttl=245 time=69.2 ms

  
  3 packets transmitted, 3 received, 0% packet loss, time 2002ms
  rtt min/avg/max/mdev = 58.661/68.594/77.930/7.877 ms
  ```

* Test connection to the API endpoints:

  ```bash        
  ○ → curl -X GET https://tidy3d-api.simulation.cloud
  {
    "error" : "Unauthorized",
    "detail" : "Access is denied",
    "code" : "401",
    "httpStatus" : "401 UNAUTHORIZED",
    "warning" : ""
  }
  ```

  **Expected output:** A `401 Unauthorized` error message. This is good news; it means you can reach our API server, and the problem is likely with authentication or SSL certificate verification.

Note that many networks can block ping messages so this is not a foolproof check.

## Step 3: Disable SSL Verification (Diagnosis Only)

**Only to confirm that SSL verification is the cause**, you can instruct `tidy3d` to skip SSL certificate verification. Turn it back on as soon as you have your answer. With verification off, anyone who can intercept your network traffic can read your API key and your simulation data.

In `tidy3d` 2.11 and later, set the `TIDY3D_WEB__SSL_VERIFY` environment variable to `false`. Version 2.12 ignores the older `TIDY3D_SSL_VERIFY` variable.

#### Setting the Environment Variable:

* **On Windows (in Command Prompt)**:

  ```bash
  set TIDY3D_WEB__SSL_VERIFY=false
  ```

* **On macOS or Linux (in a bash terminal)**:

  ```bash
  export TIDY3D_WEB__SSL_VERIFY="false"
  ```

Do not set it permanently. Remove it with `set TIDY3D_WEB__SSL_VERIFY=` on Windows or `unset TIDY3D_WEB__SSL_VERIFY` on macOS or Linux once you are done.

#### Verifying the Setting:

**It is essential to check the setting within the environment where you run your script.** Inside Python, run:

```python
from tidy3d.config import config
print(f"SSL verification enabled: {config.web.ssl_verify}")
```

The output should be `False` while the workaround is active.

## Step 4: Run the Connection Diagnostics

If the issue persists, run the built-in diagnostics (`tidy3d` 2.12 and later) from the same environment where you use `tidy3d`:

```bash
tidy3d diagnose-connection
```

It checks the network path, API health, authentication, latency and storage downloads, and prints a summary with recommended next steps. For certificate errors it suggests the fix. The output can include network details such as proxy settings, certificate paths and resolved IP addresses, so review it before sharing it. Please include it when you contact our support team.
