---
title: How to debug SSL communication issues?
date: 2023-10-24 15:55:24
enabled: true
category: "Simulation Troubleshoot"
---


# How to debug SSL communication issues?

Users operating within corporate networks, through a VPN, or behind a proxy server may sometimes encounter SSL errors when running the `tidy3d` python client in their local machines. **Note you can always use the python client with [our cloud-hosted notebook server](https://tidy3d.simulation.cloud/).**

These errors can occur because the corporsate network's security measures intercept and re-encrypt HTTPS traffic required for the `tidy3d` python client to communicate with the simulation servers.


A common error message looks like this:

```bash
requests.exceptions.SSLError: HTTPSConnectionPool(host='tidy3d-api.simulation.cloud', port=443): Max retries exceeded with url: ... (Caused by SSLError(SSLCertVerificationError(1, '[SSL: CERTIFICATE_VERIFY_FAILED] certificate verify failed: unable to get local issuer certificate ...')))
```

Note that sometimes, SSL errors can also manifest as authentication errors, or communication timeout errors.

In this FAQ, we will overview some steps to help you debug and resolve this issue.


## Step 1: Verify Your Environment and Connectivity

Before changing any settings, let's make sure you can reach the Tidy3D servers.


**Test connectivity using `ping`**. This helps confirm if the issue is with SSL verification or basic network access. You should run these commands from your command line (Terminal, PowerShell, or the Anaconda Prompt). 

      * Test connection to the web server:

        ```bash        
        ○ → ping -c 3 tidy3d.simulation.cloud
        PING tidy3d.simulation.cloud (3.160.231.60) 56(84) bytes of data.
        64 bytes from server-3-160-231-60.mad53.r.cloudfront.net (3.160.231.60): icmp_seq=1 ttl=245 time=58.7 ms
        64 bytes from server-3-160-231-60.mad53.r.cloudfront.net (3.160.231.60): icmp_seq=2 ttl=245 time=77.9 ms
        64 bytes from server-3-160-231-60.mad53.r.cloudfront.net (3.160.231.60): icmp_seq=3 ttl=245 time=69.2 ms

        --- tidy3d.simulation.cloud ping statistics ---
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


## Step 2: Disable SSL Verification (Quick Workaround)

As a temporary solution, you can instruct `tidy3d` to bypass SSL certificate verification. This is not ideal for security but is useful for confirming the source of the problem.

This is done by setting the `TIDY3D_SSL_VERIFY` environment variable to `false`.

#### Setting the Environment Variable:

  * **On Windows (in Command Prompt)**:

    ```bash
    set TIDY3D_SSL_VERIFY=false
    ```

    To set it permanently, use `setx TIDY3D_SSL_VERIFY false`.

  * **On macOS or Linux (in a bash terminal)**:

    ```bash
    export TIDY3D_SSL_VERIFY="false"
    ```

#### Verifying the Environment Variable:

**It is essential to ensure the variable is set correctly within the environment where you run your script.**

  * **In your terminal**, run the following command.

      * Windows: `echo %TIDY3D_SSL_VERIFY%`
      * macOS/Linux: `echo $TIDY3D_SSL_VERIFY`
      * The output should be `false`.

  * **Inside your Python script**, add these lines to the top to see what value the script is reading:

    ```python
    import os
    print(f"TIDY3D_SSL_VERIFY is set to: {os.getenv('TIDY3D_SSL_VERIFY')}")
    ```

    When you run your script, you should see the confirmation printed. If you see `None` or an empty string, the variable was not set correctly in your current session.


## Step 3: Run a Diagnostic Script

If the issue persists, running a minimal script can help isolate the problem to the `requests` library, which `tidy3d` uses for communication.

1.  Save the following code as a Python file (e.g., `test_connection.py`).
2.  Set the `TIDY3D_API_KEY` and `TIDY3D_SSL_VERIFY` environment variables in your terminal as shown in Step 2.
3.  Run the script with `python test_connection.py`.

<!-- end list -->

```python
# test_connection.py
import os
import requests
from tidy3d.web.core.constants import HEADER_APIKEY
from tidy3d.web.core.environment import Env

def auth(req):
    """Adds the API key to the request header."""
    # Ensure TIDY3D_API_KEY is set in your environment
    req.headers[HEADER_APIKEY] = os.getenv("TIDY3D_API_KEY")
    return req

# Let tidy3d's environment configuration read the SSL variable
# It reads from the TIDY3D_SSL_VERIFY environment variable.
ssl_verify_setting = Env.current.ssl_verify

print(f"API Endpoint: {Env.current.web_api_endpoint}")
print(f"SSL Verification Enabled: {ssl_verify_setting}")

if not ssl_verify_setting:
    # Suppress the warning that will be printed for unverified requests
    requests.packages.urllib3.disable_warnings(requests.packages.urllib3.exceptions.InsecureRequestWarning)
    print("InsecureRequestWarning suppressed.")

try:
    resp = requests.get(
        f"{Env.current.web_api_endpoint}/apikey", auth=auth, verify=ssl_verify_setting
    )

    print(f"Status Code: {resp.status_code}")
    print(f"Response Content: {resp.content}")

except requests.exceptions.SSLError as e:
    print(f"\nCaught an SSLError. This is the core issue.\nDetails: {e}")

except Exception as e:
    print(f"\nAn unexpected error occurred: {e}")

```

With `TIDY3D_SSL_VERIFY` set to `false` and `TIDY3D_API_KEY` set correctly, the expected output is a `status code: 200` and content containing your API key. You will also see an `InsecureRequestWarning` if you don't suppress it.


## Step 4: The Recommended & Most Secure Solution

The most robust and secure solution is to have your IT department add the Tidy3D SSL certificate to your system's trust store. This allows your machine to verify our servers' identity correctly without disabling security features.

  **Action**: Please ask your network administrator to whitelist the API endpoint `https://tidy3d-api.simulation.cloud` and install the following root certificate [https://github.com/flexcompute/tidy3d/blob/develop/tidy3d/web/api/cacert.pem](https://github.com/flexcompute/tidy3d/blob/develop/tidy3d/web/api/cacert.pem)

If these steps do not resolve your issue, please contact our support team and provide the logs from the commands you have tried.
