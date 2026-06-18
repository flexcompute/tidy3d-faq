# Web.account?

| Date       | Category    |
|------------|-------------|
| 2025-09-16 13:50:36 | Web API |



[`web.account`](https://docs.flexcompute.com/projects/tidy3d/en/latest/api/_autosummary/tidy3d.web.account.html) is a helper function that retrieves **account details** for the currently authenticated user. It shows your FlexCredit balance, expiration dates, and limits on daily free simulations.

## Example


```python
from tidy3d import web

# Get account information
account_info = web.account()
```



Example output:



```python
Current FlexCredit balance: 10.00 and expiration date: 2024-12-31 23:59:59. Remaining daily free simulations: 3.

# available FlexCredit balance:
available_flexcredits = account_info.credit

# expiration date
expiration = account_info.credit_expiration
```


