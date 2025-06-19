# [![Purinton Dev](https://purinton.us/logos/brand.png)](https://discord.gg/QSBxQnX7PF)

## @purinton/ssh-client [![npm version](https://img.shields.io/npm/v/@purinton/ssh-client.svg)](https://www.npmjs.com/package/@purinton/ssh-client)[![license](https://img.shields.io/github/license/purinton/ssh-client.svg)](LICENSE)[![build status](https://github.com/purinton/ssh-client/actions/workflows/nodejs.yml/badge.svg)](https://github.com/purinton/ssh-client/actions)

> A simple, ESM-first SSH client for Node.js with private key authentication and sequential command execution.

---

## Table of Contents

- [Features](#features)
- [Installation](#installation)
- [Usage](#usage)
  - [ESM Example](#esm-example)
  - [CommonJS Example](#commonjs-example)
- [API](#api)
- [TypeScript](#typescript)
- [License](#license)

## Features

- Simple SSH command execution for Node.js
- Private key authentication only (no password support)
- Sequential execution of multiple commands in a single SSH session
- Returns merged stdout/stderr and exit code for each command
- TypeScript type definitions included
- Fully ESM compatible
- Easily testable/mocked via dependency injection

## Installation

```bash
npm install @purinton/ssh-client
```

## Usage

### ESM Example

```js
import { sshExec } from '@purinton/ssh-client';

const results = await sshExec({
  host: 'your.ssh.server',
  username: 'youruser', // optional if same as local user
  commands: [
    'echo Hello, SSH!',
    'uname -a',
  ],
});

for (const [i, { result, code }] of results.entries()) {
  console.log(`Command #${i + 1} exit code: ${code}`);
  console.log(result);
}
```

### CommonJS Example

```js
const {{ sshExec }} = require('@purinton/ssh-client');

(async () => {
  const results = await sshExec({
    host: 'your.ssh.server',
    username: 'youruser',
    commands: ['echo Hello, SSH!', 'uname -a'],
  });
  for (const [i, { result, code }] of results.entries()) {
    console.log(`Command #${i + 1} exit code: ${code}`);
    console.log(result);
  }
})();
```

## API

### sshExec(options)

Executes one or more commands on a remote SSH server using private key authentication.

#### Parameters

- `host` (string): Hostname or IP address (required)
- `port` (number): SSH port (default: 22)
- `username` (string): SSH username (default: current user)
- `commands` (string[]): List of commands to execute (required)

#### Returns

- `Promise<Array<{ result: string, code: number }>>`: Resolves to an array of results for each command, with merged stdout/stderr and exit code.

#### Throws

- If connection or authentication fails, or if no private key is found in `~/.ssh/`.

## TypeScript

Type definitions are included:

```ts
export interface SshExecOptions {
  host: string;
  port?: number;
  username?: string;
  commands: string[];
}

export interface SshExecResult {
  result: string;
  code: number;
}

export declare function sshExec(options: SshExecOptions): Promise<SshExecResult[]>;
```

## Support

For help, questions, or to chat with the author and community, visit:

[![Discord](https://purinton.us/logos/discord_96.png)](https://discord.gg/QSBxQnX7PF)[![Purinton Dev](https://purinton.us/logos/purinton_96.png)](https://discord.gg/QSBxQnX7PF)

**[Purinton Dev on Discord](https://discord.gg/QSBxQnX7PF)**

## License

[MIT © 2025 Russell Purinton](LICENSE)

## Links

- [GitHub](https://github.com/purinton/ssh-client)
- [npm](https://www.npmjs.com/package/@purinton/ssh-client)
- [Discord](https://discord.gg/QSBxQnX7PF)
