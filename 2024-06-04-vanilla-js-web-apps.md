# Practical Web App Patterns with Vanilla JS w/ Maximiliano Firtman

Site: https://firtman.github.io/webapp-patterns/  
Repo: https://github.com/firtman/webapp-patterns-projects  
Deck: https://firtman.github.io/webapp-patterns/slides.pdf

## Intro

_Design patterns_ are reusable templates for solving common software design problems.

This enhances code readability, efficiency, and creates a common vocabulary.

There's a "Design Patterns" book, circa 1994. "Gang of Four" Design Patterns.

JavaScript isn't strictly object oriented. It is prototype based, so can emulate most
OO features, but not all. Most notably protected methods & fields.

Components:
- Name
- Problem
- Solution
- Context
- Consequences
- Examples

Creation:
- Singletons (easy in JS, just create an object literal, no need for a class)
- Factory

Structural:
- Decorator (React HOC)
- Adapter
- Mixins (`Object.assign(Class.prototype, mixin)` or maybe the spread operator)
- Value Object

Behavioral:
- Observer (PubSub)
- Template Method
- Memento (e.g. implementing undo/redo)
- Command

## Single Page Apps

Lazy loading can be implemented with ES Dynamic Imports.

View Transitions API is bleeding edge af.

HTML Templates w/ Interpolation: trick using ES String templates (tagged?).

Routing metadata.

## Multi Page Apps

You can do View Transition API for MPA.

Prefetch / prerender / preconnect to improve perf.

## Data & State Management Patterns

`Promise`-ify data you think may become async in the future. Just `Promise.resolve` it!

Flux. Redux is based on Flux...

Lazy sync: sync to the server async and detach from the UI.

Proxy. Detect when some value changes.

Middleware. Insert logic in the _middle_, like a pipeline.

## Advanced Ideas & Patterns

Web app classics:
- PWA
- RWD
- Mobile first
- Offline first

_Progressively enhance_ by adding additional layers on top to improve&mdash;not take away from&mdash;the experience.

HTML streaming: render in chunks.

Virtual DOM: working directly w/ DOM is expensive, so work in memory, diff, and set when needed.
