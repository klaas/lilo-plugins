# LILO Plugins

Connect your assistant to [LILO](https://lilo.app) to manage your saved places and collections.
This repository distributes a plugin for supported Codex/ChatGPT desktop clients through a custom marketplace. It is not a listing in OpenAI's public plugin directory.

## Install

With a current Codex CLI installed, run:

```sh
codex plugin marketplace add klaas/lilo-plugins --ref main
```

Restart the desktop app, open the Plugins Directory, select **LILO Plugins**, and install **LILO**. On CLI versions supporting plugin installation, you can also run:

```sh
codex plugin add lilo@lilo-plugins
```

Complete the client's OAuth connection flow and sign in with your own LILO account. If you are new to LILO, sign in at https://lilo.app first. Review the requested permissions. Never paste tokens into chat.

Start a new chat, select LILO, and try:

> Use LILO to list my saved locations. Do not change anything.

Verify that a LILO tool was actually called and returned your data.

## What you can do

- Find and manage saved locations and organize collections.
- Read and edit supported profile fields.
- Export owned locations as a Lilopack; exports exclude photos and collections.
- Upload photos to existing locations using a returned HTTP PUT URL, or import a direct public HTTPS image URL, where supported by the client.

Geocoding, nearby search, creating locations from photos, and importing Lilopacks are not supported by this plugin. Available actions depend on the permissions you grant and LILO's access rules.

## Connection and compatibility

The package connects to `https://lilo.app/mcp` using Streamable HTTP. LILO requires OAuth authorization-code flow with S256 PKCE, resource indicators, and Client ID Metadata Documents (CIMD). Dynamic client registration is disabled.

If connection fails, check that your client supports these features. An installed package alone does not establish a working authenticated connection. Direct MCP connections and marketplace installations are distinct integration paths; test the sign-in and first tool call in your client.

Your location data stays behind LILO authentication; it is not stored in this GitHub repository. Removing the plugin does not by itself prove server-side authorization has been revoked. Signed export URLs are private bearer links and expire after 15 minutes.

## Update

```sh
codex plugin marketplace upgrade lilo-plugins
```

Restart your client and check its plugin update/install controls. Existing OAuth grants do not automatically gain new permissions.

## Maintainers

The catalog is `.agents/plugins/marketplace.json`; its source path is relative to the repository root. The package lives in `plugins/lilo/`. It contains public metadata, the remote server URL, and the logo. No application backend source or credentials are needed.

For local testing:

```sh
codex plugin marketplace add .
```

Before releasing a package change, update its version, validate the JSON and referenced paths, test installation and OAuth with a normal user account, then commit and push. Backend changes are deployed separately.

## Links

- [LILO](https://lilo.app)
- [Privacy](https://lilo.app/privacy)
- [Support and publisher information](https://lilo.app/about)
- [OpenAI marketplace documentation](https://developers.openai.com/plugins/build/plugins)
