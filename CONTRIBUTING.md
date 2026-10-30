# Contributing

Thanks for looking at Rasbur. Bug fixes, new decoders, tests and documentation are all welcome. [Open issues](https://github.com/omanshchoudhary/rasbur/issues) are the best place to start, and those labelled `good first issue` are scoped for a first pull request.

For anything large, such as a new package or a change to the public API, open an issue first so the approach can be agreed before you write the code.

## Setup

Use Node 20, which is what CI runs.

The packages need no configuration:

```bash
npm install
npm test --workspace=@rasbur/decoders
```

The web app and API need MongoDB and Redis, and the API will not start without them. The free tiers of MongoDB Atlas and Upstash are enough:

```bash
cp apps/api/.env.example apps/api/.env   # fill in the required values
npm run dev
```

Never commit `.env` files or real credentials.

## Project layout

- `packages/decoders`: the decoding engine, published to npm
- `packages/mcp`: the MCP server, published to npm
- `packages/shared`: types and Zod schemas shared by the apps
- `apps/api`: Express and Socket.IO backend
- `apps/web`: React and Vite frontend

## Before a pull request

CI runs these two commands on every pull request, so run them first:

```bash
npm run build
npm test
```

Tests need no environment file. The pre-commit hook formats staged files with Prettier.

Keep each pull request to one change, and link the issue it closes. Bug fixes and new behaviour need a test that fails without the change.

## Adding a decoder

Decoders live in `packages/decoders/src/decoders`. Each one extends `Decoder` and is registered in `registerDecoders.ts`. The [package readme](packages/decoders#writing-your-own-decoder) walks through the class.

The engine has three rules that matter more than coverage of a new format:

- **Return nothing rather than guess.** Plain English and random strings such as `AKIAIOSFODNN7EXAMPLE` must not produce a decode. Add a test for what your decoder should reject, not only what it should accept.
- **No runtime dependencies.** `@rasbur/decoders` ships with none.
- **No Node-only APIs.** The engine runs in browsers too, so `Buffer` is not available.

Tests go in `packages/decoders/src/decoders.test.ts`.

## Commits

Conventional Commits, one line, no body:

```
fix(decoders): reject whitespace in hash input
feat(mcp): add a tool for listing decoders
```

Scopes in use: `decoders`, `mcp`, `api`, `web`. Pull requests are squash merged, so the title should follow the same format.

## Security

Do not open a public issue for security problems. See [SECURITY.md](SECURITY.md).

## License

By contributing, you agree that your work is released under the [MIT License](LICENSE).
