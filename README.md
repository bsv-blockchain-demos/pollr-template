# Pollr Template

A development template for building a polling application on the BSV blockchain. It combines a React interface with TypeScript scaffolding for wallet actions, overlay topic management and MongoDB-backed lookup services.

The repository is an implementation exercise. Poll creation, voting, closing polls and retrieving results are currently TODO stubs that throw `Not implemented` errors.

## What is included

- A React and Vite interface with pages for creating polls, viewing active polls, viewing a user's polls and displaying completed polls.
- A poll form supporting two to ten text options.
- MetaNet Client detection and a wallet authentication integration.
- Guided TODOs for building poll and vote tokens with PushDrop, submitting wallet actions and querying overlays.
- A topic manager skeleton, lookup service skeleton and basic MongoDB storage helpers.
- A local LARS configuration in [deployment-info.json](deployment-info.json).

## Run the frontend

Use Node.js 22 or later and npm.

```sh
git clone https://github.com/bsv-blockchain-demos/pollr-template.git
cd pollr-template/frontend
npm ci
npm run dev
```

Open the local URL printed by Vite, normally `http://localhost:5173`. The interface checks for MetaNet Client and requests wallet authentication. Installing a wallet does not complete the missing poll functions; the relevant actions and data pages remain incomplete.

Run frontend commands from `frontend/`. The root `start` script is empty and does not launch the application.

## Implementation guide

| Area | Starting point | Work remaining |
| --- | --- | --- |
| Wallet actions and queries | [frontend/src/utils/PollActions.ts](frontend/src/utils/PollActions.ts) | Implement creation, voting, closing, lookup and identity functions. |
| Output admission | [TemplateTopicManager.ts](backend/src/topic-managers/TemplateTopicManager.ts) | Parse transactions and validate which outputs belong to the poll topic. The current manager admits no outputs. |
| Overlay indexing and queries | [TemplateLookupServiceFactory.ts](backend/src/lookup-services/TemplateLookupServiceFactory.ts) | Implement admission and spend handlers, then add poll-specific queries. |
| Stored records | [TemplateStorage.ts](backend/src/lookup-services/TemplateStorage.ts) and [types.ts](backend/src/types.ts) | Extend the generic record shape and storage operations for polls and votes. |
| Deployment configuration | [deployment-info.json](deployment-info.json) | Align topic names, lookup services and network settings with the implementation. |

The existing lookup service accepts only the generic `findAll` query for `ls_template`. The poll-specific queries described in the frontend TODOs still need backend implementations.

The root package includes LARS and CARS tooling. The checked-in deployment configuration selects mainnet and registers `tm_template` and `ls_template`. The backend contains overlay components, with no standalone server entry point or start script. A complete local overlay setup still needs to be established and verified as part of implementation.

## Build status

The frontend defines these commands:

```sh
npm run build
npm run lint
npm run preview
```

The production build currently fails during TypeScript checking. Unimplemented query functions infer `void` return types where the completed-polls, my-polls and poll-detail components expect arrays. Implement those functions and their return types before using the build and preview workflow. A successful Vite build writes to `frontend/build/`.

The root and backend `test` scripts are placeholders that exit with an error. No application test suite is included.

## Licence

The package manifests declare ISC, but no licence file is included in the repository.
