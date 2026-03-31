# TanStack Start Fundamentals

- Repo: <https://github.com/arackaf/fm-tanstack-workshop>

## What is TanStack Start ... and Router?

Router came first, client only. Strongly typed.

Start takes Router and adds server support.

## Why SSR?

SPA trade off is initial load is slow (render fast, just not useful content).

## Using TanStack Start

RSC are not yet supported in TanStack Start.

The one use case for RSC that is "actually cool" is if you have a "rich" component tree it can be rendered entirely on the server.

Quick start:

```sh
npm create @tanstack/start@latest
```

Always recommend choosing `Query`.

## An aside on Drizzle

Adam likes Drizzle.

Create a `drizzle.config.ts` and a `npx drizzle-kit pull` and it will do the gen.

## Routing

Flat file use periods to delimit as slashes.

Directory is as expected.

Layouts are called `route.tsx`.

## Streaming

"One of the coolest features" -- Adam

The gist is start the data loading on the server, render the loading state, and stream data as it comes in.

Remove the `await`, so they are the Promises literal, that are being returned. These are not serializable over the wire.

## Suspense

TIL `use()` hook. New in React 19? It's a pseudo-hook.

## Middleware

Client -> Server order matters.

TIL `@ts-expect-error` for when expecting an error.

## Observability

Charity Majors' book is rec: <https://www.oreilly.com/library/view/observability-engineering/9781492076438/>

The idea is a single trace ID attached to many discrete logs.

## Misc

Should be called mapFlat, not flatMap, because it maps and _then_ flattens. Idk either.
