# OnFrontiers Python SDK

Client utilities for interacting with the official **OnFrontiers GraphQL API**.

This SDK provides both synchronous and asynchronous Python clients to authenticate and interact with the OnFrontiers API using GraphQL queries and mutations. It is designed to be easy to use, extensible, and compatible with modern Python tooling.

## 🔧 Features

-   Authenticate using email/password with optional external auth
-   Synchronous and asynchronous clients (`OnFrontiers`, `AsyncOnFrontiers`)
-   Auto-configured GraphQL client with Bearer token
-   Clean abstraction over the [`gql`](https://github.com/graphql-python/gql) library

## 🚀 Installation

```bash
pip install onfrontiers
```

## 🔐 Authentication

You can authenticate using an OnFrontiers email and password:

```python
from onfrontiers import auth_username_password

token = auth_username_password(
    email="your.email@domain.com",
    password="your-password"
)
```

For asynchronous use:

```python
import asyncio
from onfrontiers import async_auth_username_password

async def get_token():
    token = await async_auth_username_password(
        email="your.email@domain.com",
        password="your-password"
    )
    return token

token = asyncio.run(get_token())
```

You may optionally pass:

-   `client_id`: A custom client identifier (defaults to `"python-sdk"`)
-   `external_auth_token`: An optional external token to delegate auth
-   `url`: Override the default OnFrontiers API endpoint

## 🧠 Usage

### Synchronous Client

```python
from onfrontiers import OnFrontiers
from gql import gql

client = OnFrontiers(access_token=token)

query = gql("""
    query GetCurrentUser {
        currentUser {
            id
            email
        }
    }
""")

result = client.execute(query)
print(result["currentUser"])
```

### Asynchronous Client

```python
from onfrontiers import AsyncOnFrontiers
from gql import gql
import asyncio

async def run():
    client = AsyncOnFrontiers(access_token=token)

    query = gql("""
        query GetCurrentUser {
            currentUser {
                id
                email
            }
        }
    """)

    result = await client.execute(query)
    print(result["currentUser"])

asyncio.run(run())
```

## 🧪 Requirements

-   Python 3.10+

## 🌍 Endpoint

By default, all clients communicate with <https://api.onfrontiers.com/graphql>

Use the `url` parameter to override this for testing or development environments.

## 🛠 Development

Install all the dependencies:

```bash
uv sync
```

To run tests:

```bash
pytest
```

## 🧾 License

This SDK is provided and maintained by OnFrontiers. All rights reserved.

## 🤝 Support

For questions, contact [support@onfrontiers.com](mailto:support@onfrontiers.com).
