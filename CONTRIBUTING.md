# Contributing

Contributions are welcome through pull requests, however, the reference architecture
is intended to reflect the opinion of Red Hat and IBM based on the key tenets
outlined in the README.md. Therefore only PR's which are aligned with that
opinion will be accepted.

## Checking formatting and style

Before pushing changes contributors need to ensure that their markdown spec is valid
by executing

```
npm install
npm run lint
```

## Adding new documents that appear on website

Reference architecture uses docusaurus website that requires each file to supply additional metadata
At minimum file needs to have following header (where position is the next position that we have in current category)
```
---
sidebar_position: 1
---
```

For more info please see: https://docusaurus.io/docs/create-doc

## Building and publishing website

Website can be published by following commands

```
cd website
yarn
yarn build 
GIT_USER=<youruser> USE_SSH=true yarn deploy 
```
