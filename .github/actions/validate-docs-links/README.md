# GitHub Action for Validating Documentation Links

> Forked from [vercel/next.js](https://github.com/vercel/next.js/blob/canary/.github/actions/validate-docs-links/README.MD)

This action ensures that internal links in `.mdx` files in the `/docs/` directory are valid. It runs on every pull request that includes changes to these files.

The action is triggered by the workflow defined in `.github/workflows/validate-docs-links.yml`.

## Usage

This action is written in TypeScript and compiled locally before being pushed to GitHub.

To make changes:

- Edit the `src/index.ts` file.
- Navigate to the script folder `cd .github/actions/validate-docs-links`
- Run `pnpm install` to install dependencies.
- Run `pnpm run build` to compile code. This will create an updated `lib/index.js`.
- Commit and push changes to GitHub.
