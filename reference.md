# Reference
## API Keys
<details><summary><code>client.api_keys.<a href="src/wavix/api_keys/client.py">list</a>(...) -> typing.List[ApiKey]</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Returns the API keys belonging to the authenticated account.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```python
from wavix import Wavix
from wavix.environment import WavixEnvironment

client = Wavix(
    token="<token>",
    environment=WavixEnvironment.DEFAULT,
)

client.api_keys.list(
    label="production",
)

```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**label:** `typing.Optional[str]` — Filters API keys by `label`. Matches partial values.
    
</dd>
</dl>

<dl>
<dd>

**request_options:** `typing.Optional[RequestOptions]` — Request-specific configuration.
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.api_keys.<a href="src/wavix/api_keys/client.py">create</a>(...) -> ApiKeyWithSecret</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Creates an API key for the authenticated account. Restrict access by listing permitted IP addresses in `permitted_ips`.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```python
from wavix import Wavix, ApiKeyScopePermission, ApiKeyCallsScopePermission
from wavix.environment import WavixEnvironment

client = Wavix(
    token="<token>",
    environment=WavixEnvironment.DEFAULT,
)

client.api_keys.create(
    label="Production API Key",
    active=True,
    restricted=True,
    permitted_ips=[
        "192.168.1.1",
        "10.0.0.1"
    ],
    scopes_enabled=True,
    numbers=ApiKeyScopePermission(
        allow="read",
    ),
    calls=ApiKeyCallsScopePermission(
        allow="read",
    ),
    messages=ApiKeyScopePermission(
        allow="write",
    ),
    two_fa=ApiKeyScopePermission(
        allow="write",
    ),
    billing=ApiKeyScopePermission(
        allow="read",
    ),
)

```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**label:** `str` — API key label.
    
</dd>
</dl>

<dl>
<dd>

**active:** `typing.Optional[bool]` — Indicates whether the API key should be activated upon creation.
    
</dd>
</dl>

<dl>
<dd>

**restricted:** `typing.Optional[bool]` — Indicates whether to restrict API key access by IP address. When enabled, only requests from IP addresses listed in `permitted_ips` are allowed.
    
</dd>
</dl>

<dl>
<dd>

**permitted_ips:** `typing.Optional[typing.List[str]]` — List of permitted IP addresses for this API key. Each must be a valid IPv4 address. Required when `restricted` is true.
    
</dd>
</dl>

<dl>
<dd>

**scopes_enabled:** `typing.Optional[bool]` 

When `true`, scope fields below are enforced. When `false` (default), the
key has full access. Omitted scope fields default to `{ allow: none }`,
so with `scopes_enabled: true` and no scopes set the key has no access.
    
</dd>
</dl>

<dl>
<dd>

**numbers:** `typing.Optional[ApiKeyScopePermission]` — View, buy, release, and configure phone numbers, browse inventory, and manage the cart.
    
</dd>
</dl>

<dl>
<dd>

**trunks:** `typing.Optional[ApiKeyScopePermission]` — View, create, update, and delete SIP trunks and their settings.
    
</dd>
</dl>

<dl>
<dd>

**calls:** `typing.Optional[ApiKeyCallsScopePermission]` — Access call records and active calls, and control live call actions such as starting, answering, ending, audio playback, DTMF, streaming, and transcription requests.
    
</dd>
</dl>

<dl>
<dd>

**messages:** `typing.Optional[ApiKeyScopePermission]` — Access message history and Sender IDs, send messages, manage opt-outs, and create or delete Sender IDs.
    
</dd>
</dl>

<dl>
<dd>

**recordings:** `typing.Optional[ApiKeyScopePermission]` — List, download, and delete call recordings.
    
</dd>
</dl>

<dl>
<dd>

**campaigns:** `typing.Optional[ApiKeyScopePermission]` — View campaign analytics and Sender ID or Brand status, schedule bulk voice or SMS campaigns, register Brands, and create short links.
    
</dd>
</dl>

<dl>
<dd>

**two_fa:** `typing.Optional[ApiKeyScopePermission]` — View 2FA service details and verification logs, trigger OTPs by voice or SMS, and validate verification codes.
    
</dd>
</dl>

<dl>
<dd>

**validator:** `typing.Optional[ApiKeyScopePermission]` — View number validation results and trigger single or bulk validation or HLR lookup requests.
    
</dd>
</dl>

<dl>
<dd>

**webhooks:** `typing.Optional[ApiKeyScopePermission]` — List, create, and delete webhooks.
    
</dd>
</dl>

<dl>
<dd>

**embeddable:** `typing.Optional[ApiKeyScopePermission]` — Manage widget tokens, including listing, viewing, creating, updating, and deleting them.
    
</dd>
</dl>

<dl>
<dd>

**billing:** `typing.Optional[ApiKeyScopePermission]` — Access statements, balance, payment methods, usage reports, and billing settings, including payment method updates.
    
</dd>
</dl>

<dl>
<dd>

**account:** `typing.Optional[ApiKeyScopePermission]` — View and update account profile information and timezone.
    
</dd>
</dl>

<dl>
<dd>

**subaccounts:** `typing.Optional[ApiKeyScopePermission]` — Manage subaccounts: list and view them, create, update, and suspend them.
    
</dd>
</dl>

<dl>
<dd>

**request_options:** `typing.Optional[RequestOptions]` — Request-specific configuration.
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.api_keys.<a href="src/wavix/api_keys/client.py">delete</a>(...) -> SuccessResponse</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Deletes the API key identified by `id`. Deletion is permanent and revokes the key immediately.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```python
from wavix import Wavix
from wavix.environment import WavixEnvironment

client = Wavix(
    token="<token>",
    environment=WavixEnvironment.DEFAULT,
)

client.api_keys.delete(
    id=1,
)

```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**id:** `int` — The unique ID of the API key.
    
</dd>
</dl>

<dl>
<dd>

**request_options:** `typing.Optional[RequestOptions]` — Request-specific configuration.
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.api_keys.<a href="src/wavix/api_keys/client.py">update</a>(...) -> ApiKey</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Updates an API key identified by `id`. Only the provided fields are changed.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```python
from wavix import Wavix
from wavix.environment import WavixEnvironment

client = Wavix(
    token="<token>",
    environment=WavixEnvironment.DEFAULT,
)

client.api_keys.update(
    id=1,
    active=True,
    restricted=True,
    scopes_enabled=True,
    permitted_ips=[
        "192.168.1.1",
        "10.0.0.1"
    ],
    label="Production API Key",
)

```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**id:** `int` — The unique ID of the API key.
    
</dd>
</dl>

<dl>
<dd>

**active:** `typing.Optional[bool]` — Indicates whether the API key is active.
    
</dd>
</dl>

<dl>
<dd>

**restricted:** `typing.Optional[bool]` — Indicates whether the API key is restricted to the listed permitted IPs.
    
</dd>
</dl>

<dl>
<dd>

**scopes_enabled:** `typing.Optional[bool]` — Indicates whether per-resource scope permissions are enforced for the API key.
    
</dd>
</dl>

<dl>
<dd>

**permitted_ips:** `typing.Optional[typing.List[str]]` — IP addresses allowed to use the API key when restriction is enabled.
    
</dd>
</dl>

<dl>
<dd>

**label:** `typing.Optional[str]` — Human-readable label for the API key.
    
</dd>
</dl>

<dl>
<dd>

**numbers:** `typing.Optional[ApiKeyScopePermission]` — View, buy, release, and configure phone numbers, browse inventory, and manage the cart.
    
</dd>
</dl>

<dl>
<dd>

**trunks:** `typing.Optional[ApiKeyScopePermission]` — View, create, update, and delete SIP trunks and their settings.
    
</dd>
</dl>

<dl>
<dd>

**calls:** `typing.Optional[ApiKeyCallsScopePermission]` — Access call records and active calls, and control live call actions such as starting, answering, ending, audio playback, DTMF, streaming, and transcription requests.
    
</dd>
</dl>

<dl>
<dd>

**messages:** `typing.Optional[ApiKeyScopePermission]` — Access message history and Sender IDs, send messages, manage opt-outs, and create or delete Sender IDs.
    
</dd>
</dl>

<dl>
<dd>

**recordings:** `typing.Optional[ApiKeyScopePermission]` — List, download, and delete call recordings.
    
</dd>
</dl>

<dl>
<dd>

**campaigns:** `typing.Optional[ApiKeyScopePermission]` — View campaign analytics and Sender ID or Brand status, schedule bulk voice or SMS campaigns, register Brands, and create short links.
    
</dd>
</dl>

<dl>
<dd>

**two_fa:** `typing.Optional[ApiKeyScopePermission]` — View 2FA service details and verification logs, trigger OTPs by voice or SMS, and validate verification codes.
    
</dd>
</dl>

<dl>
<dd>

**validator:** `typing.Optional[ApiKeyScopePermission]` — View number validation results and trigger single or bulk validation or HLR lookup requests.
    
</dd>
</dl>

<dl>
<dd>

**webhooks:** `typing.Optional[ApiKeyScopePermission]` — List, create, and delete webhooks.
    
</dd>
</dl>

<dl>
<dd>

**embeddable:** `typing.Optional[ApiKeyScopePermission]` — Manage widget tokens, including listing, viewing, creating, updating, and deleting them.
    
</dd>
</dl>

<dl>
<dd>

**billing:** `typing.Optional[ApiKeyScopePermission]` — Access statements, balance, payment methods, usage reports, and billing settings, including payment method updates.
    
</dd>
</dl>

<dl>
<dd>

**account:** `typing.Optional[ApiKeyScopePermission]` — View and update account profile information and timezone.
    
</dd>
</dl>

<dl>
<dd>

**subaccounts:** `typing.Optional[ApiKeyScopePermission]` — Manage subaccounts: list and view them, create, update, and suspend them.
    
</dd>
</dl>

<dl>
<dd>

**request_options:** `typing.Optional[RequestOptions]` — Request-specific configuration.
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

## SIP trunks
<details><summary><code>client.sip_trunks.<a href="src/wavix/sip_trunks/client.py">list</a>(...) -> SipTrunkListResponse</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Returns a paginated list of SIP trunks for the authenticated account.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```python
from wavix import Wavix
from wavix.environment import WavixEnvironment

client = Wavix(
    token="<token>",
    environment=WavixEnvironment.DEFAULT,
)

client.sip_trunks.list()

```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**page:** `typing.Optional[int]` — Page number to retrieve. Default `1`.
    
</dd>
</dl>

<dl>
<dd>

**per_page:** `typing.Optional[int]` — Number of records to return per page. Default `25`.
    
</dd>
</dl>

<dl>
<dd>

**request_options:** `typing.Optional[RequestOptions]` — Request-specific configuration.
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.sip_trunks.<a href="src/wavix/sip_trunks/client.py">create</a>(...) -> SipTrunkResponse</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Creates a SIP trunk for routing inbound and outbound calls. Returns the trunk with its generated `access_token`.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```python
from wavix import Wavix
from wavix.environment import WavixEnvironment

client = Wavix(
    token="<token>",
    environment=WavixEnvironment.DEFAULT,
)

client.sip_trunks.create(
    label="My trunk",
    password="4r=h;EaCB85QNtr2",
    callerid="13132847320",
    ip_restrict=False,
    didinfo_enabled=True,
    call_restrict=True,
    channels_restrict=False,
    rewrite_enabled=True,
    transcription_enabled=True,
    transcription_threshold=10,
)

```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**request:** `SipTrunkCreateRequest` 
    
</dd>
</dl>

<dl>
<dd>

**request_options:** `typing.Optional[RequestOptions]` — Request-specific configuration.
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.sip_trunks.<a href="src/wavix/sip_trunks/client.py">get</a>(...) -> SipTrunkResponse</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Returns the SIP trunk identified by `id`.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```python
from wavix import Wavix
from wavix.environment import WavixEnvironment

client = Wavix(
    token="<token>",
    environment=WavixEnvironment.DEFAULT,
)

client.sip_trunks.get(
    id=3107,
)

```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**id:** `int` — The unique ID of the SIP trunk.
    
</dd>
</dl>

<dl>
<dd>

**request_options:** `typing.Optional[RequestOptions]` — Request-specific configuration.
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.sip_trunks.<a href="src/wavix/sip_trunks/client.py">update</a>(...) -> SipTrunkResponse</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Replaces the configuration of the SIP trunk identified by `id`. Omitted fields revert to their defaults.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```python
from wavix import Wavix
from wavix.environment import WavixEnvironment

client = Wavix(
    token="<token>",
    environment=WavixEnvironment.DEFAULT,
)

client.sip_trunks.update(
    id=3107,
    label="My trunk",
    password="4r=h;EaCB85QNtr2",
    callerid="13132847320",
    ip_restrict=False,
    didinfo_enabled=True,
    call_restrict=True,
    channels_restrict=False,
    rewrite_enabled=True,
    transcription_enabled=True,
    transcription_threshold=10,
)

```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**id:** `int` — The unique ID of the SIP trunk.
    
</dd>
</dl>

<dl>
<dd>

**request:** `SipTrunkCreateRequest` 
    
</dd>
</dl>

<dl>
<dd>

**request_options:** `typing.Optional[RequestOptions]` — Request-specific configuration.
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.sip_trunks.<a href="src/wavix/sip_trunks/client.py">delete</a>(...) -> SuccessResponse</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Deletes the SIP trunk identified by `id`. Deletion is permanent and stops call routing through the trunk.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```python
from wavix import Wavix
from wavix.environment import WavixEnvironment

client = Wavix(
    token="<token>",
    environment=WavixEnvironment.DEFAULT,
)

client.sip_trunks.delete(
    id=3107,
)

```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**id:** `int` — The unique ID of the SIP trunk.
    
</dd>
</dl>

<dl>
<dd>

**request_options:** `typing.Optional[RequestOptions]` — Request-specific configuration.
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

## Cart
<details><summary><code>client.cart.<a href="src/wavix/cart/client.py">get</a>() -> CartResponse</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Returns the current purchase cart, including the phone numbers it contains and the documents each requires.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```python
from wavix import Wavix
from wavix.environment import WavixEnvironment

client = Wavix(
    token="<token>",
    environment=WavixEnvironment.DEFAULT,
)

client.cart.get()

```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**request_options:** `typing.Optional[RequestOptions]` — Request-specific configuration.
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.cart.<a href="src/wavix/cart/client.py">add</a>(...) -> typing.List[AvailableNumber]</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Adds the listed phone numbers to the purchase cart.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```python
from wavix import Wavix
from wavix.environment import WavixEnvironment

client = Wavix(
    token="<token>",
    environment=WavixEnvironment.DEFAULT,
)

client.cart.add(
    ids=[
        "541139862174",
        "541139862175"
    ],
)

```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**ids:** `typing.List[str]` — Phone numbers to add to the cart.
    
</dd>
</dl>

<dl>
<dd>

**request_options:** `typing.Optional[RequestOptions]` — Request-specific configuration.
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.cart.<a href="src/wavix/cart/client.py">remove</a>(...) -> SuccessResponse</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Removes the listed phone numbers from the purchase cart.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```python
from wavix import Wavix
from wavix.environment import WavixEnvironment

client = Wavix(
    token="<token>",
    environment=WavixEnvironment.DEFAULT,
)

client.cart.remove(
    ids=[
        "541139862174",
        "541139862175"
    ],
)

```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**ids:** `typing.List[str]` — Phone numbers to remove from the cart.
    
</dd>
</dl>

<dl>
<dd>

**request_options:** `typing.Optional[RequestOptions]` — Request-specific configuration.
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.cart.<a href="src/wavix/cart/client.py">checkout</a>(...) -> SuccessResponse</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Purchases the listed phone numbers from the cart. Activation and monthly fees are debited from the account balance immediately, and the purchase cannot be reversed through this API.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```python
from wavix import Wavix
from wavix.environment import WavixEnvironment

client = Wavix(
    token="<token>",
    environment=WavixEnvironment.DEFAULT,
)

client.cart.checkout(
    ids=[
        "541139862174",
        "541139862175"
    ],
)

```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**ids:** `typing.List[str]` — Phone numbers from the cart to purchase.
    
</dd>
</dl>

<dl>
<dd>

**request_options:** `typing.Optional[RequestOptions]` — Request-specific configuration.
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

## Numbers
<details><summary><code>client.numbers.<a href="src/wavix/numbers/client.py">list</a>(...) -> NumberListResponse</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Returns a paginated list of the phone numbers owned by the authenticated account.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```python
from wavix import Wavix
from wavix.environment import WavixEnvironment

client = Wavix(
    token="<token>",
    environment=WavixEnvironment.DEFAULT,
)

client.numbers.list(
    city_id=123,
    search="256537",
    label="ALEX",
    label_present=True,
    page=2,
    per_page=50,
)

```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**city_id:** `typing.Optional[int]` — Filters numbers by the ID of their city or rate center.
    
</dd>
</dl>

<dl>
<dd>

**search:** `typing.Optional[str]` — Filters numbers by a full or partial phone number.
    
</dd>
</dl>

<dl>
<dd>

**label:** `typing.Optional[str]` — Filters numbers by `label`.
    
</dd>
</dl>

<dl>
<dd>

**label_present:** `typing.Optional[bool]` — When `true`, returns only numbers that have a label; when `false`, only numbers without one.
    
</dd>
</dl>

<dl>
<dd>

**page:** `typing.Optional[int]` — Page number to retrieve. Default `1`.
    
</dd>
</dl>

<dl>
<dd>

**per_page:** `typing.Optional[int]` — Number of records to return per page. Default `25`.
    
</dd>
</dl>

<dl>
<dd>

**request_options:** `typing.Optional[RequestOptions]` — Request-specific configuration.
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.numbers.<a href="src/wavix/numbers/client.py">delete</a>(...) -> SuccessResponse</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Releases the listed phone numbers back to stock. Selection accepts either `ids` (record IDs) or `dids` (phone numbers), but not both.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```python
from wavix import Wavix
from wavix.environment import WavixEnvironment

client = Wavix(
    token="<token>",
    environment=WavixEnvironment.DEFAULT,
)

client.numbers.delete(
    dids="47832123321,47832123324,478321233215",
)

```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**ids:** `typing.Optional[typing.Union[int, typing.Sequence[int]]]` — Record IDs of the phone numbers to release. Mutually exclusive with `dids`.
    
</dd>
</dl>

<dl>
<dd>

**dids:** `typing.Optional[str]` — Comma-separated phone numbers to release. Mutually exclusive with `ids`.
    
</dd>
</dl>

<dl>
<dd>

**request_options:** `typing.Optional[RequestOptions]` — Request-specific configuration.
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.numbers.<a href="src/wavix/numbers/client.py">bulk_update</a>(...) -> BulkUpdateNumbersResponse</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Applies the same changes to every listed phone number. Only the provided fields are changed. Destination and SMS callback changes are applied asynchronously and may not be reflected in the response immediately.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```python
from wavix import Wavix
from wavix.environment import WavixEnvironment

client = Wavix(
    token="<token>",
    environment=WavixEnvironment.DEFAULT,
)

client.numbers.bulk_update(
    ids=[
        123,
        456
    ],
)

```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**ids:** `typing.List[int]` 

Numbers (by ID) to apply the patch to. The same patch is
applied to every listed number.
    
</dd>
</dl>

<dl>
<dd>

**sms_enabled:** `typing.Optional[bool]` — Indicates whether SMS is enabled for the phone numbers.
    
</dd>
</dl>

<dl>
<dd>

**destinations:** `typing.Optional[typing.List[NumberDestination]]` — Inbound call routing destinations for the phone numbers.
    
</dd>
</dl>

<dl>
<dd>

**sms_relay_url:** `typing.Optional[str]` — Callback URL for inbound messages.
    
</dd>
</dl>

<dl>
<dd>

**call_recording_enabled:** `typing.Optional[bool]` — Indicates whether call recording is enabled.
    
</dd>
</dl>

<dl>
<dd>

**transcription_enabled:** `typing.Optional[bool]` — Indicates whether call transcription is enabled.
    
</dd>
</dl>

<dl>
<dd>

**transcription_threshold:** `typing.Optional[int]` — Minimum call duration in seconds before transcription runs.
    
</dd>
</dl>

<dl>
<dd>

**call_status_url:** `typing.Optional[str]` — Callback URL for call status updates.
    
</dd>
</dl>

<dl>
<dd>

**request_options:** `typing.Optional[RequestOptions]` — Request-specific configuration.
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.numbers.<a href="src/wavix/numbers/client.py">get</a>(...) -> Number</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Returns the phone number identified by `id`, including its destinations, documents, and feature settings.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```python
from wavix import Wavix
from wavix.environment import WavixEnvironment

client = Wavix(
    token="<token>",
    environment=WavixEnvironment.DEFAULT,
)

client.numbers.get(
    id=123,
)

```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**id:** `int` — The unique ID of the phone number.
    
</dd>
</dl>

<dl>
<dd>

**request_options:** `typing.Optional[RequestOptions]` — Request-specific configuration.
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.numbers.<a href="src/wavix/numbers/client.py">update</a>(...) -> Number</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Updates the phone number identified by `id`. Only the provided fields are changed.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```python
from wavix import Wavix
from wavix.environment import WavixEnvironment

client = Wavix(
    token="<token>",
    environment=WavixEnvironment.DEFAULT,
)

client.numbers.update(
    id=123,
)

```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**id:** `int` — The unique ID of the phone number.
    
</dd>
</dl>

<dl>
<dd>

**sms_enabled:** `typing.Optional[bool]` — Indicates whether SMS is enabled for the phone number.
    
</dd>
</dl>

<dl>
<dd>

**destinations:** `typing.Optional[typing.List[NumberDestination]]` — Inbound call routing destinations for the phone number.
    
</dd>
</dl>

<dl>
<dd>

**sms_relay_url:** `typing.Optional[str]` — Callback URL for inbound messages.
    
</dd>
</dl>

<dl>
<dd>

**call_recording_enabled:** `typing.Optional[bool]` — Indicates whether call recording is enabled.
    
</dd>
</dl>

<dl>
<dd>

**transcription_enabled:** `typing.Optional[bool]` — Indicates whether call transcription is enabled.
    
</dd>
</dl>

<dl>
<dd>

**transcription_threshold:** `typing.Optional[int]` — Minimum call duration in seconds before transcription runs.
    
</dd>
</dl>

<dl>
<dd>

**call_status_url:** `typing.Optional[str]` — Callback URL for call status updates.
    
</dd>
</dl>

<dl>
<dd>

**request_options:** `typing.Optional[RequestOptions]` — Request-specific configuration.
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

## CDRs
<details><summary><code>client.cdrs.<a href="src/wavix/cdrs/client.py">list</a>(...) -> CdrListResponse</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Returns a paginated list of call detail records for the authenticated account, within the requested date range.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```python
from wavix import Wavix
from wavix.environment import WavixEnvironment
import datetime

client = Wavix(
    token="<token>",
    environment=WavixEnvironment.DEFAULT,
)

client.cdrs.list(
    from_=datetime.date.fromisoformat("2023-01-01"),
    to=datetime.date.fromisoformat("2023-09-01"),
    type="received",
    from_search="13524815863",
    to_search="12565378257",
    sip_trunk="12321",
    uuid_="99df5ffd-962a-410f-bcce-d08f1f7f328c",
    page=1,
    per_page=25,
)

```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**from:** `datetime.date` — Start of the date range to query, in `YYYY-MM-DD` format. Inclusive.
    
</dd>
</dl>

<dl>
<dd>

**to:** `datetime.date` — End of the date range to query, in `YYYY-MM-DD` format. Inclusive.
    
</dd>
</dl>

<dl>
<dd>

**type:** `str` — Filters CDRs by call direction. One of `placed` (outbound calls dialed by the account) or `received` (inbound calls answered by the account).
    
</dd>
</dl>

<dl>
<dd>

**disposition:** `typing.Optional[CallDisposition]` — Filters CDRs by call disposition. One of `answered` (the called party answered), `noanswer` (no answer within the ring timeout), `busy` (the called party was busy), `failed` (the call could not be routed), or `all` (no disposition filter).
    
</dd>
</dl>

<dl>
<dd>

**from_search:** `typing.Optional[str]` — Filters CDRs by originating phone number. Accepts a full or partial number.
    
</dd>
</dl>

<dl>
<dd>

**to_search:** `typing.Optional[str]` — Filters CDRs by destination phone number. Accepts a full or partial number.
    
</dd>
</dl>

<dl>
<dd>

**sip_trunk:** `typing.Optional[str]` — Filters outbound CDRs by SIP trunk login. Ignored for inbound calls.
    
</dd>
</dl>

<dl>
<dd>

**uuid:** `typing.Optional[str]` — Filters CDRs by the unique call ID.
    
</dd>
</dl>

<dl>
<dd>

**page:** `typing.Optional[int]` — Page number to retrieve. Default `1`.
    
</dd>
</dl>

<dl>
<dd>

**per_page:** `typing.Optional[int]` — Number of records to return per page. Default `25`.
    
</dd>
</dl>

<dl>
<dd>

**request_options:** `typing.Optional[RequestOptions]` — Request-specific configuration.
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.cdrs.<a href="src/wavix/cdrs/client.py">search</a>(...) -> CdrTranscriptionSearchResponse</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Searches call transcriptions for the given keywords or phrases and returns the matching CDRs with their transcriptions.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```python
from wavix import Wavix
from wavix.environment import WavixEnvironment
import datetime

client = Wavix(
    token="<token>",
    environment=WavixEnvironment.DEFAULT,
)

client.cdrs.search(
    type="placed",
    from_=datetime.date.fromisoformat("2023-08-01"),
    to=datetime.date.fromisoformat("2023-08-31"),
)

```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**type:** `CdrSearchRequestType` — Filters by call type. One of `placed` (outbound calls dialed by the account) or `received` (inbound calls answered by the account).
    
</dd>
</dl>

<dl>
<dd>

**from:** `datetime.date` — Start date for call search in `YYYY-MM-DD` format.
    
</dd>
</dl>

<dl>
<dd>

**to:** `datetime.date` — End date for call search in `YYYY-MM-DD` format.
    
</dd>
</dl>

<dl>
<dd>

**from_search:** `typing.Optional[str]` — Originating phone number to filter results. Accepts full or partial number.
    
</dd>
</dl>

<dl>
<dd>

**to_search:** `typing.Optional[str]` — Destination phone number to filter results. Accepts full or partial number.
    
</dd>
</dl>

<dl>
<dd>

**sip_trunk:** `typing.Optional[str]` — SIP trunk login to filter outbound calls. Ignored for inbound calls.
    
</dd>
</dl>

<dl>
<dd>

**min_duration:** `typing.Optional[int]` — Minimum call duration in seconds.
    
</dd>
</dl>

<dl>
<dd>

**transcription:** `typing.Optional[TranscriptionFilter]` 
    
</dd>
</dl>

<dl>
<dd>

**uuid:** `typing.Optional[str]` — Call ID.
    
</dd>
</dl>

<dl>
<dd>

**disposition:** `typing.Optional[CallDisposition]` 

Call disposition to filter results.  If omitted, returns only answered
 calls. Allowed values: `answered`, `noanswer`, `busy`,
  `failed`, `all`. Use `all` to return calls
   regardless of their disposition.
    
</dd>
</dl>

<dl>
<dd>

**page:** `typing.Optional[int]` — Page number to retrieve.
    
</dd>
</dl>

<dl>
<dd>

**per_page:** `typing.Optional[int]` — Number of records per page.
    
</dd>
</dl>

<dl>
<dd>

**request_options:** `typing.Optional[RequestOptions]` — Request-specific configuration.
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.cdrs.<a href="src/wavix/cdrs/client.py">retranscribe</a>(...) -> SuccessResponse</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Transcribes the recording of the call identified by `call_id`. Transcription is asynchronous; poll the transcription endpoint for the result. Billed per minute at the account's call-transcription rate; fails with an insufficient-funds error when the balance cannot cover it.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```python
from wavix import Wavix
from wavix.environment import WavixEnvironment

client = Wavix(
    token="<token>",
    environment=WavixEnvironment.DEFAULT,
)

client.cdrs.retranscribe(
    call_id="bbaa37bf-430a-46da-ade3-c248e4070160",
)

```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**call_id:** `str` — The unique ID of the call.
    
</dd>
</dl>

<dl>
<dd>

**language:** `typing.Optional[TranscriptionLanguage]` 
    
</dd>
</dl>

<dl>
<dd>

**webhook_url:** `typing.Optional[str]` — Webhook URL to receive status updates.
    
</dd>
</dl>

<dl>
<dd>

**request_options:** `typing.Optional[RequestOptions]` — Request-specific configuration.
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.cdrs.<a href="src/wavix/cdrs/client.py">transcriptions</a>(...) -> CdrTranscriptionResponse</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Returns the transcription of the recorded call identified by `call_id`. Alias of the `transcription` endpoint.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```python
from wavix import Wavix
from wavix.environment import WavixEnvironment

client = Wavix(
    token="<token>",
    environment=WavixEnvironment.DEFAULT,
)

client.cdrs.transcriptions(
    call_id="bbaa37bf-430a-46da-ade3-c248e4070160",
)

```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**call_id:** `str` — The unique ID of the call.
    
</dd>
</dl>

<dl>
<dd>

**request_options:** `typing.Optional[RequestOptions]` — Request-specific configuration.
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.cdrs.<a href="src/wavix/cdrs/client.py">get</a>(...) -> CdrResponse</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Returns the call detail record for the call identified by `call_id`.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```python
from wavix import Wavix
from wavix.environment import WavixEnvironment

client = Wavix(
    token="<token>",
    environment=WavixEnvironment.DEFAULT,
)

client.cdrs.get(
    call_id="aa566501-c591-4a8b-b3b9-cc1295398b72",
    show_transcription=True,
)

```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**call_id:** `str` — The unique ID of the call.
    
</dd>
</dl>

<dl>
<dd>

**show_transcription:** `typing.Optional[bool]` — When `true`, includes the call transcription in the response.
    
</dd>
</dl>

<dl>
<dd>

**request_options:** `typing.Optional[RequestOptions]` — Request-specific configuration.
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.cdrs.<a href="src/wavix/cdrs/client.py">list_all</a>(...) -> str</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Streams matching call detail records as newline-delimited JSON (NDJSON), one record per line, for bulk export.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```python
from wavix import Wavix
from wavix.environment import WavixEnvironment
import datetime

client = Wavix(
    token="<token>",
    environment=WavixEnvironment.DEFAULT,
)

client.cdrs.list_all(
    from_=datetime.date.fromisoformat("2023-01-01"),
    to=datetime.date.fromisoformat("2023-09-01"),
    type="received",
    from_search="13524815863",
    to_search="12565378257",
    sip_trunk="12321",
    uuid_="99df5ffd-962a-410f-bcce-d08f1f7f328c",
    page=1,
    per_page=25,
)

```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**from:** `datetime.date` — Start of the date range to query, in `YYYY-MM-DD` format. Inclusive.
    
</dd>
</dl>

<dl>
<dd>

**to:** `datetime.date` — End of the date range to query, in `YYYY-MM-DD` format. Inclusive.
    
</dd>
</dl>

<dl>
<dd>

**type:** `str` — Filters CDRs by call direction. One of `placed` (outbound calls dialed by the account) or `received` (inbound calls answered by the account).
    
</dd>
</dl>

<dl>
<dd>

**disposition:** `typing.Optional[CallDisposition]` — Filters CDRs by call disposition. One of `answered` (the called party answered), `noanswer` (no answer within the ring timeout), `busy` (the called party was busy), `failed` (the call could not be routed), or `all` (no disposition filter).
    
</dd>
</dl>

<dl>
<dd>

**from_search:** `typing.Optional[str]` — Filters CDRs by originating phone number. Accepts a full or partial number.
    
</dd>
</dl>

<dl>
<dd>

**to_search:** `typing.Optional[str]` — Filters CDRs by destination phone number. Accepts a full or partial number.
    
</dd>
</dl>

<dl>
<dd>

**sip_trunk:** `typing.Optional[str]` — Filters outbound CDRs by SIP trunk login. Ignored for inbound calls.
    
</dd>
</dl>

<dl>
<dd>

**uuid:** `typing.Optional[str]` — Filters CDRs by the unique call ID.
    
</dd>
</dl>

<dl>
<dd>

**page:** `typing.Optional[int]` — Page number to retrieve. Default `1`.
    
</dd>
</dl>

<dl>
<dd>

**per_page:** `typing.Optional[int]` — Number of records to return per page. Default `25`.
    
</dd>
</dl>

<dl>
<dd>

**request_options:** `typing.Optional[RequestOptions]` — Request-specific configuration.
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

## Call recording
<details><summary><code>client.call_recording.<a href="src/wavix/call_recording/client.py">list</a>(...) -> CallRecordingListResponse</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Returns a paginated list of call recordings for the authenticated account, filtered by date range, number, call, or SIP trunk.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```python
from wavix import Wavix
from wavix.environment import WavixEnvironment
import datetime

client = Wavix(
    token="<token>",
    environment=WavixEnvironment.DEFAULT,
)

client.call_recording.list(
    from_date=datetime.date.fromisoformat("2023-01-01"),
    to_date=datetime.date.fromisoformat("2023-12-31"),
    from_="123456",
    to="1987654321",
    call_uuid="aa566501-c591-4a8b-b3b9-cc1295398b72",
    page=1,
    per_page=25,
)

```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**from_date:** `typing.Optional[datetime.date]` — Start of the date range to query, in `YYYY-MM-DD` format. Inclusive.
    
</dd>
</dl>

<dl>
<dd>

**to_date:** `typing.Optional[datetime.date]` — End of the date range to query, in `YYYY-MM-DD` format. Inclusive.
    
</dd>
</dl>

<dl>
<dd>

**from:** `typing.Optional[str]` — Filters recordings by originating phone number. Accepts a full or partial number.
    
</dd>
</dl>

<dl>
<dd>

**to:** `typing.Optional[str]` — Filters recordings by destination phone number. Accepts a full or partial number.
    
</dd>
</dl>

<dl>
<dd>

**call_uuid:** `typing.Optional[str]` — Filters recordings by the unique call ID.
    
</dd>
</dl>

<dl>
<dd>

**sip_trunks:** `typing.Optional[typing.Union[str, typing.Sequence[str]]]` — Filters recordings of outbound calls placed through the listed SIP trunk logins.
    
</dd>
</dl>

<dl>
<dd>

**page:** `typing.Optional[int]` — Page number to retrieve. Default `1`.
    
</dd>
</dl>

<dl>
<dd>

**per_page:** `typing.Optional[int]` — Number of records to return per page. Default `25`.
    
</dd>
</dl>

<dl>
<dd>

**request_options:** `typing.Optional[RequestOptions]` — Request-specific configuration.
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.call_recording.<a href="src/wavix/call_recording/client.py">get_by_call</a>(...)</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Redirects to the recording file for the call identified by `call_id`. The download URL is returned in the `Location` header.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```python
from wavix import Wavix
from wavix.environment import WavixEnvironment

client = Wavix(
    token="<token>",
    environment=WavixEnvironment.DEFAULT,
)

client.call_recording.get_by_call(
    call_id="aa566501-c591-4a8b-b3b9-cc1295398b72",
)

```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**call_id:** `str` — The unique ID of the call whose recording is retrieved.
    
</dd>
</dl>

<dl>
<dd>

**request_options:** `typing.Optional[RequestOptions]` — Request-specific configuration.
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.call_recording.<a href="src/wavix/call_recording/client.py">get</a>(...) -> Recording</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Returns the call recording identified by `id`, including its metadata and download URL.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```python
from wavix import Wavix
from wavix.environment import WavixEnvironment

client = Wavix(
    token="<token>",
    environment=WavixEnvironment.DEFAULT,
)

client.call_recording.get(
    id=123,
)

```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**id:** `int` — The unique ID of the call recording.
    
</dd>
</dl>

<dl>
<dd>

**request_options:** `typing.Optional[RequestOptions]` — Request-specific configuration.
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.call_recording.<a href="src/wavix/call_recording/client.py">delete</a>(...) -> SuccessResponse</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Deletes the call recording identified by `id`. Deletion is permanent — the audio file is unrecoverable.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```python
from wavix import Wavix
from wavix.environment import WavixEnvironment

client = Wavix(
    token="<token>",
    environment=WavixEnvironment.DEFAULT,
)

client.call_recording.delete(
    id=123,
)

```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**id:** `int` — The unique ID of the call recording.
    
</dd>
</dl>

<dl>
<dd>

**request_options:** `typing.Optional[RequestOptions]` — Request-specific configuration.
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

## Speech Analytics
<details><summary><code>client.speech_analytics.<a href="src/wavix/speech_analytics/client.py">create</a>(...) -> SubmitFileTranscriptionResponse</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Uploads an audio file for transcription. Transcription is asynchronous; Wavix sends a POST callback to `callback_url` when it completes, including the `request_id` returned by this request.

Callback body:
```json
   {
        "request_id": "e865ea07-25af-4fdd-876e-04b0d41d5ebd",
        "status": "completed",
        "error": null
   }
```

- `request_id`: ID of the transcription request.
- `status`: One of `completed` (transcription succeeded) or `failed` (transcription encountered an error).
- `error`: Error description, or `null` when the transcription succeeded.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```python
from wavix import Wavix
from wavix.environment import WavixEnvironment

client = Wavix(
    token="<token>",
    environment=WavixEnvironment.DEFAULT,
)

client.speech_analytics.create(
    file="example_file",
    callback_url="callback_url",
)

```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**file:** `core.File` — Audio file to transcribe. Maximum size is 25 MB. Supported formats are WAV, MP3, and MP4 stereo.
    
</dd>
</dl>

<dl>
<dd>

**callback_url:** `str` — URL that receives the POST callback when transcription completes.
    
</dd>
</dl>

<dl>
<dd>

**insights:** `typing.Optional[bool]` — When `true`, generates conversation insights alongside the transcript.
    
</dd>
</dl>

<dl>
<dd>

**request_options:** `typing.Optional[RequestOptions]` — Request-specific configuration.
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.speech_analytics.<a href="src/wavix/speech_analytics/client.py">get</a>(...) -> FileTranscriptionResponse</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Returns the transcription for the request identified by `request_id`, including transcript, speaker turns, and insights when available.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```python
from wavix import Wavix
from wavix.environment import WavixEnvironment

client = Wavix(
    token="<token>",
    environment=WavixEnvironment.DEFAULT,
)

client.speech_analytics.get(
    request_id="e865ea07-25af-4fdd-876e-04b0d41d5ebd",
)

```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**request_id:** `str` — The `request_id` of the transcription, returned when the file was uploaded.
    
</dd>
</dl>

<dl>
<dd>

**request_options:** `typing.Optional[RequestOptions]` — Request-specific configuration.
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.speech_analytics.<a href="src/wavix/speech_analytics/client.py">retranscribe</a>(...) -> SuccessResponse</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Re-runs transcription on the file identified by `request_id`, replacing the existing transcript.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```python
from wavix import Wavix
from wavix.environment import WavixEnvironment

client = Wavix(
    token="<token>",
    environment=WavixEnvironment.DEFAULT,
)

client.speech_analytics.retranscribe(
    request_id="e865ea07-25af-4fdd-876e-04b0d41d5ebd",
    callback_url="https://you-site.com/webhook",
)

```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**request_id:** `str` — The `request_id` of the transcription, returned when the file was uploaded.
    
</dd>
</dl>

<dl>
<dd>

**callback_url:** `str` — Callback URL for transcription status updates.
    
</dd>
</dl>

<dl>
<dd>

**insights:** `typing.Optional[bool]` — Indicates whether to enable insights generation.
    
</dd>
</dl>

<dl>
<dd>

**request_options:** `typing.Optional[RequestOptions]` — Request-specific configuration.
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

## Call webhooks
<details><summary><code>client.call_webhooks.<a href="src/wavix/call_webhooks/client.py">list</a>() -> CallWebhookListResponse</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Returns the configured call webhooks for the authenticated account. Wavix sends POST callbacks for `on-call` and `post-call` events.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```python
from wavix import Wavix
from wavix.environment import WavixEnvironment

client = Wavix(
    token="<token>",
    environment=WavixEnvironment.DEFAULT,
)

client.call_webhooks.list()

```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**request_options:** `typing.Optional[RequestOptions]` — Request-specific configuration.
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.call_webhooks.<a href="src/wavix/call_webhooks/client.py">create</a>(...) -> CallWebhook</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Registers a callback URL for the `on-call` or `post-call` event. Wavix sends a POST callback to the URL when the event occurs. Creates persistent configuration that forwards call metadata to the URL on every matching call until the webhook is deleted.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```python
from wavix import Wavix
from wavix.environment import WavixEnvironment

client = Wavix(
    token="<token>",
    environment=WavixEnvironment.DEFAULT,
)

client.call_webhooks.create(
    url="https://you-site.com/webhook",
    event_type="post-call",
)

```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**url:** `str` — Webhook URL to send call events to.
    
</dd>
</dl>

<dl>
<dd>

**event_type:** `CallWebhooksCreateRequestEventType` 

Allowed values: `on-call`, `post-call`.
 - `on-call`: Sends real-time status updates
  when a call starts, is answered, and ends.

 - `post-call`: Sends a callback after the call ends
  with disposition, duration, and cost.
    
</dd>
</dl>

<dl>
<dd>

**request_options:** `typing.Optional[RequestOptions]` — Request-specific configuration.
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.call_webhooks.<a href="src/wavix/call_webhooks/client.py">delete</a>(...) -> SuccessResponse</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Removes the call webhook for the given event type. Wavix stops sending callbacks for that event.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```python
from wavix import Wavix
from wavix.environment import WavixEnvironment

client = Wavix(
    token="<token>",
    environment=WavixEnvironment.DEFAULT,
)

client.call_webhooks.delete(
    event_type="post-call",
)

```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**event_type:** `DeleteCallWebhooksRequestEventType` — Event type of the webhook to delete. One of `post-call` (callbacks sent after a call ends) or `on-call` (real-time call status callbacks during a call).
    
</dd>
</dl>

<dl>
<dd>

**request_options:** `typing.Optional[RequestOptions]` — Request-specific configuration.
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

## Call control
<details><summary><code>client.call_control.<a href="src/wavix/call_control/client.py">list</a>() -> CallListResponse</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Returns the calls currently in progress for the authenticated account.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```python
from wavix import Wavix
from wavix.environment import WavixEnvironment

client = Wavix(
    token="<token>",
    environment=WavixEnvironment.DEFAULT,
)

client.call_control.list()

```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**request_options:** `typing.Optional[RequestOptions]` — Request-specific configuration.
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.call_control.<a href="src/wavix/call_control/client.py">create</a>(...) -> CallCreateResponse</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Places a real, billable outbound PSTN call. Returns the call with its `uuid` for tracking and control.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```python
from wavix import Wavix
from wavix.environment import WavixEnvironment

client = Wavix(
    token="<token>",
    environment=WavixEnvironment.DEFAULT,
)

client.call_control.create(
    from_="+1234567890",
    to="+1987654321",
    callback_url="https://examples.com/callback",
)

```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**from:** `str` — Caller ID. Must be an active or verified phone number on the account.
    
</dd>
</dl>

<dl>
<dd>

**to:** `str` — Destination number in E.164 format
    
</dd>
</dl>

<dl>
<dd>

**callback_url:** `str` — The callback URL where Wavix sends the call status updates
    
</dd>
</dl>

<dl>
<dd>

**recording:** `typing.Optional[bool]` — Specifies whether to record the call
    
</dd>
</dl>

<dl>
<dd>

**voicemail_detection:** `typing.Optional[bool]` — Specifies whether the AMD is turned on for the call
    
</dd>
</dl>

<dl>
<dd>

**tag:** `typing.Optional[str]` — Call metadata
    
</dd>
</dl>

<dl>
<dd>

**timeout:** `typing.Optional[int]` — The ring timeout, in seconds, before the call is considered unanswered.
    
</dd>
</dl>

<dl>
<dd>

**request_options:** `typing.Optional[RequestOptions]` — Request-specific configuration.
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.call_control.<a href="src/wavix/call_control/client.py">get</a>(...) -> CallResponse</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Returns the call identified by `id`, including its current event and timestamps.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```python
from wavix import Wavix
from wavix.environment import WavixEnvironment

client = Wavix(
    token="<token>",
    environment=WavixEnvironment.DEFAULT,
)

client.call_control.get(
    id="id",
)

```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**id:** `str` — The `uuid` of the call.
    
</dd>
</dl>

<dl>
<dd>

**request_options:** `typing.Optional[RequestOptions]` — Request-specific configuration.
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.call_control.<a href="src/wavix/call_control/client.py">delete</a>(...) -> SuccessResponse</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Ends the active call identified by `id` by hanging up. Irreversible — the call cannot be resumed once ended.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```python
from wavix import Wavix
from wavix.environment import WavixEnvironment

client = Wavix(
    token="<token>",
    environment=WavixEnvironment.DEFAULT,
)

client.call_control.delete(
    id="id",
)

```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**id:** `str` — The `uuid` of the call.
    
</dd>
</dl>

<dl>
<dd>

**request_options:** `typing.Optional[RequestOptions]` — Request-specific configuration.
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.call_control.<a href="src/wavix/call_control/client.py">update</a>(...) -> SuccessResponse</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Updates the active call identified by `id`. Only the `tag` field can be changed.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```python
from wavix import Wavix
from wavix.environment import WavixEnvironment

client = Wavix(
    token="<token>",
    environment=WavixEnvironment.DEFAULT,
)

client.call_control.update(
    id="id",
    tag="marketing-campaign",
)

```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**id:** `str` — The `uuid` of the call.
    
</dd>
</dl>

<dl>
<dd>

**tag:** `str` — User-defined label attached to the Call for tracking or reporting.
    
</dd>
</dl>

<dl>
<dd>

**request_options:** `typing.Optional[RequestOptions]` — Request-specific configuration.
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.call_control.<a href="src/wavix/call_control/client.py">answer</a>(...) -> SuccessResponse</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Answers the inbound call identified by `id`. Optionally starts recording, post-call transcription, or live media streaming on answer.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```python
from wavix import Wavix
from wavix.environment import WavixEnvironment

client = Wavix(
    token="<token>",
    environment=WavixEnvironment.DEFAULT,
)

client.call_control.answer(
    id="id",
)

```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**id:** `str` — The `uuid` of the call.
    
</dd>
</dl>

<dl>
<dd>

**call_recording:** `typing.Optional[bool]` — Indicates whether the call should be recorded.
    
</dd>
</dl>

<dl>
<dd>

**call_transcription:** `typing.Optional[bool]` — Indicates whether the call should be transcribed after it ends.
    
</dd>
</dl>

<dl>
<dd>

**stream_url:** `typing.Optional[str]` — WebSocket URL to stream the call.
    
</dd>
</dl>

<dl>
<dd>

**stream_type:** `typing.Optional[CallStreamType]` — Direction of audio streamed to `stream_url`.
    
</dd>
</dl>

<dl>
<dd>

**stream_channel:** `typing.Optional[CallStreamChannel]` — Audio channel streamed to `stream_url`.
    
</dd>
</dl>

<dl>
<dd>

**request_options:** `typing.Optional[RequestOptions]` — Request-specific configuration.
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.call_control.<a href="src/wavix/call_control/client.py">collect</a>(...) -> SuccessResponse</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Collects DTMF keypad input from the caller on the active call identified by `id`.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```python
from wavix import Wavix
from wavix.environment import WavixEnvironment

client = Wavix(
    token="<token>",
    environment=WavixEnvironment.DEFAULT,
)

client.call_control.collect(
    id="id",
)

```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**id:** `str` — The `uuid` of the call.
    
</dd>
</dl>

<dl>
<dd>

**max_digits:** `typing.Optional[int]` — Maximum number of digits to collect.
    
</dd>
</dl>

<dl>
<dd>

**timeout:** `typing.Optional[int]` — Timeout for digit collection in seconds.
    
</dd>
</dl>

<dl>
<dd>

**termination_character:** `typing.Optional[str]` — DTMF character that ends input collection.
    
</dd>
</dl>

<dl>
<dd>

**max_attempts:** `typing.Optional[int]` — Maximum number of attempts.
    
</dd>
</dl>

<dl>
<dd>

**prompt:** `typing.Optional[CallDtmfCollectRequestPrompt]` 

Prompt to play before collecting digits.
 Play a prerecorded audio file or use Wavix Text-To-Speech.
    
</dd>
</dl>

<dl>
<dd>

**request_options:** `typing.Optional[RequestOptions]` — Request-specific configuration.
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

## NumberValidator
<details><summary><code>client.number_validator.<a href="src/wavix/number_validator/client.py">get</a>(...) -> PhoneValidationResponse</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Validates a single phone number and returns line type, carrier, portability, and reachability details. The response's `error_code` is a per-number result code (`000` success; `013` internal error; `021` invalid format; `041` remote timeout; `042` remote query failed; `091` insufficient funds) — distinct from the HTTP status codes below.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```python
from wavix import Wavix
from wavix.environment import WavixEnvironment

client = Wavix(
    token="<token>",
    environment=WavixEnvironment.DEFAULT,
)

client.number_validator.get(
    phone_number="971569483322",
    type="format",
)

```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**phone_number:** `str` — The phone number to validate, in E.164 format with or without the leading `+`.
    
</dd>
</dl>

<dl>
<dd>

**type:** `PhoneNumberValidationType` — Depth of validation to perform. Accepts a `PhoneNumberValidationType` value.
    
</dd>
</dl>

<dl>
<dd>

**request_options:** `typing.Optional[RequestOptions]` — Request-specific configuration.
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.number_validator.<a href="src/wavix/number_validator/client.py">create_bulk</a>(...) -> NumberValidatorCreateBulkResponse</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Validates a batch of phone numbers. When `async` is `true`, returns a `request_id` to poll for results instead of the validation details.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```python
from wavix import Wavix
from wavix.environment import WavixEnvironment

client = Wavix(
    token="<token>",
    environment=WavixEnvironment.DEFAULT,
)

client.number_validator.create_bulk(
    phone_numbers=[
        "971501390098",
        "971504359195"
    ],
    type="format",
)

```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**phone_numbers:** `typing.List[str]` — List of phone numbers to get detailed information about. Maximum 1000 numbers per request.
    
</dd>
</dl>

<dl>
<dd>

**type:** `PhoneNumberValidationType` 
    
</dd>
</dl>

<dl>
<dd>

**async:** `typing.Optional[bool]` — Indicates whether the request should be executed asynchronously. If `true`, the response will include a `request_uuid` that can be used to poll for results. If `false` (default), the response will include validation results directly.
    
</dd>
</dl>

<dl>
<dd>

**force:** `typing.Optional[bool]` — Indicates whether to force a fresh validation instead of returning a previously cached result. Defaults to `false`.
    
</dd>
</dl>

<dl>
<dd>

**request_options:** `typing.Optional[RequestOptions]` — Request-specific configuration.
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

## Voice campaigns
<details><summary><code>client.voice_campaigns.<a href="src/wavix/voice_campaigns/client.py">create</a>(...) -> VoiceCampaignsCreateResponse</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Launches a voice campaign that places a real outbound call using a pre-configured scenario. Track progress with the returned voice campaign `id`.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```python
from wavix import Wavix, VoiceCampaignResponse
from wavix.environment import WavixEnvironment

client = Wavix(
    token="<token>",
    environment=WavixEnvironment.DEFAULT,
)

client.voice_campaigns.create(
    voice_campaign=VoiceCampaignResponse(
        callflow_id=3212,
        caller_id="13123310912",
        contact="16729923812",
    ),
)

```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**voice_campaign:** `VoiceCampaignResponse` 
    
</dd>
</dl>

<dl>
<dd>

**request_options:** `typing.Optional[RequestOptions]` — Request-specific configuration.
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.voice_campaigns.<a href="src/wavix/voice_campaigns/client.py">get</a>(...) -> VoiceCampaignsGetResponse</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Returns the voice campaign identified by `id`, including its current status.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```python
from wavix import Wavix
from wavix.environment import WavixEnvironment

client = Wavix(
    token="<token>",
    environment=WavixEnvironment.DEFAULT,
)

client.voice_campaigns.get(
    id=2321423,
)

```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**id:** `int` — The unique ID of the voice campaign to retrieve.
    
</dd>
</dl>

<dl>
<dd>

**request_options:** `typing.Optional[RequestOptions]` — Request-specific configuration.
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

## Link shortener
<details><summary><code>client.link_shortener.<a href="src/wavix/link_shortener/client.py">create</a>(...) -> ShortLinkResponse</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Creates a short link that redirects to the target URL and tracks click metrics.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```python
from wavix import Wavix
from wavix.environment import WavixEnvironment

client = Wavix(
    token="<token>",
    environment=WavixEnvironment.DEFAULT,
)

client.link_shortener.create(
    link="https://your-site.com/long-url",
)

```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**link:** `str` — Target URL to shorten. Must be `https://` — the short link is publicly resolvable and redirects any visitor here, so only pass URLs you trust; this endpoint is a common target for open-redirect and phishing abuse.
    
</dd>
</dl>

<dl>
<dd>

**expiration_time:** `typing.Optional[datetime.datetime]` — Expiration date and time in ISO 8601 format.
    
</dd>
</dl>

<dl>
<dd>

**fallback_url:** `typing.Optional[str]` — Fallback URL for expired or invalid links. Must be `https://` — same open-redirect/phishing considerations as `link` apply.
    
</dd>
</dl>

<dl>
<dd>

**phone:** `typing.Optional[str]` — Phone number the short link is associated with, in E.164 format (without the leading `+`). Used to attribute click metrics returned by short link metrics list.
    
</dd>
</dl>

<dl>
<dd>

**utm_campaign:** `typing.Optional[str]` — UTM campaign name for tracking insights.
    
</dd>
</dl>

<dl>
<dd>

**request_options:** `typing.Optional[RequestOptions]` — Request-specific configuration.
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

## Profile
<details><summary><code>client.profile.<a href="src/wavix/profile/client.py">get</a>() -> ProfileResponse</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Returns the profile and billing details of the authenticated account.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```python
from wavix import Wavix
from wavix.environment import WavixEnvironment

client = Wavix(
    token="<token>",
    environment=WavixEnvironment.DEFAULT,
)

client.profile.get()

```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**request_options:** `typing.Optional[RequestOptions]` — Request-specific configuration.
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.profile.<a href="src/wavix/profile/client.py">update</a>(...) -> ProfileResponse</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Updates the profile and billing details of the authenticated account.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```python
from wavix import Wavix
from wavix.environment import WavixEnvironment

client = Wavix(
    token="<token>",
    environment=WavixEnvironment.DEFAULT,
)

client.profile.update()

```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**additional_info:** `typing.Optional[str]` — Additional information associated with the account.
    
</dd>
</dl>

<dl>
<dd>

**contacts:** `typing.Optional[str]` — Email associated with the account.
    
</dd>
</dl>

<dl>
<dd>

**default_short_link_endpoint:** `typing.Optional[str]` — Default short link endpoint.
    
</dd>
</dl>

<dl>
<dd>

**first_name:** `typing.Optional[str]` — Account owner's first name.
    
</dd>
</dl>

<dl>
<dd>

**last_name:** `typing.Optional[str]` — Account owner's last name.
    
</dd>
</dl>

<dl>
<dd>

**phone:** `typing.Optional[str]` — Account owner's phone number
    
</dd>
</dl>

<dl>
<dd>

**sms_relay_url:** `typing.Optional[str]` — Callback URL to forward inbound SMS to.
    
</dd>
</dl>

<dl>
<dd>

**dlr_relay_url:** `typing.Optional[str]` — Callback URL to forward message delivery reports (DLRs) to.
    
</dd>
</dl>

<dl>
<dd>

**time_zone:** `typing.Optional[str]` — Timezone configured on the account.
    
</dd>
</dl>

<dl>
<dd>

**job_title:** `typing.Optional[str]` — Account owner's job title.
    
</dd>
</dl>

<dl>
<dd>

**company_info:** `typing.Optional[ProfileUpdateRequestCompanyInfo]` 
    
</dd>
</dl>

<dl>
<dd>

**request_options:** `typing.Optional[RequestOptions]` — Request-specific configuration.
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

## SubAccounts
<details><summary><code>client.sub_accounts.<a href="src/wavix/sub_accounts/client.py">list</a>(...) -> SubAccountsListResponse</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Returns a paginated list of sub-accounts under the authenticated master account.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```python
from wavix import Wavix
from wavix.environment import WavixEnvironment

client = Wavix(
    token="<token>",
    environment=WavixEnvironment.DEFAULT,
)

client.sub_accounts.list()

```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**status:** `typing.Optional[ListSubAccountsRequestStatus]` — Filters sub-accounts by status. One of `enabled` (the sub-account is active) or `disabled` (the sub-account is suspended).
    
</dd>
</dl>

<dl>
<dd>

**page:** `typing.Optional[int]` — Page number to retrieve. Default `1`.
    
</dd>
</dl>

<dl>
<dd>

**per_page:** `typing.Optional[int]` — Number of records to return per page. Default `25`.
    
</dd>
</dl>

<dl>
<dd>

**request_options:** `typing.Optional[RequestOptions]` — Request-specific configuration.
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.sub_accounts.<a href="src/wavix/sub_accounts/client.py">create</a>(...) -> SubOrganizationResponse</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Creates a sub-account under the authenticated master account. Returns the sub-account with its generated `api_key`.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```python
from wavix import Wavix
from wavix.environment import WavixEnvironment
from wavix.sub_accounts import SubAccountsCreateRequestDefaultDestinations

client = Wavix(
    token="<token>",
    environment=WavixEnvironment.DEFAULT,
)

client.sub_accounts.create(
    name="Company",
    default_destinations=SubAccountsCreateRequestDefaultDestinations(
        sms_endpoint="https://examples.com/sms",
        dlr_endpoint="https://examples.com/dlr",
    ),
)

```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**name:** `str` — Sub-account name.
    
</dd>
</dl>

<dl>
<dd>

**default_destinations:** `typing.Optional[SubAccountsCreateRequestDefaultDestinations]` — Default webhook URLs for inbound messages and delivery reports.
    
</dd>
</dl>

<dl>
<dd>

**request_options:** `typing.Optional[RequestOptions]` — Request-specific configuration.
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.sub_accounts.<a href="src/wavix/sub_accounts/client.py">get</a>(...) -> SubOrganizationResponse</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Returns the sub-account identified by `id`.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```python
from wavix import Wavix
from wavix.environment import WavixEnvironment

client = Wavix(
    token="<token>",
    environment=WavixEnvironment.DEFAULT,
)

client.sub_accounts.get(
    id=123,
)

```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**id:** `int` — The unique ID of the sub-account.
    
</dd>
</dl>

<dl>
<dd>

**request_options:** `typing.Optional[RequestOptions]` — Request-specific configuration.
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.sub_accounts.<a href="src/wavix/sub_accounts/client.py">update</a>(...) -> SubOrganizationResponse</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Replaces the configuration of the sub-account identified by `id`. Omitted fields revert to their defaults.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```python
from wavix import Wavix
from wavix.environment import WavixEnvironment
from wavix.sub_accounts import SubAccountsUpdateRequestDefaultDestinations

client = Wavix(
    token="<token>",
    environment=WavixEnvironment.DEFAULT,
)

client.sub_accounts.update(
    id=123,
    name="Updated Company Name",
    status="enabled",
    default_destinations=SubAccountsUpdateRequestDefaultDestinations(
        sms_endpoint="https://examples.com/sms",
        dlr_endpoint="https://examples.com/dlr",
    ),
)

```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**id:** `int` — The unique ID of the sub-account.
    
</dd>
</dl>

<dl>
<dd>

**name:** `typing.Optional[str]` — Sub-account name.
    
</dd>
</dl>

<dl>
<dd>

**status:** `typing.Optional[SubAccountsUpdateRequestStatus]` — Status of the subaccount. One of `enabled` (the subaccount is active and can be used) or `disabled` (the subaccount is suspended).
    
</dd>
</dl>

<dl>
<dd>

**default_destinations:** `typing.Optional[SubAccountsUpdateRequestDefaultDestinations]` — Default webhook URLs for inbound messages and delivery reports.
    
</dd>
</dl>

<dl>
<dd>

**request_options:** `typing.Optional[RequestOptions]` — Request-specific configuration.
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

## Billing Transactions
<details><summary><code>client.billing.transactions.<a href="src/wavix/billing/transactions/client.py">list</a>(...) -> BillingTransactionListResponse</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Returns a paginated list of billing transactions for the authenticated account within the requested date range.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```python
from wavix import Wavix
from wavix.environment import WavixEnvironment
import datetime

client = Wavix(
    token="<token>",
    environment=WavixEnvironment.DEFAULT,
)

client.billing.transactions.list(
    from_date=datetime.date.fromisoformat("2023-08-01"),
    to_date=datetime.date.fromisoformat("2023-08-31"),
    details_contains="monthly",
    payments=True,
    page=1,
    per_page=25,
)

```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**from_date:** `datetime.date` — Start of the date range to query, in `YYYY-MM-DD` format. Inclusive.
    
</dd>
</dl>

<dl>
<dd>

**to_date:** `datetime.date` — End of the date range to query, in `YYYY-MM-DD` format. Inclusive.
    
</dd>
</dl>

<dl>
<dd>

**type:** `typing.Optional[TransactionType]` — Filters transactions by type. Accepts a `TransactionType` value.
    
</dd>
</dl>

<dl>
<dd>

**details_contains:** `typing.Optional[str]` — Filters transactions whose `details` contain the given substring.
    
</dd>
</dl>

<dl>
<dd>

**payments:** `typing.Optional[bool]` — When `true`, returns only account top-up transactions. Defaults to all transaction types.
    
</dd>
</dl>

<dl>
<dd>

**page:** `typing.Optional[int]` — Page number to retrieve. Default `1`.
    
</dd>
</dl>

<dl>
<dd>

**per_page:** `typing.Optional[int]` — Number of records to return per page. Default `25`.
    
</dd>
</dl>

<dl>
<dd>

**request_options:** `typing.Optional[RequestOptions]` — Request-specific configuration.
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

## Billing Invoices
<details><summary><code>client.billing.invoices.<a href="src/wavix/billing/invoices/client.py">list</a>(...) -> InvoiceListResponse</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Returns the auto-generated financial statements for the authenticated account, paginated and ordered by billing period.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```python
from wavix import Wavix
from wavix.environment import WavixEnvironment

client = Wavix(
    token="<token>",
    environment=WavixEnvironment.DEFAULT,
)

client.billing.invoices.list(
    page=1,
    per_page=25,
)

```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**page:** `typing.Optional[int]` — Page number to retrieve. Default `1`.
    
</dd>
</dl>

<dl>
<dd>

**per_page:** `typing.Optional[int]` — Number of records to return per page. Default `25`.
    
</dd>
</dl>

<dl>
<dd>

**request_options:** `typing.Optional[RequestOptions]` — Request-specific configuration.
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.billing.invoices.<a href="src/wavix/billing/invoices/client.py">download</a>(...) -> typing.Iterator[bytes]</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Returns the financial statement identified by `id` as a PDF file.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```python
from wavix import Wavix
from wavix.environment import WavixEnvironment

client = Wavix(
    token="<token>",
    environment=WavixEnvironment.DEFAULT,
)

client.billing.invoices.download(
    id=1,
)

```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**id:** `int` — The unique ID of the financial statement to download.
    
</dd>
</dl>

<dl>
<dd>

**request_options:** `typing.Optional[RequestOptions]` — Request-specific configuration.
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

## Buy Countries
<details><summary><code>client.buy.countries.<a href="src/wavix/buy/countries/client.py">list</a>(...) -> CountryListResponse</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Returns a list of countries where phone numbers are available.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```python
from wavix import Wavix
from wavix.environment import WavixEnvironment

client = Wavix(
    token="<token>",
    environment=WavixEnvironment.DEFAULT,
)

client.buy.countries.list()

```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**text_enabled_only:** `typing.Optional[bool]` — When `true`, returns only countries that offer text-enabled phone numbers.
    
</dd>
</dl>

<dl>
<dd>

**request_options:** `typing.Optional[RequestOptions]` — Request-specific configuration.
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

## Buy Regions
<details><summary><code>client.buy.regions.<a href="src/wavix/buy/regions/client.py">list</a>(...) -> RegionListResponse</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Returns a list of regions (states or provinces) for countries where `has_provinces_or_states` is `true`.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```python
from wavix import Wavix
from wavix.environment import WavixEnvironment

client = Wavix(
    token="<token>",
    environment=WavixEnvironment.DEFAULT,
)

client.buy.regions.list(
    country_id=1892,
)

```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**country_id:** `int` — The unique ID of the country.
    
</dd>
</dl>

<dl>
<dd>

**text_enabled_only:** `typing.Optional[bool]` — When `true`, returns only regions that offer text-enabled numbers.
    
</dd>
</dl>

<dl>
<dd>

**request_options:** `typing.Optional[RequestOptions]` — Request-specific configuration.
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

## Buy Cities
<details><summary><code>client.buy.cities.<a href="src/wavix/buy/cities/client.py">list</a>(...) -> CityListResponse</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Returns a list of cities for countries where
 `has_provinces_or_states` is `false`.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```python
from wavix import Wavix
from wavix.environment import WavixEnvironment

client = Wavix(
    token="<token>",
    environment=WavixEnvironment.DEFAULT,
)

client.buy.cities.list(
    country_id=1891,
)

```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**country_id:** `int` — The unique ID of the country.
    
</dd>
</dl>

<dl>
<dd>

**text_enabled_only:** `typing.Optional[bool]` — When `true`, returns only cities that offer text-enabled numbers.
    
</dd>
</dl>

<dl>
<dd>

**request_options:** `typing.Optional[RequestOptions]` — Request-specific configuration.
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

## Buy RegionCities
<details><summary><code>client.buy.region_cities.<a href="src/wavix/buy/region_cities/client.py">list</a>(...) -> CityListResponse</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Returns a list of cities in the specified region for countries where `has_provinces_or_states` is `true`.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```python
from wavix import Wavix
from wavix.environment import WavixEnvironment

client = Wavix(
    token="<token>",
    environment=WavixEnvironment.DEFAULT,
)

client.buy.region_cities.list(
    country_id=1891,
    region_id=821,
)

```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**country_id:** `int` — The unique ID of the country.
    
</dd>
</dl>

<dl>
<dd>

**region_id:** `int` — The unique ID of the region.
    
</dd>
</dl>

<dl>
<dd>

**text_enabled_only:** `typing.Optional[bool]` — When `true`, returns only cities that offer text-enabled numbers.
    
</dd>
</dl>

<dl>
<dd>

**request_options:** `typing.Optional[RequestOptions]` — Request-specific configuration.
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

## Buy Numbers
<details><summary><code>client.buy.numbers.<a href="src/wavix/buy/numbers/client.py">list</a>(...) -> AvailableNumberListResponse</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Returns a paginated list of phone numbers available for purchase in the specified city.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```python
from wavix import Wavix
from wavix.environment import WavixEnvironment

client = Wavix(
    token="<token>",
    environment=WavixEnvironment.DEFAULT,
)

client.buy.numbers.list(
    country_id=1,
    city_id=1,
)

```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**country_id:** `int` — The unique ID of the country.
    
</dd>
</dl>

<dl>
<dd>

**city_id:** `int` — The unique ID of the city.
    
</dd>
</dl>

<dl>
<dd>

**text_enabled_only:** `typing.Optional[bool]` — When `true`, returns only text-enabled phone numbers.
    
</dd>
</dl>

<dl>
<dd>

**page:** `typing.Optional[int]` — Page number to retrieve. Default `1`.
    
</dd>
</dl>

<dl>
<dd>

**per_page:** `typing.Optional[int]` — Number of records to return per page. Default `25`.
    
</dd>
</dl>

<dl>
<dd>

**request_options:** `typing.Optional[RequestOptions]` — Request-specific configuration.
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

## CallControl Streams
<details><summary><code>client.call_control.streams.<a href="src/wavix/call_control/streams/client.py">create</a>(...) -> CallStreamResponse</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Starts streaming the audio of the call identified by `call_id` to a WebSocket destination you supply, in the direction (`stream_type`) and channel (`stream_channel`) you configure. The destination can be any URL you specify — Wavix does not restrict it. Returns the `stream_id`.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```python
from wavix import Wavix
from wavix.environment import WavixEnvironment

client = Wavix(
    token="<token>",
    environment=WavixEnvironment.DEFAULT,
)

client.call_control.streams.create(
    call_id="call_id",
    stream_url="wss://examples.com/stream",
    stream_type="oneway",
    stream_channel="inbound",
)

```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**call_id:** `str` — The `uuid` of the call.
    
</dd>
</dl>

<dl>
<dd>

**stream_url:** `str` — WebSocket URL for call streaming
    
</dd>
</dl>

<dl>
<dd>

**stream_type:** `CallStreamType` — Direction of audio streamed to `stream_url`.
    
</dd>
</dl>

<dl>
<dd>

**stream_channel:** `CallStreamChannel` — Audio channel streamed to `stream_url`.
    
</dd>
</dl>

<dl>
<dd>

**request_options:** `typing.Optional[RequestOptions]` — Request-specific configuration.
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.call_control.streams.<a href="src/wavix/call_control/streams/client.py">delete</a>(...) -> SuccessResponse</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Stops the media stream identified by `id` on the call identified by `call_id`.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```python
from wavix import Wavix
from wavix.environment import WavixEnvironment

client = Wavix(
    token="<token>",
    environment=WavixEnvironment.DEFAULT,
)

client.call_control.streams.delete(
    call_id="call_id",
    id="id",
)

```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**call_id:** `str` — The `uuid` of the call.
    
</dd>
</dl>

<dl>
<dd>

**id:** `str` — The `uuid` of the media stream to stop.
    
</dd>
</dl>

<dl>
<dd>

**request_options:** `typing.Optional[RequestOptions]` — Request-specific configuration.
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

## CallControl Audio
<details><summary><code>client.call_control.audio.<a href="src/wavix/call_control/audio/client.py">play</a>(...) -> SuccessResponse</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Plays an audio prompt into the active call identified by `id`. The audio is audible to the remote party in real time.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```python
from wavix import Wavix
from wavix.environment import WavixEnvironment

client = Wavix(
    token="<token>",
    environment=WavixEnvironment.DEFAULT,
)

client.call_control.audio.play(
    id="id",
    audio_file="https://examples.com/audio.wav",
)

```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**id:** `str` — The `uuid` of the call.
    
</dd>
</dl>

<dl>
<dd>

**audio_file:** `str` — URL of the audio file to play to the call.
    
</dd>
</dl>

<dl>
<dd>

**request_options:** `typing.Optional[RequestOptions]` — Request-specific configuration.
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.call_control.audio.<a href="src/wavix/call_control/audio/client.py">stop</a>(...) -> SuccessResponse</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Stops audio playback in the active call identified by `id`.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```python
from wavix import Wavix
from wavix.environment import WavixEnvironment

client = Wavix(
    token="<token>",
    environment=WavixEnvironment.DEFAULT,
)

client.call_control.audio.stop(
    id="id",
)

```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**id:** `str` — The `uuid` of the call.
    
</dd>
</dl>

<dl>
<dd>

**request_options:** `typing.Optional[RequestOptions]` — Request-specific configuration.
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

## Cdrs Transcription
<details><summary><code>client.cdrs.transcription.<a href="src/wavix/cdrs/transcription/client.py">get</a>(...) -> CdrTranscriptionResponse</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Returns the transcription of the recorded call identified by `call_id`, including the transcript, speaker turns, and summary.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```python
from wavix import Wavix
from wavix.environment import WavixEnvironment

client = Wavix(
    token="<token>",
    environment=WavixEnvironment.DEFAULT,
)

client.cdrs.transcription.get(
    call_id="bbaa37bf-430a-46da-ade3-c248e4070160",
)

```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**call_id:** `str` — The unique ID of the call.
    
</dd>
</dl>

<dl>
<dd>

**request_options:** `typing.Optional[RequestOptions]` — Request-specific configuration.
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

## LinkShortener Metrics
<details><summary><code>client.link_shortener.metrics.<a href="src/wavix/link_shortener/metrics/client.py">list</a>(...) -> ShortLinkMetricsResponse</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Returns per-click metrics for short links, including device, location, and campaign attribution, within the requested date range.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```python
from wavix import Wavix
from wavix.environment import WavixEnvironment
import datetime

client = Wavix(
    token="<token>",
    environment=WavixEnvironment.DEFAULT,
)

client.link_shortener.metrics.list(
    from_=datetime.date.fromisoformat("2023-05-01"),
    to=datetime.date.fromisoformat("2023-05-31"),
    phone="1872025555",
    utm_campaign="summer",
    page=1,
    per_page=25,
)

```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**from:** `datetime.date` — Start of the date range to query, in `YYYY-MM-DD` format. Inclusive.
    
</dd>
</dl>

<dl>
<dd>

**to:** `datetime.date` — End of the date range to query, in `YYYY-MM-DD` format. Inclusive.
    
</dd>
</dl>

<dl>
<dd>

**phone:** `typing.Optional[str]` — Filters metrics by the phone number associated with the click, in E.164 format.
    
</dd>
</dl>

<dl>
<dd>

**utm_campaign:** `typing.Optional[str]` — Filters metrics by `utm_campaign` name.
    
</dd>
</dl>

<dl>
<dd>

**page:** `typing.Optional[int]` — Page number to retrieve. Default `1`.
    
</dd>
</dl>

<dl>
<dd>

**per_page:** `typing.Optional[int]` — Number of records to return per page. Default `25`.
    
</dd>
</dl>

<dl>
<dd>

**request_options:** `typing.Optional[RequestOptions]` — Request-specific configuration.
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

## NumberValidator Results
<details><summary><code>client.number_validator.results.<a href="src/wavix/number_validator/results/client.py">get</a>(...) -> PhoneValidationBatchResultResponse</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Returns the results of an asynchronous batch validation identified by `request_id`.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```python
from wavix import Wavix
from wavix.environment import WavixEnvironment

client = Wavix(
    token="<token>",
    environment=WavixEnvironment.DEFAULT,
)

client.number_validator.results.get(
    request_id="12542c5c-1a17-4d12-a163-5b68543e75f6",
)

```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**request_id:** `str` — The `request_id` returned by the asynchronous bulk validation request.
    
</dd>
</dl>

<dl>
<dd>

**request_options:** `typing.Optional[RequestOptions]` — Request-specific configuration.
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

## Numbers Papers
<details><summary><code>client.numbers.papers.<a href="src/wavix/numbers/papers/client.py">upload</a>(...) -> typing.List[NumberDocument]</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Uploads a verification document for one or more phone numbers.
Uploaded files must meet the following requirements:
- Allowed formats: PNG, JPG, JPEG, TIFF, BMP, or PDF
- Maximum file size: 10 MB
- Files can't be password protected
- PDF files must not contain digital signatures
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```python
from wavix import Wavix
from wavix.environment import WavixEnvironment

client = Wavix(
    token="<token>",
    environment=WavixEnvironment.DEFAULT,
)

client.numbers.papers.upload(
    doc_attachment="example_doc_attachment",
    did_ids="did_ids",
    doc_id="id",
)

```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**did_ids:** `str` — Comma-separated record IDs of the phone numbers the document applies to.
    
</dd>
</dl>

<dl>
<dd>

**doc_attachment:** `core.File` — Document file to upload. Allowed formats are PNG, JPG, JPEG, TIFF, BMP, and PDF. Maximum size is 10 MB.
    
</dd>
</dl>

<dl>
<dd>

**doc_id:** `DocumentType` 
    
</dd>
</dl>

<dl>
<dd>

**request_options:** `typing.Optional[RequestOptions]` — Request-specific configuration.
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

## Profile Config
<details><summary><code>client.profile.config.<a href="src/wavix/profile/config/client.py">get</a>() -> ProfileConfigResponse</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Returns the balance and global limits configured for the authenticated account.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```python
from wavix import Wavix
from wavix.environment import WavixEnvironment

client = Wavix(
    token="<token>",
    environment=WavixEnvironment.DEFAULT,
)

client.profile.config.get()

```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**request_options:** `typing.Optional[RequestOptions]` — Request-specific configuration.
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

## SmsAndMms SenderIds
<details><summary><code>client.sms_and_mms.sender_ids.<a href="src/wavix/sms_and_mms/sender_ids/client.py">list</a>() -> SenderIdListResponse</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Returns the Sender IDs registered for the authenticated account.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```python
from wavix import Wavix
from wavix.environment import WavixEnvironment

client = Wavix(
    token="<token>",
    environment=WavixEnvironment.DEFAULT,
)

client.sms_and_mms.sender_ids.list()

```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**request_options:** `typing.Optional[RequestOptions]` — Request-specific configuration.
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.sms_and_mms.sender_ids.<a href="src/wavix/sms_and_mms/sender_ids/client.py">create</a>(...) -> SenderIdDetails</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Creates a Sender ID. Use the 10DLC API to create Sender IDs in the US. Registering a Sender ID incurs a recurring monthly fee, billed to the account balance.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```python
from wavix import Wavix
from wavix.environment import WavixEnvironment

client = Wavix(
    token="<token>",
    environment=WavixEnvironment.DEFAULT,
)

client.sms_and_mms.sender_ids.create(
    sender_id="Wavix",
    type="numeric",
    countries=[
        "countries"
    ],
    usecase="transactional",
)

```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**sender_id:** `str` — Sender ID name. Can be either an alphanumeric string or a  phone number.
    
</dd>
</dl>

<dl>
<dd>

**type:** `SenderIdType` 
    
</dd>
</dl>

<dl>
<dd>

**countries:** `typing.List[str]` — Two-letter ISO country codes where the Sender ID is allowlisted.
    
</dd>
</dl>

<dl>
<dd>

**usecase:** `SenderIdCreateRequestUsecase` — Primary use case for the Sender ID. One of `transactional` (account or order notifications), `promo` (marketing and promotional messages), or `authentication` (one-time passcodes and verification codes).
    
</dd>
</dl>

<dl>
<dd>

**monthly_volume:** `typing.Optional[SenderIdCreateRequestMonthlyVolume]` — Expected number of messages sent per month from the Sender ID. One of `1-1000`, `1001-20000`, `20001-50000`, `50001-100000`, or `More than 100000`. Each value is the message-count band for the month.
    
</dd>
</dl>

<dl>
<dd>

**samples:** `typing.Optional[typing.List[str]]` — Message samples.
    
</dd>
</dl>

<dl>
<dd>

**request_options:** `typing.Optional[RequestOptions]` — Request-specific configuration.
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.sms_and_mms.sender_ids.<a href="src/wavix/sms_and_mms/sender_ids/client.py">get</a>(...) -> SenderIdResponse</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Returns the Sender ID identified by `id`.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```python
from wavix import Wavix
from wavix.environment import WavixEnvironment

client = Wavix(
    token="<token>",
    environment=WavixEnvironment.DEFAULT,
)

client.sms_and_mms.sender_ids.get(
    id="id",
)

```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**id:** `str` — The unique ID of the Sender ID.
    
</dd>
</dl>

<dl>
<dd>

**request_options:** `typing.Optional[RequestOptions]` — Request-specific configuration.
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.sms_and_mms.sender_ids.<a href="src/wavix/sms_and_mms/sender_ids/client.py">delete</a>(...) -> SuccessResponse</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Deletes the Sender ID identified by `id`. Deletion is permanent.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```python
from wavix import Wavix
from wavix.environment import WavixEnvironment

client = Wavix(
    token="<token>",
    environment=WavixEnvironment.DEFAULT,
)

client.sms_and_mms.sender_ids.delete(
    id="fc34ba88-1eee-476e-b09e-dae63dc441e0",
)

```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**id:** `str` — The unique ID of the Sender ID.
    
</dd>
</dl>

<dl>
<dd>

**request_options:** `typing.Optional[RequestOptions]` — Request-specific configuration.
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

## SmsAndMms OptOuts
<details><summary><code>client.sms_and_mms.opt_outs.<a href="src/wavix/sms_and_mms/opt_outs/client.py">list</a>(...) -> OptOutsListResponse</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Returns a paginated list of phone numbers that have opted out of receiving messages from the authenticated account.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```python
from wavix import Wavix
from wavix.environment import WavixEnvironment
import datetime

client = Wavix(
    token="<token>",
    environment=WavixEnvironment.DEFAULT,
)

client.sms_and_mms.opt_outs.list(
    sender_id="MySender",
    campaign_id="C123456",
    created_after=datetime.date.fromisoformat("2024-01-01"),
    created_before=datetime.date.fromisoformat("2024-12-31"),
)

```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**sender_id:** `typing.Optional[str]` — Filters opt-outs by the Sender ID they apply to.
    
</dd>
</dl>

<dl>
<dd>

**campaign_id:** `typing.Optional[str]` — Filters opt-outs by the 10DLC campaign ID they apply to.
    
</dd>
</dl>

<dl>
<dd>

**created_after:** `typing.Optional[datetime.date]` — Returns opt-outs created on or after this date, in `YYYY-MM-DD` format.
    
</dd>
</dl>

<dl>
<dd>

**created_before:** `typing.Optional[datetime.date]` — Returns opt-outs created on or before this date, in `YYYY-MM-DD` format.
    
</dd>
</dl>

<dl>
<dd>

**page:** `typing.Optional[int]` — Page number to retrieve. Minimum `1`, default `1`.
    
</dd>
</dl>

<dl>
<dd>

**per_page:** `typing.Optional[int]` — Number of records to return per page. Default `25`, maximum `100`.
    
</dd>
</dl>

<dl>
<dd>

**request_options:** `typing.Optional[RequestOptions]` — Request-specific configuration.
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.sms_and_mms.opt_outs.<a href="src/wavix/sms_and_mms/opt_outs/client.py">create</a>(...) -> SuccessResponse</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Opts a phone number out of receiving messages from a Sender ID, a 10DLC campaign, or all outbound messages.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```python
from wavix import Wavix, OptOut
from wavix.environment import WavixEnvironment

client = Wavix(
    token="<token>",
    environment=WavixEnvironment.DEFAULT,
)

client.sms_and_mms.opt_outs.create(
    opt_out=OptOut(
        number="16419252149",
        sender_id="15072429497",
    ),
)

```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**opt_out:** `OptOut` 
    
</dd>
</dl>

<dl>
<dd>

**request_options:** `typing.Optional[RequestOptions]` — Request-specific configuration.
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

## SmsAndMms Messages
<details><summary><code>client.sms_and_mms.messages.<a href="src/wavix/sms_and_mms/messages/client.py">list</a>(...) -> MessageListResponse</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Returns a paginated list of SMS and MMS messages for the authenticated account, filtered by direction, date, and other criteria.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```python
from wavix import Wavix
from wavix.environment import WavixEnvironment
import datetime

client = Wavix(
    token="<token>",
    environment=WavixEnvironment.DEFAULT,
)

client.sms_and_mms.messages.list(
    sent_after=datetime.date.fromisoformat("2023-04-10"),
    sent_before=datetime.date.fromisoformat("2023-04-13"),
    type="outbound",
    from_="15072429497",
    to="16419252149",
    tag="campaignX",
    page=2,
    per_page=50,
)

```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**type:** `str` — Filters messages by direction. One of `inbound` (messages received by the account) or `outbound` (messages sent by the account).
    
</dd>
</dl>

<dl>
<dd>

**sent_after:** `typing.Optional[datetime.date]` — Returns messages sent on or after this date, in `YYYY-MM-DD` format.
    
</dd>
</dl>

<dl>
<dd>

**sent_before:** `typing.Optional[datetime.date]` — Returns messages sent on or before this date, in `YYYY-MM-DD` format.
    
</dd>
</dl>

<dl>
<dd>

**from:** `typing.Optional[str]` — Filters by message sender. For `outbound` messages, the Sender ID used to send the message; for `inbound` messages, the originating phone number.
    
</dd>
</dl>

<dl>
<dd>

**to:** `typing.Optional[str]` — Filters by message recipient. For `outbound` messages, the destination phone number; for `inbound` messages, an SMS-enabled number on the Wavix platform.
    
</dd>
</dl>

<dl>
<dd>

**status:** `typing.Optional[MessageDeliveryStatus]` — Filters messages by delivery status. Accepts a `MessageDeliveryStatus` value.
    
</dd>
</dl>

<dl>
<dd>

**tag:** `typing.Optional[str]` — Filters messages by `tag`. Supported for outbound messages only.
    
</dd>
</dl>

<dl>
<dd>

**message_type:** `typing.Optional[ListMessagesRequestMessageType]` — Filters messages by type. One of `sms` (text message) or `mms` (multimedia message).
    
</dd>
</dl>

<dl>
<dd>

**page:** `typing.Optional[int]` — Page number to retrieve. Default `1`.
    
</dd>
</dl>

<dl>
<dd>

**per_page:** `typing.Optional[int]` — Number of records to return per page. Default `25`.
    
</dd>
</dl>

<dl>
<dd>

**request_options:** `typing.Optional[RequestOptions]` — Request-specific configuration.
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.sms_and_mms.messages.<a href="src/wavix/sms_and_mms/messages/client.py">send</a>(...) -> SendMessagesResponse</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Sends an SMS or MMS message. MMS is supported for U.S. numbers only. Track delivery using the returned `message_id` and the message status callback. The recipient must be opted in to receive messages from the account; sending to an opted-out number fails.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```python
from wavix import Wavix, MessageBody
from wavix.environment import WavixEnvironment

client = Wavix(
    token="<token>",
    environment=WavixEnvironment.DEFAULT,
)

client.sms_and_mms.messages.send(
    from_="Wavix",
    to="+447537151866",
    message_body=MessageBody(
        text="Hi there, this is a message from Wavix",
    ),
    callback_url="https://you-site.com/webhook",
    validity=3600,
    tag="Fall sale",
)

```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**from:** `str` — Sender ID. Numeric or alphanumeric.
    
</dd>
</dl>

<dl>
<dd>

**to:** `str` — Recipient phone number.
    
</dd>
</dl>

<dl>
<dd>

**message_body:** `MessageBody` 
    
</dd>
</dl>

<dl>
<dd>

**callback_url:** `typing.Optional[str]` — Callback URL for delivery reports.
    
</dd>
</dl>

<dl>
<dd>

**validity:** `typing.Optional[int]` — Message validity period in seconds. Delivery attempts stop after this period expires.
    
</dd>
</dl>

<dl>
<dd>

**tag:** `typing.Optional[str]` — Tag to group messages, such as for a specific campaign.
    
</dd>
</dl>

<dl>
<dd>

**request_options:** `typing.Optional[RequestOptions]` — Request-specific configuration.
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.sms_and_mms.messages.<a href="src/wavix/sms_and_mms/messages/client.py">get</a>(...) -> MessageResponse</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Returns the SMS or MMS message identified by `id`, including its delivery status and content.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```python
from wavix import Wavix
from wavix.environment import WavixEnvironment

client = Wavix(
    token="<token>",
    environment=WavixEnvironment.DEFAULT,
)

client.sms_and_mms.messages.get(
    id="3a525ca2-6909-4c72-9399-905adf7f3a74",
)

```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**id:** `str` — The unique ID of the message.
    
</dd>
</dl>

<dl>
<dd>

**request_options:** `typing.Optional[RequestOptions]` — Request-specific configuration.
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.sms_and_mms.messages.<a href="src/wavix/sms_and_mms/messages/client.py">list_all</a>(...) -> str</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Streams matching SMS and MMS messages as newline-delimited JSON (NDJSON), one message per line, for bulk export.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```python
from wavix import Wavix
from wavix.environment import WavixEnvironment

client = Wavix(
    token="<token>",
    environment=WavixEnvironment.DEFAULT,
)

client.sms_and_mms.messages.list_all(
    sent_after="2023-04-10T00:00:00",
    sent_before="2023-04-13T23:59:59",
    type="outbound",
    from_="15072429497",
    to="16419252149",
    tag="campaignX",
)

```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**type:** `str` — Filters messages by direction. One of `inbound` (messages received by the account) or `outbound` (messages sent by the account).
    
</dd>
</dl>

<dl>
<dd>

**sent_after:** `typing.Optional[str]` — Returns messages sent on or after this timestamp, in `YYYY-MM-DDTHH:MM:SS` format.
    
</dd>
</dl>

<dl>
<dd>

**sent_before:** `typing.Optional[str]` — Returns messages sent on or before this timestamp, in `YYYY-MM-DDTHH:MM:SS` format.
    
</dd>
</dl>

<dl>
<dd>

**from:** `typing.Optional[str]` — Filters by message sender. For `outbound` messages, the Sender ID used to send the message; for `inbound` messages, the originating phone number.
    
</dd>
</dl>

<dl>
<dd>

**to:** `typing.Optional[str]` — Filters by message recipient. For `outbound` messages, the destination phone number; for `inbound` messages, the SMS-enabled number that received the message.
    
</dd>
</dl>

<dl>
<dd>

**status:** `typing.Optional[MessageDeliveryStatus]` — Filters messages by delivery status. Accepts a `MessageDeliveryStatus` value.
    
</dd>
</dl>

<dl>
<dd>

**tag:** `typing.Optional[str]` — Filters messages by `tag`. Supported for outbound messages only.
    
</dd>
</dl>

<dl>
<dd>

**message_type:** `typing.Optional[ListAllMessagesRequestMessageType]` — Filters messages by type. One of `sms` (text message) or `mms` (multimedia message).
    
</dd>
</dl>

<dl>
<dd>

**request_options:** `typing.Optional[RequestOptions]` — Request-specific configuration.
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

## SpeechAnalytics File
<details><summary><code>client.speech_analytics.file.<a href="src/wavix/speech_analytics/file/client.py">get</a>(...) -> typing.Iterator[bytes]</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Returns the original audio file submitted for the transcription identified by `request_id`.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```python
from wavix import Wavix
from wavix.environment import WavixEnvironment

client = Wavix(
    token="<token>",
    environment=WavixEnvironment.DEFAULT,
)

client.speech_analytics.file.get(
    request_id="request_id",
)

```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**request_id:** `str` — The `request_id` of the transcription, returned when the file was uploaded.
    
</dd>
</dl>

<dl>
<dd>

**request_options:** `typing.Optional[RequestOptions]` — Request-specific configuration.
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

## SubAccounts Transactions
<details><summary><code>client.sub_accounts.transactions.<a href="src/wavix/sub_accounts/transactions/client.py">list</a>(...) -> SubAccountsTransactionsListResponse</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Returns a paginated list of billing transactions for the sub-account identified by `id`, within the requested date range.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```python
from wavix import Wavix
from wavix.environment import WavixEnvironment
import datetime

client = Wavix(
    token="<token>",
    environment=WavixEnvironment.DEFAULT,
)

client.sub_accounts.transactions.list(
    id=123,
    from_date=datetime.date.fromisoformat("2023-01-01"),
    to_date=datetime.date.fromisoformat("2023-12-31"),
    type=[
        1
    ],
    page=1,
    per_page=25,
)

```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**id:** `int` — The unique ID of the sub-account.
    
</dd>
</dl>

<dl>
<dd>

**from_date:** `datetime.date` — Start of the date range to query, in `YYYY-MM-DD` format. Inclusive.
    
</dd>
</dl>

<dl>
<dd>

**to_date:** `datetime.date` — End of the date range to query, in `YYYY-MM-DD` format. Inclusive.
    
</dd>
</dl>

<dl>
<dd>

**type:** `typing.Optional[typing.Union[int, typing.Sequence[int]]]` — Filters transactions by type. Accepts a single transaction type code or an array of codes.
    
</dd>
</dl>

<dl>
<dd>

**page:** `typing.Optional[int]` — Page number to retrieve. Default `1`.
    
</dd>
</dl>

<dl>
<dd>

**per_page:** `typing.Optional[int]` — Number of records to return per page. Default `25`.
    
</dd>
</dl>

<dl>
<dd>

**request_options:** `typing.Optional[RequestOptions]` — Request-specific configuration.
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

## TenDlc Brands
<details><summary><code>client.ten_dlc.brands.<a href="src/wavix/ten_dlc/brands/client.py">list</a>(...) -> TenDlcBrandListResponse</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Returns a paginated list of 10DLC Brands for the authenticated account, filtered by date, name, legal name, and status.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```python
from wavix import Wavix
from wavix.environment import WavixEnvironment

client = Wavix(
    token="<token>",
    environment=WavixEnvironment.DEFAULT,
)

client.ten_dlc.brands.list(
    dba_name="Brand",
    company_name="Company",
    entity_type="PRIVATE_PROFIT",
    status="VERIFIED",
    country="US",
    show_deleted=False,
    ein_taxid="999999999",
    mock=False,
    created_before="2024-08-22",
    created_after="2024-08-22",
    page=1,
    per_page=25,
)

```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**dba_name:** `typing.Optional[str]` — Filters Brands by `dba_name` (doing-business-as name). Matches partial values.
    
</dd>
</dl>

<dl>
<dd>

**company_name:** `typing.Optional[str]` — Filters Brands by `company_name` (registered legal name). Matches partial values.
    
</dd>
</dl>

<dl>
<dd>

**entity_type:** `typing.Optional[str]` — Filters Brands by business entity type, such as `PRIVATE_PROFIT`.
    
</dd>
</dl>

<dl>
<dd>

**status:** `typing.Optional[str]` — Filters Brands by identity verification status, such as `VERIFIED`.
    
</dd>
</dl>

<dl>
<dd>

**country:** `typing.Optional[str]` — Filters Brands by registration country, as an ISO 3166-1 alpha-2 code (e.g., `US`).
    
</dd>
</dl>

<dl>
<dd>

**show_deleted:** `typing.Optional[bool]` — When `true`, includes deleted Brands in the results. Default `false`.
    
</dd>
</dl>

<dl>
<dd>

**ein_taxid:** `typing.Optional[str]` — Filters Brands by their Employer Identification Number (EIN) or tax ID.
    
</dd>
</dl>

<dl>
<dd>

**mock:** `typing.Optional[bool]` — When `true`, returns only mock Brands used for testing. Default `false`.
    
</dd>
</dl>

<dl>
<dd>

**created_before:** `typing.Optional[str]` — Returns brands created on or before this date, in `YYYY-MM-DD` format.
    
</dd>
</dl>

<dl>
<dd>

**created_after:** `typing.Optional[str]` — Returns brands created on or after this date, in `YYYY-MM-DD` format.
    
</dd>
</dl>

<dl>
<dd>

**page:** `typing.Optional[int]` — Page number to retrieve. Default `1`.
    
</dd>
</dl>

<dl>
<dd>

**per_page:** `typing.Optional[int]` — Number of records to return per page. Default `25`.
    
</dd>
</dl>

<dl>
<dd>

**request_options:** `typing.Optional[RequestOptions]` — Request-specific configuration.
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.ten_dlc.brands.<a href="src/wavix/ten_dlc/brands/client.py">create</a>(...) -> TenDlcBrand</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Registers a 10DLC Brand. Submits the company's legal identity data (EIN/Tax ID, legal company name, contact and address) to The Campaign Registry (TCR), which verifies the brand identity. Charges a 10DLC brand registration fee on successful submission; fails with an insufficient-funds error when the balance cannot cover it. Only brands with `VERIFIED` or `VETTED_VERIFIED` identity status can register 10DLC Campaigns.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```python
from wavix import Wavix, TenDlcBrandCreateRequestZero
from wavix.environment import WavixEnvironment

client = Wavix(
    token="<token>",
    environment=WavixEnvironment.DEFAULT,
)

client.ten_dlc.brands.create(
    request=TenDlcBrandCreateRequestZero(),
)

```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**request:** `TenDlcBrandCreateRequest` 
    
</dd>
</dl>

<dl>
<dd>

**request_options:** `typing.Optional[RequestOptions]` — Request-specific configuration.
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.ten_dlc.brands.<a href="src/wavix/ten_dlc/brands/client.py">get</a>(...) -> TenDlcBrand</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Returns the 10DLC Brand identified by `brand_id`.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```python
from wavix import Wavix
from wavix.environment import WavixEnvironment

client = Wavix(
    token="<token>",
    environment=WavixEnvironment.DEFAULT,
)

client.ten_dlc.brands.get(
    brand_id="BM20QP9",
)

```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**brand_id:** `str` — The unique ID of the 10DLC Brand.
    
</dd>
</dl>

<dl>
<dd>

**request_options:** `typing.Optional[RequestOptions]` — Request-specific configuration.
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.ten_dlc.brands.<a href="src/wavix/ten_dlc/brands/client.py">update</a>(...) -> TenDlcBrand</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Updates the 10DLC Brand identified by `brand_id`. Changing identity fields, including `ein_taxid`, `ein_taxid_country`, and `entity_type`, resets the Brand status to `UNVERIFIED` and triggers automatic re-submission. Brands in `VETTED_VERIFIED` status or with active Campaigns cannot be updated.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```python
from wavix import Wavix
from wavix.environment import WavixEnvironment

client = Wavix(
    token="<token>",
    environment=WavixEnvironment.DEFAULT,
)

client.ten_dlc.brands.update(
    brand_id="BM20QP9",
)

```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**brand_id:** `str` — The unique ID of the 10DLC Brand.
    
</dd>
</dl>

<dl>
<dd>

**dba_name:** `typing.Optional[str]` — Brand name or DBA
    
</dd>
</dl>

<dl>
<dd>

**company_name:** `typing.Optional[str]` — Legal name of the company
    
</dd>
</dl>

<dl>
<dd>

**entity_type:** `typing.Optional[TenDlcBrandUpdateRequestEntityType]` — Legal entity type of the company. One of `PRIVATE_PROFIT` (privately held for-profit company), `PUBLIC_PROFIT` (publicly traded for-profit company), `NON_PROFIT` (non-profit organization), or `GOVERNMENT` (government entity).
    
</dd>
</dl>

<dl>
<dd>

**vertical:** `typing.Optional[TenDlcBrandUpdateRequestVertical]` 

Business segment the Brand operates in. One of:

- `HEALTHCARE` — healthcare.
- `PROFESSIONAL` — professional services.
- `RETAIL` — retail.
- `TECHNOLOGY` — technology.
- `EDUCATION` — education.
- `FINANCIAL` — financial services.
- `NON_PROFIT` — non-profit organizations.
- `GOVERNMENT` — government entities.
- `OTHER` — any segment not listed above.
    
</dd>
</dl>

<dl>
<dd>

**ein_taxid:** `typing.Optional[str]` — IRS Employee Identification Number (EIN) for US-based or foreign companies with EIN. The numeric portion of Tax ID for companies incorporated in other countries.
    
</dd>
</dl>

<dl>
<dd>

**ein_taxid_country:** `typing.Optional[str]` — 2-letter ISO country code of the Tax ID issuing country
    
</dd>
</dl>

<dl>
<dd>

**website:** `typing.Optional[str]` — The website of the business
    
</dd>
</dl>

<dl>
<dd>

**stock_symbol:** `typing.Optional[str]` — The stock symbol of the Brand. For PUBLIC_PROFIT Brands only.
    
</dd>
</dl>

<dl>
<dd>

**stock_exchange:** `typing.Optional[str]` — The stock exchange code. For PUBLIC_PROFIT Brands only.
    
</dd>
</dl>

<dl>
<dd>

**first_name:** `typing.Optional[str]` — The first name of the business contact
    
</dd>
</dl>

<dl>
<dd>

**last_name:** `typing.Optional[str]` — The last name of the business contact
    
</dd>
</dl>

<dl>
<dd>

**phone_number:** `typing.Optional[str]` — The support contact telephone in E.164 format
    
</dd>
</dl>

<dl>
<dd>

**email:** `typing.Optional[str]` — The email address of the support contact
    
</dd>
</dl>

<dl>
<dd>

**street_address:** `typing.Optional[str]` — Street name and house number
    
</dd>
</dl>

<dl>
<dd>

**city:** `typing.Optional[str]` — The city name
    
</dd>
</dl>

<dl>
<dd>

**state_or_province:** `typing.Optional[str]` — State or province. For the United States, use 2 character codes.
    
</dd>
</dl>

<dl>
<dd>

**zip:** `typing.Optional[str]` — The business zip or postal code
    
</dd>
</dl>

<dl>
<dd>

**country:** `typing.Optional[str]` — 2-letter ISO country code the business address
    
</dd>
</dl>

<dl>
<dd>

**mock:** `typing.Optional[bool]` — Mock flag for testing (optional, defaults to false)
    
</dd>
</dl>

<dl>
<dd>

**request_options:** `typing.Optional[RequestOptions]` — Request-specific configuration.
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.ten_dlc.brands.<a href="src/wavix/ten_dlc/brands/client.py">delete</a>(...) -> SuccessResponse</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Deletes a 10DLC Brand. Brands with active campaigns cannot be deleted.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```python
from wavix import Wavix
from wavix.environment import WavixEnvironment

client = Wavix(
    token="<token>",
    environment=WavixEnvironment.DEFAULT,
)

client.ten_dlc.brands.delete(
    brand_id="BM20QP9",
)

```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**brand_id:** `str` — The unique ID of the 10DLC Brand.
    
</dd>
</dl>

<dl>
<dd>

**request_options:** `typing.Optional[RequestOptions]` — Request-specific configuration.
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.ten_dlc.brands.<a href="src/wavix/ten_dlc/brands/client.py">qualify_usecase</a>(...) -> TenDlcBrandQualificationResult</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Returns the qualification results for a 10DLC Brand use case. Includes MNO-specific attributes, restrictions, and fees.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```python
from wavix import Wavix
from wavix.environment import WavixEnvironment

client = Wavix(
    token="<token>",
    environment=WavixEnvironment.DEFAULT,
)

client.ten_dlc.brands.qualify_usecase(
    brand_id="BMQFB7X",
    use_case="AGENTS_FRANCHISES",
)

```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**brand_id:** `str` — The unique ID of the 10DLC Brand.
    
</dd>
</dl>

<dl>
<dd>

**use_case:** `QualifyUsecaseBrandsRequestUseCase` — Name of the use case to qualify the Brand for.
    
</dd>
</dl>

<dl>
<dd>

**request_options:** `typing.Optional[RequestOptions]` — Request-specific configuration.
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

## TenDlc BrandAppeals
<details><summary><code>client.ten_dlc.brand_appeals.<a href="src/wavix/ten_dlc/brand_appeals/client.py">list</a>(...) -> typing.List[TenDlcBrandAppeal]</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Returns the identity verification appeals submitted for the 10DLC Brand identified by `brand_id`.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```python
from wavix import Wavix
from wavix.environment import WavixEnvironment

client = Wavix(
    token="<token>",
    environment=WavixEnvironment.DEFAULT,
)

client.ten_dlc.brand_appeals.list(
    brand_id="BM20QP9",
)

```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**brand_id:** `str` — The unique ID of the 10DLC Brand.
    
</dd>
</dl>

<dl>
<dd>

**request_options:** `typing.Optional[RequestOptions]` — Request-specific configuration.
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.ten_dlc.brand_appeals.<a href="src/wavix/ten_dlc/brand_appeals/client.py">create</a>(...) -> SuccessResponse</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Submits an appeal for 10DLC brand identity verification. Provide any additional documentation to support the appeal. Use `appeal_category` to specify the appeal type:
- `VERIFY_TAX_ID` — Use if the brand is UNVERIFIED due to a tax ID mismatch. Applies to private companies, public companies, non-profits, and government entities.
- `VERIFY_NON_PROFIT` — Use if a non-profit brand is UNVERIFIED or VERIFIED but missing tax-exempt status.
- `VERIFY_GOVERNMENT` — Use if a government brand is UNVERIFIED or VERIFIED but missing government entity status.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```python
from wavix import Wavix
from wavix.environment import WavixEnvironment

client = Wavix(
    token="<token>",
    environment=WavixEnvironment.DEFAULT,
)

client.ten_dlc.brand_appeals.create(
    brand_id="BM20QP9",
    appeal_categories=[
        "VERIFY_TAX_ID"
    ],
    evidence=[
        "855dff49-c097-4645-3983-08dcb9856232"
    ],
)

```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**brand_id:** `str` — The unique ID of the 10DLC Brand.
    
</dd>
</dl>

<dl>
<dd>

**appeal_categories:** `typing.List[CreateBrandAppealsRequestAppealCategoriesItem]` — List of appeal categories. Allowed values: `VERIFY_TAX_ID`, `VERIFY_NON_PROFIT`, `VERIFY_GOVERNMENT`
    
</dd>
</dl>

<dl>
<dd>

**evidence:** `typing.List[str]` — List of evidence IDs associated with the appeal.
    
</dd>
</dl>

<dl>
<dd>

**explanation:** `typing.Optional[str]` — Appeal comment or justification.
    
</dd>
</dl>

<dl>
<dd>

**request_options:** `typing.Optional[RequestOptions]` — Request-specific configuration.
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

## TenDlc BrandEvidence
<details><summary><code>client.ten_dlc.brand_evidence.<a href="src/wavix/ten_dlc/brand_evidence/client.py">list</a>(...) -> ListBrandEvidenceResponse</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Returns the evidence files uploaded for the 10DLC Brand identified by `brand_id`.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```python
from wavix import Wavix
from wavix.environment import WavixEnvironment

client = Wavix(
    token="<token>",
    environment=WavixEnvironment.DEFAULT,
)

client.ten_dlc.brand_evidence.list(
    brand_id="B6AI7PA",
)

```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**brand_id:** `str` — The unique ID of the 10DLC Brand.
    
</dd>
</dl>

<dl>
<dd>

**request_options:** `typing.Optional[RequestOptions]` — Request-specific configuration.
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.ten_dlc.brand_evidence.<a href="src/wavix/ten_dlc/brand_evidence/client.py">upload</a>(...) -> TenDlcBrandEvidence</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Uploads a supporting evidence file for the 10DLC Brand identified by `brand_id`. Supported formats include `.jpg`, `.png`, and `.pdf`. Maximum size is 10 MB.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```python
from wavix import Wavix
from wavix.environment import WavixEnvironment

client = Wavix(
    token="<token>",
    environment=WavixEnvironment.DEFAULT,
)

client.ten_dlc.brand_evidence.upload(
    brand_id="B6AI7PA",
    file="example_file",
)

```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**brand_id:** `str` — The unique ID of the 10DLC Brand.
    
</dd>
</dl>

<dl>
<dd>

**file:** `core.File` — Evidence file to upload. Maximum size is 10 MB.
    
</dd>
</dl>

<dl>
<dd>

**request_options:** `typing.Optional[RequestOptions]` — Request-specific configuration.
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.ten_dlc.brand_evidence.<a href="src/wavix/ten_dlc/brand_evidence/client.py">get</a>(...) -> typing.Iterator[bytes]</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Returns the Brand evidence file identified by the evidence ID.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```python
from wavix import Wavix
from wavix.environment import WavixEnvironment

client = Wavix(
    token="<token>",
    environment=WavixEnvironment.DEFAULT,
)

client.ten_dlc.brand_evidence.get(
    brand_id="brand_id",
    id="id",
)

```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**brand_id:** `str` — The unique ID of the 10DLC Brand.
    
</dd>
</dl>

<dl>
<dd>

**id:** `str` — The unique ID of the Brand evidence file.
    
</dd>
</dl>

<dl>
<dd>

**request_options:** `typing.Optional[RequestOptions]` — Request-specific configuration.
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.ten_dlc.brand_evidence.<a href="src/wavix/ten_dlc/brand_evidence/client.py">delete</a>(...) -> SuccessResponse</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Deletes the Brand evidence file identified by the evidence ID. Deletion is permanent.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```python
from wavix import Wavix
from wavix.environment import WavixEnvironment

client = Wavix(
    token="<token>",
    environment=WavixEnvironment.DEFAULT,
)

client.ten_dlc.brand_evidence.delete(
    brand_id="B6AI7PA",
    id="191eb205-8357-4d71-b8da-160a25a000d7",
)

```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**brand_id:** `str` — The unique ID of the 10DLC Brand.
    
</dd>
</dl>

<dl>
<dd>

**id:** `str` — The unique ID of the Brand evidence file.
    
</dd>
</dl>

<dl>
<dd>

**request_options:** `typing.Optional[RequestOptions]` — Request-specific configuration.
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

## TenDlc BrandVettings
<details><summary><code>client.ten_dlc.brand_vettings.<a href="src/wavix/ten_dlc/brand_vettings/client.py">list</a>(...) -> typing.List[TenDlcBrandVetting]</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Returns the external vettings for the 10DLC Brand identified by `brand_id`.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```python
from wavix import Wavix
from wavix.environment import WavixEnvironment

client = Wavix(
    token="<token>",
    environment=WavixEnvironment.DEFAULT,
)

client.ten_dlc.brand_vettings.list(
    brand_id="B6AI7PA",
)

```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**brand_id:** `str` — The unique ID of the 10DLC Brand.
    
</dd>
</dl>

<dl>
<dd>

**request_options:** `typing.Optional[RequestOptions]` — Request-specific configuration.
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.ten_dlc.brand_vettings.<a href="src/wavix/ten_dlc/brand_vettings/client.py">create</a>(...) -> TenDlcBrandVetting</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Requests external vetting for a 10DLC Brand. Supported providers: `AEGIS`, `CV`, `WMC`. Supported classes: `STANDARD`, `ENHANCED`. Charges a 10DLC brand vetting fee (Standard or Enhanced); fails with an insufficient-funds error when the balance cannot cover it.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```python
from wavix import Wavix
from wavix.environment import WavixEnvironment

client = Wavix(
    token="<token>",
    environment=WavixEnvironment.DEFAULT,
)

client.ten_dlc.brand_vettings.create(
    brand_id="B6AI7PA",
    evp_id="AEGIS",
    vetting_class="STANDARD",
)

```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**brand_id:** `str` — The unique ID of the 10DLC Brand.
    
</dd>
</dl>

<dl>
<dd>

**evp_id:** `str` — Code identifying the external vetting provider to perform the vetting.
    
</dd>
</dl>

<dl>
<dd>

**vetting_class:** `str` — Class of vetting to request, such as `STANDARD` or `ENHANCED`.
    
</dd>
</dl>

<dl>
<dd>

**request_options:** `typing.Optional[RequestOptions]` — Request-specific configuration.
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.ten_dlc.brand_vettings.<a href="src/wavix/ten_dlc/brand_vettings/client.py">import</a>(...) -> TenDlcBrandVetting</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Imports an existing external vetting record into the 10DLC Brand identified by `brand_id`.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```python
from wavix import Wavix
from wavix.environment import WavixEnvironment

client = Wavix(
    token="<token>",
    environment=WavixEnvironment.DEFAULT,
)

client.ten_dlc.brand_vettings.import_(
    brand_id="B6AI7PA",
    evp_id="AEGIS",
    vetting_id="13d8e00c-3cb4-4dc0-9e26-d5057fa938d9",
    vetting_token="3oDcE1vq8OR43claMa6Thu/7V4vzZywAfKRgiJnXDjlw+08wpWbGqOssAXKgeZibHCLaGgXvU/yPb7kISeeb5qGdisGRLdhPnSNpvRR82RnCWYNpTp92orlJWjTJU8ZGmNxL5MwK0tt/9SxCha36iTtPV2+4vND8xCPe5suItuQTonG4A3Yi6F1LMqihgwdesRjxJnKqcE7Thcv9ug1NyNPYEZQvPugFj2F2DdU6jFZcOWgXsnE7ucZ+xNaNX9LkF9if3v0hrcviG9L8bUUrpPBGr02txP0i+cPBTLbj4Rq1Ox83R+WUx1gnoXHCIU1ByDGWvQq2Ef4qxGVOwPJHJbja1BovxKBk4YJxiz8OSO68QAIEfxuPTpj5eZz7KEFtFmBIVaVmxBDe4b8Tpl01C2rek7xgPzXaoURvh7CQVnVmJL00DTWKvyOmUOQQW901XEcgcJ7VWgfIvxhIMuXEXXtVDGNowmEc9JQXXYHVlGuN5QicSbApkwwqRZI7TQ4lsS66zCfqomIIJyBNRJpl+8sGwsa2J2h6fEkAD77J9zdUgIKXMFamHbvRadCKMZNIbMrkOC7PuOjZdSiWKh5A8FSjzkv3PlN2hRDqkaODEoodp5pTQeBtNe37+uAMOuHNfsZXlwvfMgCZjiZJ9HQNSLhJBUq7/IvT/EzszUk4HPTj/WFSbT1YrrkDi+zrB20ZDY9lZFWxN1hlYQoNcanDAAWPmw/yW1+8DroL5WIMGsXX3WFGOG7eWB1GHgFQsziAeRQl78u1qOvsRMN08+GrkASBJwqwy5l7xCesUKqbz3O0QA/dwzzsWIDvFPavZpjqMBSjRTurQLFahAaGmdY0BX/Ii+s2+OxfaHQIa1lgucm0P7GPKeZvLX/8boO01Onr/87ra+NX7ABvQb+SXvwsg+Bm5CziWB6DMKDKRD/KQjHxpjIY35UwSEW7G4ixux7ufizXttthHfPJWd/rWFhfYigFhVLgIPCR12smwFVuZwM7ujvY2CIM0X4E0dsX9uVHkgYmqRIdNf5vshpmRuIcHsXZpTJP/tD7zQM6m214c5xkJSfAVIaD7WzRYS4eVL+R3z4u+6n5p6FjuWSjSzuEffUai3HCWjes4JbtDSjIwoG0tOMtBukgPbreH+pjXcvnhU+1QhCV2aIdG6C3FmaI5Uoo/mthJyiFAThwtOpxQ5YkdsRunqVVEFYZfMNEn4Ig2clCFrLOm46JB2wPcLGP2MoH5RqajYzQ6IV8IXIFQVzG0C7HoHsBkVp+GrpnH6N0FCKR+fpbGjigM2lLf4pYBhChUY4ao9hvV1hd8ikS6QoasvDLPytBBa1YAwbSa8d7YdwO6fXfQqetfS8S9gbHD0zxazw5p9Lp5fXFmajDNkD2voYNMzOHJMMHG/49pWV2",
)

```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**brand_id:** `str` — The unique ID of the 10DLC Brand.
    
</dd>
</dl>

<dl>
<dd>

**evp_id:** `str` — Code identifying the external vetting provider that issued the vetting.
    
</dd>
</dl>

<dl>
<dd>

**vetting_id:** `str` — Unique identifier of the vetting request to import.
    
</dd>
</dl>

<dl>
<dd>

**vetting_token:** `str` — Token issued by the vetting provider that uniquely identifies the vetting result to import.
    
</dd>
</dl>

<dl>
<dd>

**request_options:** `typing.Optional[RequestOptions]` — Request-specific configuration.
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

## TenDlc BrandVettingAppeals
<details><summary><code>client.ten_dlc.brand_vetting_appeals.<a href="src/wavix/ten_dlc/brand_vetting_appeals/client.py">list</a>(...) -> typing.List[TenDlcBrandVettingAppeal]</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Returns the external vetting appeals for the 10DLC Brand identified by `brand_id`.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```python
from wavix import Wavix
from wavix.environment import WavixEnvironment

client = Wavix(
    token="<token>",
    environment=WavixEnvironment.DEFAULT,
)

client.ten_dlc.brand_vetting_appeals.list(
    brand_id="BMQFB7X",
)

```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**brand_id:** `str` — The unique ID of the 10DLC Brand.
    
</dd>
</dl>

<dl>
<dd>

**request_options:** `typing.Optional[RequestOptions]` — Request-specific configuration.
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.ten_dlc.brand_vetting_appeals.<a href="src/wavix/ten_dlc/brand_vetting_appeals/client.py">create</a>(...) -> SuccessResponse</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Submits an appeal for an external vetting of the 10DLC Brand identified by `brand_id`.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```python
from wavix import Wavix
from wavix.environment import WavixEnvironment

client = Wavix(
    token="<token>",
    environment=WavixEnvironment.DEFAULT,
)

client.ten_dlc.brand_vetting_appeals.create(
    brand_id="B6AI7PA",
    appeal_categories=[
        "VERIFY_TAX_ID"
    ],
    evidence=[
        "855dff49-c097-4645-3983-08dcb9856232"
    ],
)

```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**brand_id:** `str` — The unique ID of the 10DLC Brand.
    
</dd>
</dl>

<dl>
<dd>

**appeal_categories:** `typing.List[TenDlcBrandVettingAppealCreateRequestAppealCategoriesItem]` — List of appeal categories. Allowed values: `VERIFY_TAX_ID`, `VERIFY_NON_PROFIT`, `VERIFY_GOVERNMENT`, `LOW_SCORE`. `LOW_SCORE` is only valid for vetting appeals — brand identity appeals (`ten_dlc_brand_appeals_create`) do not accept it.
    
</dd>
</dl>

<dl>
<dd>

**evidence:** `typing.List[str]` — List of evidence IDs associated with the appeal.
    
</dd>
</dl>

<dl>
<dd>

**explanation:** `typing.Optional[str]` — Appeal comment or justification.
    
</dd>
</dl>

<dl>
<dd>

**evp_id:** `typing.Optional[str]` — EVP ID.
    
</dd>
</dl>

<dl>
<dd>

**vetting_id:** `typing.Optional[str]` — Vetting ID.
    
</dd>
</dl>

<dl>
<dd>

**request_options:** `typing.Optional[RequestOptions]` — Request-specific configuration.
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

## TenDlc Campaigns
<details><summary><code>client.ten_dlc.campaigns.<a href="src/wavix/ten_dlc/campaigns/client.py">list</a>(...) -> TenDlcCampaignListResponse</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Returns a paginated list of 10DLC Campaigns for the authenticated account, filtered by date, status, and use case.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```python
from wavix import Wavix
from wavix.environment import WavixEnvironment
import datetime

client = Wavix(
    token="<token>",
    environment=WavixEnvironment.DEFAULT,
)

client.ten_dlc.campaigns.list(
    name="Name",
    usecase="2FA",
    status="APPROVED",
    mock=True,
    created_before=datetime.date.fromisoformat("2024-08-22"),
    created_after=datetime.date.fromisoformat("2024-08-22"),
    page=1,
    per_page=25,
)

```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**name:** `typing.Optional[str]` — Filters Campaigns by name. Matches partial values.
    
</dd>
</dl>

<dl>
<dd>

**usecase:** `typing.Optional[str]` — Filters Campaigns by use case.
    
</dd>
</dl>

<dl>
<dd>

**status:** `typing.Optional[str]` — Filters Campaigns by status.
    
</dd>
</dl>

<dl>
<dd>

**mock:** `typing.Optional[bool]` — When `true`, returns only mock Campaigns used for testing. Default `false`.
    
</dd>
</dl>

<dl>
<dd>

**created_before:** `typing.Optional[datetime.date]` — Returns Campaigns created on or before this date, in `YYYY-MM-DD` format.
    
</dd>
</dl>

<dl>
<dd>

**created_after:** `typing.Optional[datetime.date]` — Returns Campaigns created on or after this date, in `YYYY-MM-DD` format.
    
</dd>
</dl>

<dl>
<dd>

**page:** `typing.Optional[int]` — Page number to retrieve. Default `1`.
    
</dd>
</dl>

<dl>
<dd>

**per_page:** `typing.Optional[int]` — Number of records to return per page. Default `25`.
    
</dd>
</dl>

<dl>
<dd>

**request_options:** `typing.Optional[RequestOptions]` — Request-specific configuration.
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.ten_dlc.campaigns.<a href="src/wavix/ten_dlc/campaigns/client.py">list_by_brand</a>(...) -> TenDlcCampaignListResponse</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Returns a paginated list of 10DLC Campaigns associated with the 10DLC Brand identified by `brand_id`.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```python
from wavix import Wavix
from wavix.environment import WavixEnvironment
import datetime

client = Wavix(
    token="<token>",
    environment=WavixEnvironment.DEFAULT,
)

client.ten_dlc.campaigns.list_by_brand(
    brand_id="BM20QP9",
    name="Name",
    usecase="2FA",
    status="APPROVED",
    mock=True,
    created_before=datetime.date.fromisoformat("2024-08-22"),
    created_after=datetime.date.fromisoformat("2024-08-22"),
    page=1,
    per_page=25,
)

```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**brand_id:** `str` — The unique ID of the 10DLC Brand.
    
</dd>
</dl>

<dl>
<dd>

**name:** `typing.Optional[str]` — Filters Campaigns by name. Matches partial values.
    
</dd>
</dl>

<dl>
<dd>

**usecase:** `typing.Optional[str]` — Filters Campaigns by use case.
    
</dd>
</dl>

<dl>
<dd>

**status:** `typing.Optional[str]` — Filters Campaigns by status.
    
</dd>
</dl>

<dl>
<dd>

**mock:** `typing.Optional[bool]` — When `true`, returns only mock Campaigns used for testing. Default `false`.
    
</dd>
</dl>

<dl>
<dd>

**created_before:** `typing.Optional[datetime.date]` — Returns Campaigns created on or before this date, in `YYYY-MM-DD` format.
    
</dd>
</dl>

<dl>
<dd>

**created_after:** `typing.Optional[datetime.date]` — Returns Campaigns created on or after this date, in `YYYY-MM-DD` format.
    
</dd>
</dl>

<dl>
<dd>

**page:** `typing.Optional[int]` — Page number to retrieve. Default `1`.
    
</dd>
</dl>

<dl>
<dd>

**per_page:** `typing.Optional[int]` — Number of records to return per page. Default `25`.
    
</dd>
</dl>

<dl>
<dd>

**request_options:** `typing.Optional[RequestOptions]` — Request-specific configuration.
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.ten_dlc.campaigns.<a href="src/wavix/ten_dlc/campaigns/client.py">create</a>(...) -> TenDlcCampaign</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Registers a 10DLC Campaign under the 10DLC Brand identified by `brand_id`. The Brand must have a verified identity status.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```python
from wavix import Wavix
from wavix.environment import WavixEnvironment

client = Wavix(
    token="<token>",
    environment=WavixEnvironment.DEFAULT,
)

client.ten_dlc.campaigns.create(
    brand_id="BM20QP9",
    affiliate_marketing=False,
    age_gated=False,
    auto_renewal=False,
    direct_lending=False,
    embedded_links=False,
    embedded_phones=False,
    embedded_link_sample="https://site.com/verify",
    description="Our campaign aims to …",
    optin_workflow="Our SMS ...",
    help=True,
    help_keywords="help",
    help_message="For help, please visit www.site.com. To opt-out, reply STOP.",
    optin=True,
    optin_keywords="begin,start",
    optin_message="You are now opted-in for help please reply HELP, to stop please reply STOP",
    optout=True,
    optout_keywords="stop,quit,unsubscribe",
    optout_message="You are now opted out and will receive no further messages",
    name="My first campaign",
    sample1="Your verification code is XXXXXX",
    sample2="XXXX is your verification code",
    sample3="Your code is XXXXXX, valid for 10 minutes",
    sample4="Use code XXXXXX to confirm your login",
    sample5="XXXXXX is your one-time passcode",
    mock=False,
    usecase="2FA",
    privacy_policy="https://site.com/privacy-policy",
    terms_conditions="https://site.com/terms-and-conditions",
)

```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**brand_id:** `str` — The unique ID of the 10DLC Brand.
    
</dd>
</dl>

<dl>
<dd>

**affiliate_marketing:** `bool` — Indicates whether the Campaign is used for affiliate marketing.
    
</dd>
</dl>

<dl>
<dd>

**age_gated:** `bool` — Indicates whether the Campaign messages contain age-gated content.
    
</dd>
</dl>

<dl>
<dd>

**auto_renewal:** `bool` — Indicates whether the Campaign is automatically renewed at the end of each billing period.
    
</dd>
</dl>

<dl>
<dd>

**direct_lending:** `bool` — Indicates whether the Campaign messages contain direct lending content.
    
</dd>
</dl>

<dl>
<dd>

**embedded_links:** `bool` — Indicates whether the Campaign messages contain embedded links.
    
</dd>
</dl>

<dl>
<dd>

**description:** `str` — Description of the Campaign and its messaging purpose.
    
</dd>
</dl>

<dl>
<dd>

**optin_workflow:** `str` — Description of the workflow through which subscribers opt in to the Campaign.
    
</dd>
</dl>

<dl>
<dd>

**help:** `bool` — Indicates whether the Campaign provides a help system that subscribers can trigger with a keyword such as HELP or INFO.
    
</dd>
</dl>

<dl>
<dd>

**help_keywords:** `str` — Comma-separated list of help keywords. Keywords are case-insensitive.
    
</dd>
</dl>

<dl>
<dd>

**help_message:** `str` — Acknowledgement sent when a subscriber texts a help keyword.
    
</dd>
</dl>

<dl>
<dd>

**optin:** `bool` — Indicates whether the Campaign requires subscribers to opt in before receiving messages.
    
</dd>
</dl>

<dl>
<dd>

**optin_keywords:** `str` — Comma-separated list of opt-in keywords. Keywords are case-insensitive.
    
</dd>
</dl>

<dl>
<dd>

**optin_message:** `str` — Acknowledgement sent when a subscriber texts an opt-in keyword.
    
</dd>
</dl>

<dl>
<dd>

**optout:** `bool` — Indicates whether the Campaign provides an opt-out system that subscribers can trigger with a keyword such as STOP or QUIT.
    
</dd>
</dl>

<dl>
<dd>

**optout_keywords:** `str` — Comma-separated list of opt-out keywords. Keywords are case-insensitive.
    
</dd>
</dl>

<dl>
<dd>

**optout_message:** `str` — Acknowledgement sent when a subscriber texts an opt-out keyword.
    
</dd>
</dl>

<dl>
<dd>

**name:** `str` — Display name of the Campaign.
    
</dd>
</dl>

<dl>
<dd>

**sample1:** `str` — Sample message demonstrating the content sent through the Campaign.
    
</dd>
</dl>

<dl>
<dd>

**mock:** `bool` — Indicates whether the Campaign is a mock campaign used for testing. Mock campaigns cannot send production traffic.
    
</dd>
</dl>

<dl>
<dd>

**usecase:** `str` — Registered use case for the Campaign, such as `2FA` or `MARKETING`.
    
</dd>
</dl>

<dl>
<dd>

**terms_conditions:** `str` — URL of the Campaign terms and conditions.
    
</dd>
</dl>

<dl>
<dd>

**embedded_phones:** `typing.Optional[bool]` — Indicates whether the Campaign messages contain embedded phone numbers.
    
</dd>
</dl>

<dl>
<dd>

**embedded_link_sample:** `typing.Optional[str]` — Sample of an embedded link used in Campaign messages.
    
</dd>
</dl>

<dl>
<dd>

**sample2:** `typing.Optional[str]` — Sample message demonstrating the content sent through the Campaign.
    
</dd>
</dl>

<dl>
<dd>

**sample3:** `typing.Optional[str]` — Sample message demonstrating the content sent through the Campaign.
    
</dd>
</dl>

<dl>
<dd>

**sample4:** `typing.Optional[str]` — Sample message demonstrating the content sent through the Campaign.
    
</dd>
</dl>

<dl>
<dd>

**sample5:** `typing.Optional[str]` — Sample message demonstrating the content sent through the Campaign.
    
</dd>
</dl>

<dl>
<dd>

**privacy_policy:** `typing.Optional[str]` — URL of the Campaign privacy policy.
    
</dd>
</dl>

<dl>
<dd>

**request_options:** `typing.Optional[RequestOptions]` — Request-specific configuration.
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.ten_dlc.campaigns.<a href="src/wavix/ten_dlc/campaigns/client.py">get</a>(...) -> TenDlcCampaign</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Returns the 10DLC Campaign identified by `campaign_id` under the Brand identified by `brand_id`.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```python
from wavix import Wavix
from wavix.environment import WavixEnvironment

client = Wavix(
    token="<token>",
    environment=WavixEnvironment.DEFAULT,
)

client.ten_dlc.campaigns.get(
    brand_id="BM20QP9",
    campaign_id="CKLCK95",
)

```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**brand_id:** `str` — The unique ID of the 10DLC Brand.
    
</dd>
</dl>

<dl>
<dd>

**campaign_id:** `str` — The unique ID of the 10DLC Campaign.
    
</dd>
</dl>

<dl>
<dd>

**request_options:** `typing.Optional[RequestOptions]` — Request-specific configuration.
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.ten_dlc.campaigns.<a href="src/wavix/ten_dlc/campaigns/client.py">update</a>(...) -> TenDlcCampaign</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Updates the 10DLC Campaign identified by `campaign_id`. Only the provided fields are changed.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```python
from wavix import Wavix
from wavix.environment import WavixEnvironment

client = Wavix(
    token="<token>",
    environment=WavixEnvironment.DEFAULT,
)

client.ten_dlc.campaigns.update(
    brand_id="BM20QP9",
    campaign_id="CKLCK95",
)

```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**brand_id:** `str` — The unique ID of the 10DLC Brand.
    
</dd>
</dl>

<dl>
<dd>

**campaign_id:** `str` — The unique ID of the 10DLC Campaign.
    
</dd>
</dl>

<dl>
<dd>

**name:** `typing.Optional[str]` — Display name of the Campaign.
    
</dd>
</dl>

<dl>
<dd>

**usecase:** `typing.Optional[TenDlcCampaignUpdateRequestUsecase]` — Registered use case for the Campaign. One of `CUSTOMER_CARE` (customer support messaging), `MARKETING` (promotional content), `ACCOUNT_NOTIFICATION` (account-related alerts), `FRAUD_ALERT` (fraud and suspicious-activity warnings), `PUBLIC_SERVICE_ANNOUNCEMENT` (public-interest notices), or `SECURITY_ALERT` (security-related warnings).
    
</dd>
</dl>

<dl>
<dd>

**description:** `typing.Optional[str]` — Description of the Campaign and its messaging purpose.
    
</dd>
</dl>

<dl>
<dd>

**embedded_links:** `typing.Optional[bool]` — Indicates whether the Campaign messages contain embedded links.
    
</dd>
</dl>

<dl>
<dd>

**embedded_phones:** `typing.Optional[bool]` — Indicates whether the Campaign messages contain embedded phone numbers.
    
</dd>
</dl>

<dl>
<dd>

**age_gated:** `typing.Optional[bool]` — Indicates whether the Campaign messages contain age-gated content.
    
</dd>
</dl>

<dl>
<dd>

**direct_lending:** `typing.Optional[bool]` — Indicates whether the Campaign messages contain direct lending content.
    
</dd>
</dl>

<dl>
<dd>

**optin:** `typing.Optional[bool]` — Indicates whether the Campaign requires subscribers to opt in before receiving messages.
    
</dd>
</dl>

<dl>
<dd>

**optout:** `typing.Optional[bool]` — Indicates whether the Campaign provides an opt-out system that subscribers can trigger with a keyword.
    
</dd>
</dl>

<dl>
<dd>

**help:** `typing.Optional[bool]` — Indicates whether the Campaign provides a help system that subscribers can trigger with a keyword.
    
</dd>
</dl>

<dl>
<dd>

**sample1:** `typing.Optional[str]` — Sample message demonstrating the content sent through the Campaign.
    
</dd>
</dl>

<dl>
<dd>

**sample2:** `typing.Optional[str]` — Sample message demonstrating the content sent through the Campaign.
    
</dd>
</dl>

<dl>
<dd>

**sample3:** `typing.Optional[str]` — Sample message demonstrating the content sent through the Campaign.
    
</dd>
</dl>

<dl>
<dd>

**sample4:** `typing.Optional[str]` — Sample message demonstrating the content sent through the Campaign.
    
</dd>
</dl>

<dl>
<dd>

**sample5:** `typing.Optional[str]` — Sample message demonstrating the content sent through the Campaign.
    
</dd>
</dl>

<dl>
<dd>

**optin_workflow:** `typing.Optional[str]` — Description of the workflow through which subscribers opt in to the Campaign.
    
</dd>
</dl>

<dl>
<dd>

**help_message:** `typing.Optional[str]` — Acknowledgement sent when a subscriber texts a help keyword.
    
</dd>
</dl>

<dl>
<dd>

**optin_message:** `typing.Optional[str]` — Acknowledgement sent when a subscriber texts an opt-in keyword.
    
</dd>
</dl>

<dl>
<dd>

**optout_message:** `typing.Optional[str]` — Acknowledgement sent when a subscriber texts an opt-out keyword.
    
</dd>
</dl>

<dl>
<dd>

**auto_renewal:** `typing.Optional[bool]` — Indicates whether the Campaign is automatically renewed at the end of each billing period.
    
</dd>
</dl>

<dl>
<dd>

**optin_keywords:** `typing.Optional[str]` — Comma-separated list of opt-in keywords. Keywords are case-insensitive.
    
</dd>
</dl>

<dl>
<dd>

**help_keywords:** `typing.Optional[str]` — Comma-separated list of help keywords. Keywords are case-insensitive.
    
</dd>
</dl>

<dl>
<dd>

**optout_keywords:** `typing.Optional[str]` — Comma-separated list of opt-out keywords. Keywords are case-insensitive.
    
</dd>
</dl>

<dl>
<dd>

**terms_conditions:** `typing.Optional[str]` — URL of the Campaign terms and conditions.
    
</dd>
</dl>

<dl>
<dd>

**privacy_policy:** `typing.Optional[str]` — URL of the Campaign privacy policy.
    
</dd>
</dl>

<dl>
<dd>

**embedded_link_sample:** `typing.Optional[str]` — Sample of an embedded link used in Campaign messages.
    
</dd>
</dl>

<dl>
<dd>

**request_options:** `typing.Optional[RequestOptions]` — Request-specific configuration.
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.ten_dlc.campaigns.<a href="src/wavix/ten_dlc/campaigns/client.py">delete</a>(...) -> SuccessResponse</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Deletes a 10DLC Campaign. Associated phone numbers cannot be used as Sender IDs once the Campaign is deleted.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```python
from wavix import Wavix
from wavix.environment import WavixEnvironment

client = Wavix(
    token="<token>",
    environment=WavixEnvironment.DEFAULT,
)

client.ten_dlc.campaigns.delete(
    brand_id="BM20QP9",
    campaign_id="CKLCK95",
)

```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**brand_id:** `str` — The unique ID of the 10DLC Brand.
    
</dd>
</dl>

<dl>
<dd>

**campaign_id:** `str` — The unique ID of the 10DLC Campaign.
    
</dd>
</dl>

<dl>
<dd>

**request_options:** `typing.Optional[RequestOptions]` — Request-specific configuration.
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.ten_dlc.campaigns.<a href="src/wavix/ten_dlc/campaigns/client.py">nudge</a>(...) -> SuccessResponse</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Requests action on a pending or rejected 10DLC Campaign. Use `nudge_intent` to specify the action: 
- `REVIEW`: Request review for a pending Campaign. - `APPEAL_REJECTION`: Appeal a rejected Campaign.
Note:
- The Campaign must be at least 72 hours old.
- Only one nudge request per Campaign is allowed every 24 hours.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```python
from wavix import Wavix
from wavix.environment import WavixEnvironment

client = Wavix(
    token="<token>",
    environment=WavixEnvironment.DEFAULT,
)

client.ten_dlc.campaigns.nudge(
    brand_id="B9FXYNH",
    campaign_id="CSJ4TV0",
    nudge_intent="REVIEW",
    description="Please review the campaign.",
)

```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**brand_id:** `str` — The unique ID of the 10DLC Brand.
    
</dd>
</dl>

<dl>
<dd>

**campaign_id:** `str` — The unique ID of the 10DLC Campaign.
    
</dd>
</dl>

<dl>
<dd>

**nudge_intent:** `str` 

Nudge intent. Allowed values: `REVIEW`, `APPEAL_REJECTION`. 
Use `nudge_intent` to specify the action: - `REVIEW`: Request review for a pending Campaign. - `APPEAL_REJECTION`: Appeal a rejected Campaign.
    
</dd>
</dl>

<dl>
<dd>

**description:** `str` — Description of the nudge request.
    
</dd>
</dl>

<dl>
<dd>

**request_options:** `typing.Optional[RequestOptions]` — Request-specific configuration.
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

## TenDlc Subscriptions
<details><summary><code>client.ten_dlc.subscriptions.<a href="src/wavix/ten_dlc/subscriptions/client.py">list</a>() -> typing.List[TenDlcEventSubscription]</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Returns the 10DLC event subscriptions for the authenticated account.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```python
from wavix import Wavix
from wavix.environment import WavixEnvironment

client = Wavix(
    token="<token>",
    environment=WavixEnvironment.DEFAULT,
)

client.ten_dlc.subscriptions.list()

```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**request_options:** `typing.Optional[RequestOptions]` — Request-specific configuration.
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.ten_dlc.subscriptions.<a href="src/wavix/ten_dlc/subscriptions/client.py">create</a>(...) -> TenDlcEventSubscription</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Registers a callback URL to receive Wavix 10DLC event notifications.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```python
from wavix import Wavix
from wavix.environment import WavixEnvironment

client = Wavix(
    token="<token>",
    environment=WavixEnvironment.DEFAULT,
)

client.ten_dlc.subscriptions.create(
    subscription_category="brand",
    url="https://webhook.url",
)

```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**request:** `TenDlcEventSubscription` 
    
</dd>
</dl>

<dl>
<dd>

**request_options:** `typing.Optional[RequestOptions]` — Request-specific configuration.
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.ten_dlc.subscriptions.<a href="src/wavix/ten_dlc/subscriptions/client.py">delete</a>(...) -> SuccessResponse</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Removes the 10DLC event subscription for the specified event category.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```python
from wavix import Wavix
from wavix.environment import WavixEnvironment

client = Wavix(
    token="<token>",
    environment=WavixEnvironment.DEFAULT,
)

client.ten_dlc.subscriptions.delete(
    subscription_category="number",
)

```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**subscription_category:** `str` — Event category to unsubscribe from.
    
</dd>
</dl>

<dl>
<dd>

**request_options:** `typing.Optional[RequestOptions]` — Request-specific configuration.
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

## TenDlc CampaignNumbers
<details><summary><code>client.ten_dlc.campaign_numbers.<a href="src/wavix/ten_dlc/campaign_numbers/client.py">link</a>(...) -> SuccessResponse</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Links a phone number to a 10DLC Campaign. Wavix automatically creates a Sender ID once the number is approved.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```python
from wavix import Wavix
from wavix.environment import WavixEnvironment

client = Wavix(
    token="<token>",
    environment=WavixEnvironment.DEFAULT,
)

client.ten_dlc.campaign_numbers.link(
    brand_id="B9FXYNH",
    campaign_id="CSJ4TV0",
    number="17029641104",
)

```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**brand_id:** `str` — The unique ID of the 10DLC Brand.
    
</dd>
</dl>

<dl>
<dd>

**campaign_id:** `str` — The unique ID of the 10DLC Campaign.
    
</dd>
</dl>

<dl>
<dd>

**number:** `str` — The phone number to link to the Campaign, in E.164 format.
    
</dd>
</dl>

<dl>
<dd>

**request_options:** `typing.Optional[RequestOptions]` — Request-specific configuration.
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.ten_dlc.campaign_numbers.<a href="src/wavix/ten_dlc/campaign_numbers/client.py">unlink</a>(...) -> SuccessResponse</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Unlinks a phone number from a 10DLC Campaign. The associated Sender ID is also deleted.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```python
from wavix import Wavix
from wavix.environment import WavixEnvironment

client = Wavix(
    token="<token>",
    environment=WavixEnvironment.DEFAULT,
)

client.ten_dlc.campaign_numbers.unlink(
    brand_id="B9FXYNH",
    campaign_id="CSJ4TV0",
    number="17029641104",
)

```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**brand_id:** `str` — The unique ID of the 10DLC Brand.
    
</dd>
</dl>

<dl>
<dd>

**campaign_id:** `str` — The unique ID of the 10DLC Campaign.
    
</dd>
</dl>

<dl>
<dd>

**number:** `str` — The phone number to unlink from the Campaign, in E.164 format.
    
</dd>
</dl>

<dl>
<dd>

**request_options:** `typing.Optional[RequestOptions]` — Request-specific configuration.
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.ten_dlc.campaign_numbers.<a href="src/wavix/ten_dlc/campaign_numbers/client.py">list</a>(...) -> TenDlcCampaignNumberListResponse</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Returns the phone numbers linked to the 10DLC Campaign identified by `campaign_id`.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```python
from wavix import Wavix
from wavix.environment import WavixEnvironment

client = Wavix(
    token="<token>",
    environment=WavixEnvironment.DEFAULT,
)

client.ten_dlc.campaign_numbers.list(
    brand_id="B9FXYNH",
    campaign_id="CSJ4TV0",
)

```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**brand_id:** `str` — The unique ID of the 10DLC Brand.
    
</dd>
</dl>

<dl>
<dd>

**campaign_id:** `str` — The unique ID of the 10DLC Campaign.
    
</dd>
</dl>

<dl>
<dd>

**request_options:** `typing.Optional[RequestOptions]` — Request-specific configuration.
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

## TwoFa Verification
<details><summary><code>client.two_fa.verification.<a href="src/wavix/two_fa/verification/client.py">create</a>(...) -> TwoFactorVerificationResponse</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Creates a 2FA verification and sends a real one-time password (OTP) to the destination phone number over the selected channel; this bills the account per OTP sent. Requires a 2FA service configured in the Wavix portal; the service is reused to generate and validate OTPs.

The verification proceeds through three steps:
1. Create a verification to generate and send an OTP.
2. Resend the OTP on the same verification if needed.
3. Validate the OTP through the check endpoint.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```python
from wavix import Wavix
from wavix.environment import WavixEnvironment

client = Wavix(
    token="<token>",
    environment=WavixEnvironment.DEFAULT,
)

client.two_fa.verification.create(
    service_id="7204a030201211ee9fb47d093f2f127c",
    to="447919433768",
    channel="sms",
)

```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**service_id:** `str` — Unique Wavix 2FA Service ID. Available on the Wavix portal.
    
</dd>
</dl>

<dl>
<dd>

**to:** `str` — End user's phone number to which the verification code will be sent. The phone number must be in E.164 format.
    
</dd>
</dl>

<dl>
<dd>

**channel:** `str` — Channel used to deliver the verification code. One of `sms` (sent as a text message) or `voice` (read aloud over a phone call).
    
</dd>
</dl>

<dl>
<dd>

**request_options:** `typing.Optional[RequestOptions]` — Request-specific configuration.
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.two_fa.verification.<a href="src/wavix/two_fa/verification/client.py">resend</a>(...) -> TwoFactorVerificationResendResponse</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Resends the OTP for the verification identified by `session_id` over the specified channel. Previously sent codes are invalidated.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```python
from wavix import Wavix
from wavix.environment import WavixEnvironment

client = Wavix(
    token="<token>",
    environment=WavixEnvironment.DEFAULT,
)

client.two_fa.verification.resend(
    session_id="2953d4308f2e11ecb75fcdafd6d2d687",
    channel="sms",
)

```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**session_id:** `str` — The unique ID of the 2FA verification session.
    
</dd>
</dl>

<dl>
<dd>

**channel:** `TwoFactorVerificationResendRequestChannel` — Channel used to resend the verification code. One of `sms` (sent as a text message) or `voice` (read aloud over a phone call).
    
</dd>
</dl>

<dl>
<dd>

**request_options:** `typing.Optional[RequestOptions]` — Request-specific configuration.
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.two_fa.verification.<a href="src/wavix/two_fa/verification/client.py">check</a>(...) -> TwoFactorVerificationCheckResponse</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Validates the OTP submitted by the end user against the verification identified by `session_id`. Non-idempotent — each call consumes one of a limited number of attempts tracked server-side; once exhausted, the verification returns `429` until a new verification is created.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```python
from wavix import Wavix
from wavix.environment import WavixEnvironment

client = Wavix(
    token="<token>",
    environment=WavixEnvironment.DEFAULT,
)

client.two_fa.verification.check(
    session_id="2953d4308f2e11ecb75fcdafd6d2d687",
    code="123456",
)

```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**session_id:** `str` — The unique ID of the 2FA verification session.
    
</dd>
</dl>

<dl>
<dd>

**code:** `str` — The code entered by an end user
    
</dd>
</dl>

<dl>
<dd>

**request_options:** `typing.Optional[RequestOptions]` — Request-specific configuration.
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.two_fa.verification.<a href="src/wavix/two_fa/verification/client.py">cancel</a>(...) -> SuccessResponse</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Cancels the 2FA verification identified by `session_id`. No further codes are sent, and previously sent codes can no longer be validated. A new verification is required to send another code.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```python
from wavix import Wavix
from wavix.environment import WavixEnvironment

client = Wavix(
    token="<token>",
    environment=WavixEnvironment.DEFAULT,
)

client.two_fa.verification.cancel(
    session_id="2953d4308f2e11ecb75fcdafd6d2d687",
)

```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**session_id:** `str` — The unique ID of the 2FA verification session.
    
</dd>
</dl>

<dl>
<dd>

**request_options:** `typing.Optional[RequestOptions]` — Request-specific configuration.
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

## TwoFa Sessions
<details><summary><code>client.two_fa.sessions.<a href="src/wavix/two_fa/sessions/client.py">list</a>(...) -> typing.List[ListSessionsResponseItem]</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Returns the 2FA verifications for the service identified by `service_id`, within the requested date range.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```python
from wavix import Wavix
from wavix.environment import WavixEnvironment
import datetime

client = Wavix(
    token="<token>",
    environment=WavixEnvironment.DEFAULT,
)

client.two_fa.sessions.list(
    service_id="7204a030201211ee9fb47d093f2f127c",
    from_=datetime.date.fromisoformat("2022-01-01"),
    to=datetime.date.fromisoformat("2022-01-31"),
)

```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**service_id:** `str` — The unique ID of the 2FA service.
    
</dd>
</dl>

<dl>
<dd>

**from:** `datetime.date` — Start of the date range to query, in `YYYY-MM-DD` format. Inclusive.
    
</dd>
</dl>

<dl>
<dd>

**to:** `datetime.date` — End of the date range to query, in `YYYY-MM-DD` format. Inclusive.
    
</dd>
</dl>

<dl>
<dd>

**request_options:** `typing.Optional[RequestOptions]` — Request-specific configuration.
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

## TwoFa Events
<details><summary><code>client.two_fa.events.<a href="src/wavix/two_fa/events/client.py">list</a>(...) -> typing.List[TwoFactorVerificationEvent]</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Returns the lifecycle events of the 2FA verification identified by `session_id`, such as number lookup and code delivery.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```python
from wavix import Wavix
from wavix.environment import WavixEnvironment

client = Wavix(
    token="<token>",
    environment=WavixEnvironment.DEFAULT,
)

client.two_fa.events.list(
    session_id="8753d4308f2e11ecb75fcdafd6d2d690",
)

```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**session_id:** `str` — The unique ID of the 2FA verification session.
    
</dd>
</dl>

<dl>
<dd>

**request_options:** `typing.Optional[RequestOptions]` — Request-specific configuration.
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

## Webrtc Tokens
<details><summary><code>client.webrtc.tokens.<a href="src/wavix/webrtc/tokens/client.py">list</a>(...) -> WebRtcTokensListResponse</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Returns a paginated list of Wavix Embeddable widget tokens for the authenticated account.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```python
from wavix import Wavix
from wavix.environment import WavixEnvironment

client = Wavix(
    token="<token>",
    environment=WavixEnvironment.DEFAULT,
)

client.webrtc.tokens.list()

```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**page:** `typing.Optional[int]` — Page number to retrieve. Default `1`.
    
</dd>
</dl>

<dl>
<dd>

**per_page:** `typing.Optional[int]` — Number of records to return per page. Default `25`.
    
</dd>
</dl>

<dl>
<dd>

**request_options:** `typing.Optional[RequestOptions]` — Request-specific configuration.
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.webrtc.tokens.<a href="src/wavix/webrtc/tokens/client.py">create</a>(...) -> WebRtcTokenResponse</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Creates a Wavix Embeddable widget token that authenticates a browser-based softphone session. The token expires after `ttl` seconds.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```python
from wavix import Wavix
from wavix.environment import WavixEnvironment

client = Wavix(
    token="<token>",
    environment=WavixEnvironment.DEFAULT,
)

client.webrtc.tokens.create(
    sip_trunk="my-sip-trunk",
    payload={
        "user_id": "42"
    },
    ttl=3600,
)

```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**sip_trunk:** `str` — Name of the SIP trunk the token authenticates against.
    
</dd>
</dl>

<dl>
<dd>

**payload:** `typing.Optional[typing.Dict[str, typing.Any]]` — Arbitrary client-defined data to associate with the token.
    
</dd>
</dl>

<dl>
<dd>

**ttl:** `typing.Optional[int]` — Time to live in seconds. Default `3600`. Pass `null` for no expiration.
    
</dd>
</dl>

<dl>
<dd>

**request_options:** `typing.Optional[RequestOptions]` — Request-specific configuration.
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.webrtc.tokens.<a href="src/wavix/webrtc/tokens/client.py">get</a>(...) -> WebRtcToken</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Returns the Wavix Embeddable widget token identified by `id`.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```python
from wavix import Wavix
from wavix.environment import WavixEnvironment

client = Wavix(
    token="<token>",
    environment=WavixEnvironment.DEFAULT,
)

client.webrtc.tokens.get(
    id="id",
)

```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**id:** `str` — The UUID of the widget token to retrieve.
    
</dd>
</dl>

<dl>
<dd>

**request_options:** `typing.Optional[RequestOptions]` — Request-specific configuration.
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.webrtc.tokens.<a href="src/wavix/webrtc/tokens/client.py">update</a>(...) -> WebRtcToken</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Updates the `payload` carried by the Wavix Embeddable widget token identified by `id`.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```python
from wavix import Wavix
from wavix.environment import WavixEnvironment

client = Wavix(
    token="<token>",
    environment=WavixEnvironment.DEFAULT,
)

client.webrtc.tokens.update(
    id="id",
    payload={
        "key": "value"
    },
)

```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**id:** `str` — The UUID of the widget token to update.
    
</dd>
</dl>

<dl>
<dd>

**payload:** `typing.Dict[str, typing.Any]` — Arbitrary client-defined data to associate with the token, replacing the existing payload.
    
</dd>
</dl>

<dl>
<dd>

**request_options:** `typing.Optional[RequestOptions]` — Request-specific configuration.
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.webrtc.tokens.<a href="src/wavix/webrtc/tokens/client.py">delete</a>(...) -> SuccessResponse</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Deletes the Wavix Embeddable widget token identified by `id`. The token can no longer authenticate widget sessions, and any active session using it ends.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```python
from wavix import Wavix
from wavix.environment import WavixEnvironment

client = Wavix(
    token="<token>",
    environment=WavixEnvironment.DEFAULT,
)

client.webrtc.tokens.delete(
    id="id",
)

```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**id:** `str` — The UUID of the widget token to delete.
    
</dd>
</dl>

<dl>
<dd>

**request_options:** `typing.Optional[RequestOptions]` — Request-specific configuration.
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

