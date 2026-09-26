# Chaster for Home Assistant

A Home Assistant custom integration for the [Chaster](https://chaster.app/) Public API.

It brings Chaster lock information, timing, permissions, messages, history, and supported lock controls into Home Assistant through a HACS-compatible integration.

> **Important:** Chaster remains the authority for authentication, permissions, lock rules, safety restrictions, and API access. This integration does not bypass Chaster restrictions.

## ✨ Features

- 🔐 Developer-token authentication through Home Assistant Config Flow
- 🔄 Automatic reauthentication when a token expires or is revoked
- 👤 Automatic role detection:
  - Auto
  - Wearer
  - Keyholder
  - Both
- 🔒 Current-lock entity that follows the active lock
- 📜 Historical wearer and keyholder lock sensors
- 🤝 Shared-lock support when permitted by the API/account
- 💬 Messaging data and message service
- 🕒 Current-lock history diagnostics
- 🎛️ Supported lock controls:
  - Refresh
  - Freeze
  - Unfreeze
  - Unlock
  - Emergency unlock
  - Archive
- ➕ `chaster.add_time`
- ➖ `chaster.remove_time`
- 🧩 Generic `chaster.api_request` service for documented API operations
- 🧩 Generic `chaster.lock_action` service for supported lock endpoints
- 📡 Home Assistant events for API responses, lock actions, and messages
- ⚙️ Configurable polling interval and optional features

## 📋 Requirements

- Home Assistant **2024.1.0 or newer**
- [HACS](https://hacs.xyz/) installed
- A Chaster account
- A Chaster developer/API token with the required scopes
- Network access from Home Assistant to the Chaster API

## 📦 Installation

### HACS

1. Open **HACS → Integrations**.
2. Search for **Chaster**.
3. Install the integration.
4. Restart Home Assistant.
5. Go to **Settings → Devices & services → Add Integration**.
6. Search for **Chaster**.
7. Enter your Chaster developer token.

If the repository is not listed in HACS, add this repository as a custom repository:

`https://github.com/jonny5509/Chaster`

### Manual installation

Copy the `custom_components/chaster` directory into:

```text
/config/custom_components/chaster
```

Restart Home Assistant, then add **Chaster** from **Settings → Devices & services**.

## 🔑 Authentication

This integration uses a **Chaster developer token**.

OAuth, browser login, client IDs, client secrets, and OAuth callbacks are not required.

### Getting a developer token

1. Open the [Chaster developer area](https://chaster.app/developers).
2. Request API access if required.
3. Open the **Developer interface**.
4. Create or open an application.
5. Select **Tokens**.
6. Generate a developer token.
7. Copy the token and enter it during Home Assistant setup.

**Keep your token private.** Never commit it to Git or post it in issues, screenshots, forums, or chat.

### Official Chaster API documentation

- [Getting started](https://docs.chaster.app/api/basics/getting-started/)
- [Developer tokens](https://docs.chaster.app/api/public-api/developer-token/)
- [Public API endpoints](https://docs.chaster.app/api/public-api/endpoints/)
- [API scopes](https://docs.chaster.app/api/reference/scopes/)

## ⚙️ Configuration

After installation:

**Settings → Devices & services → Chaster → Configure**

Available options include:

| Option | Description |
| --- | --- |
| **Polling interval** | How often Chaster data is refreshed |
| **Role mode** | Auto, Wearer, Keyholder, or Both |
| **Keyholder features** | Enables keyholder-related entities and data |
| **Shared locks** | Enables shared-lock support when available |
| **Messaging** | Enables messaging data/services |
| **Lock actions** | Enables supported lock-control actions |

The polling interval can be configured between **30 and 3600 seconds**.

## 🛠️ Services

### `chaster.add_time`

Adds time to a lock, subject to Chaster permissions.

```yaml
action: chaster.add_time
data:
  lock_id: LOCK_ID
  seconds: 3600
```

### `chaster.remove_time`

Removes time from a lock, subject to Chaster permissions.

```yaml
action: chaster.remove_time
data:
  lock_id: LOCK_ID
  seconds: 600
```

### `chaster.lock_action`

Calls a supported Chaster lock-action endpoint.

```yaml
action: chaster.lock_action
data:
  lock_id: LOCK_ID
  path: /locks/{lock_id}/...
  method: POST
  body: {}
```

The `{lock_id}` placeholder is replaced automatically.

### `chaster.api_request`

Provides a generic interface to documented Chaster Public API endpoints.

```yaml
action: chaster.api_request
data:
  method: GET
  path: /permissions/definitions
  params: {}
  body: {}
```

Use the official Chaster API documentation as the source of truth for endpoint paths, request bodies, responses, and scopes.

### `chaster.send_message`

Sends a message using a supported Chaster conversation endpoint.

```yaml
action: chaster.send_message
data:
  path: /conversations/CONVERSATION_ID
  body:
    # documented Chaster message payload
```

## 📡 Home Assistant events

### `chaster_api_response`

Fired after a successful generic API request.

Example event data:

```yaml
method: GET
path: /permissions/definitions
result: ...
```

### `chaster_action`

Fired after a lock action or time change.

```yaml
lock_id: LOCK_ID
action: add_time
seconds: 3600
result: ...
```

### `chaster_message`

Fired after sending a message.

```yaml
result: ...
```

## 🔒 Permissions and safety

Chaster is authoritative for all account and lock permissions.

The integration does **not** attempt to bypass:

- API scopes
- Lock permissions
- Minimum or maximum dates
- Timer restrictions
- History visibility
- Extension permissions
- Safety settings
- Freeze/unfreeze restrictions
- Unlock restrictions

If Chaster rejects an operation, the integration does not override that decision.

## 🔄 Existing installations

The integration stores the developer token as `token`.

If you are upgrading from an older OAuth-based version, remove the old Chaster integration and add it again using a developer token.

After updating through HACS, restart Home Assistant so the new integration version is loaded.

## 🧑‍💻 Development

The Home Assistant integration lives in:

```text
custom_components/chaster/
```

The project uses:

- Python
- Home Assistant Config Entries and Config Flow
- Home Assistant DataUpdateCoordinator
- HACS
- GitHub Actions

Validation includes Home Assistant **hassfest**, HACS validation, and Python bytecode compilation.

## 📁 Repository

Source code and issue tracking:

https://github.com/jonny5509/Chaster

## 📄 License

MIT License. See [LICENSE](LICENSE).
