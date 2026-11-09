# Contributing

1. `git clone https://github.com/MARYCOMPLEX/ttc-ui-kit && cd ttc-ui-kit`
2. `npm run verify` — prints the compatibility matrix for the repo you are in. Run it from the
   consumer project's root when you are checking an integration, not from this repo.
3. Keep `dist/` and `dist/index.d.ts` in sync with any component change; there is no build step.
4. Cut a tag (`v1.1.1`, `v1.1.2`, …) for every change consumers should pick up. `main` is the
   integration branch only.

## Reporting a rendering difference

Run `npm run verify` in the consumer project and paste the matrix plus the `TTC-DIAG` line (if
printed) into the issue. Without it a report cannot be reproduced.
