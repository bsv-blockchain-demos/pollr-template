# Pollr Frontend

React interface for the Pollr development template. It provides poll forms and navigation while leaving the BSV wallet and overlay operations as implementation exercises.

See the [project README](../README.md) for the backend components and implementation plan.

## Run locally

Use Node.js 22 and npm. From the repository root:

```sh
cd frontend
npm ci
npm run dev -- --host 127.0.0.1
```

Open the URL printed by Vite, normally `http://localhost:5173`. The interface detects MetaNet Client and requests wallet authentication. No frontend environment variables are currently read by the application.

## Included screens

| Route | Purpose |
| --- | --- |
| `/` | Create a poll with two to ten text options. |
| `/Active-polls` | Display active polls. |
| `/MyPolls` | Display the current user's polls. |
| `/CompletedPolls` | Display completed polls. |
| `/poll/:pollId` | Display poll details and voting controls. |

These screens call functions in [PollActions.ts](src/utils/PollActions.ts) that currently throw `Not implemented` errors. Connecting a wallet does not make creation, voting, lookup or closing polls functional.

## Implementation starting points

- [PollActions.ts](src/utils/PollActions.ts): guided TODOs for token creation, wallet actions, overlay queries and results.
- [CreatePollForm.tsx](src/components/CreatePollForm.tsx): poll inputs and submission.
- [PollDetails.tsx](src/components/PollDetails.tsx): voting and detail view.
- [App.tsx](src/App.tsx): routes, navigation and wallet detection.

The [backend](../backend/src/) must implement the corresponding poll topic and lookup behaviour. The checked-in [deployment configuration](../deployment-info.json) still uses the generic `tm_template` and `ls_template` identifiers.

## Build status

```sh
npm run build
npm run lint
npm run preview -- --host 127.0.0.1
```

The build currently fails during TypeScript checking because unimplemented query functions infer `void` where components expect arrays. Complete those functions and their return types before using production builds.

A successful build writes `build/`, as specified in [vite.config.ts](vite.config.ts). Preview requires a successful build. No frontend test script is defined.
