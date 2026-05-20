# TypeScript in the Age of AI

- Repo: <https://github.com/arackaf/fm-typescript-workshop>
- Slides: <https://drive.google.com/drive/folders/1B24-OuO89ohEjIz9rkqXTHdCVnx7Sk5M?usp=sharing>

TS is _structurally_ typed — it's not typical and is due to being types bolted
on to JS.

## Types

**Nominal**: types define the values a variable can hold based on the value's _type_

**Structural**: types define the _structure_ of what values a variable can hold

Types are _sets_ of valid (matching) values.

Type hierarchy:

![Source: https://www.oreilly.com/library/view/programming-typescript/9781492037644/ch03.html](https://www.oreilly.com/api/v2/epubs/urn:orm:book:9781492037644/files/assets/prts_0301.png)

## Unions

Union of types => intersection of properties.

Intersection of types => union of properties.

## Conditional Types

Union to a conditional type, does every part of the union, and returns the union
of those results.

## Variance

**Covariance**: providing something more specific than what you asked for

Ex: asked for shape, I gave you circle

**Contravariance**: providing something less specific than what you asked for

Ex: asked for circle, I gave you shape

**Bivariance**: both

## Misc

TIL `ReturnType<typeof thirdPartyFn>`. Wrap with `Awaited<>` to strip Promise.

TIL `Parameters<typeof thirdPartyFn>[0]` for external non-exported-typed code.

File away for the future: re-spread to array -> tuple e.g. `[...Args]`.

Tip: twoslash query comments extension: <https://marketplace.visualstudio.com/items?itemName=Orta.vscode-twoslash-queries>
