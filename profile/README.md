# Kingdom Community

This organization publishes open-source libraries for running an online
community: the website chrome, the accounts, the security controls, the
documentation pipeline, the server status panel.

They were not written as a library project. They were extracted from the stack
behind a working community, generalised, and released under the MIT license.
Wherever a library used to name a particular site, a particular identity
service, or a particular game server, that became configuration. None of them
depends on anything belonging to the community they came from, and anyone can
use them for their own.

The organization also hosts that community's own private repositories, which is
why the name is what it is. The libraries below are the part that generalised.

## The libraries

- **[minecraft-server-ping](https://github.com/kingdom-community/minecraft-server-ping)**
  — TypeScript, npm, Node 18+. A zero-dependency implementation of the Minecraft
  Server List Ping protocol: open a TCP socket to a host and read back its MOTD,
  player counts, version, favicon and round-trip latency. A server being down
  arrives as a return value, not an exception.

- **[community-site-kit](https://github.com/kingdom-community/community-site-kit)**
  — TypeScript, npm. Shared Next.js + MUI building blocks for a community
  website: an SSR-safe colour-mode provider and toggle, prop-driven top and
  bottom navigation bars, a `next/link` bridge for MUI's `component` prop,
  per-page SEO metadata, a "temporarily unavailable" panel, and pure builders for
  `sitemap.xml` and `robots.txt`. It knows nothing about what your community is
  about; you pass in the brand, the nav items and the links.

- **[web-guards](https://github.com/kingdom-community/web-guards)** — TypeScript,
  npm, no runtime dependencies. Fail-closed security primitives for a small
  community website: a fixed-window rate limiter with an injectable clock, the
  `Origin`/`Referer` check for state-changing routes, `__Host-` prefixed session
  cookie rules, a signed OAuth `state` bound to the session that started the
  flow, and the client address read correctly from behind a reverse proxy. It
  imports no framework.

- **[github-docs](https://github.com/kingdom-community/github-docs)** —
  **TypeScript and Python**, two packages in one repository. Run your community's
  documentation out of a git repository: the TypeScript reader (npm) fetches
  markdown for your site to render and turns an upstream failure into a value
  rather than a 5xx, and the Python writer (PyPI, standard library only) lands an
  edit on a per-file branch and opens or reuses a pull request, so a change to
  the rules gets reviewed before it is the rules. The two halves are independent;
  they talk to the same repository, not to each other.

- **[discord-account-link](https://github.com/kingdom-community/discord-account-link)**
  — TypeScript, npm, server-side only. Attach a Discord identity to an account
  somebody already has on your own site, via the Discord OAuth2
  authorization-code flow. Deliberately not "Sign in with Discord": the `identify`
  scope only, no session is ever minted from a Discord identity, and the access
  token buys one `/users/@me` call and is then discarded rather than stored.

- **[session-client](https://github.com/kingdom-community/session-client)** —
  **TypeScript and Python**, two packages in one repository. Clients for an HTTP
  identity service that issues bearer tokens — register, login, validate,
  refresh, logout — written against the shape of such a service rather than one
  vendor's implementation, with every endpoint path and response field name
  configurable. The point of the library is that it keeps success, refusal ("no,
  and here is why") and unavailable ("nobody did anything wrong and nothing is
  known") as three outcomes you cannot mistake for each other.

## Status

All six are at version `0.1.0`, and **none of them is published to npm or PyPI
yet**. The individual READMEs show `npm install` and `pip install` lines with the
intended package names; those commands do not work today. To use one now, clone
the repository and build it from source.

Each repository has tests and CI, and each README documents what the library
does not do as well as what it does.

## License

MIT, all six. Copyright (c) 2026 Daniel McCoy Stephenson.
