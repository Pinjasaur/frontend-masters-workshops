Workshop: <https://frontendmasters.com/workshops/design-systems-v2/>

Course site: <https://stevekinney.net/courses/storybook>

Repository: <https://github.com/stevekinney/anthology> (`live-coding` is the live workshop branch)

`appearance` vs `kind` vs `variant`. I kinda like `wich` 'cuz it's short for `sandwich`. :)

TIL easier way of extending native HTML attributes e.g.

```ts
export type ButtonProps = ComponentProps<'button'> & {
  variant: 'primary' | 'secondary' | 'destructive';
}
```

Fontsource is essentially fonts, on NPM: <https://fontsource.org/>

Also, `PropsWithChildren`:

```ts
type CalloutProps = PropsWithChildren<{ title: string }> & VariantProps<typeof variants>;
```

TIL `as const` e.g.

```ts
const variations = ['primary', 'secondary', 'tertiary'] as const
type Variations = typeof variations[number]
```

Mock Service Worker: <https://mswjs.io/>
