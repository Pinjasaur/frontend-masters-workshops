# Practical Prompt Engineering for Developers

- Notes: <https://sgoldfarb2.github.io/practical-prompt-engineering>
- Repo: <https://github.com/sgoldfarb2-fem/practical-prompt-engineering-code-exercise>

## LLMs

- Pattern predictors (one token at a time)
- Token by token, so no "planning ahead"
- Kinda like autocomplete
- _Non-deterministic_
- There's always a training cutoff date

## But how?

- Transformer arch (Google's 2017 paper ["Attention Is All You Need"](https://arxiv.org/pdf/1706.03762))
- Attn mechanism: model learns which tokens matter for prediction
- Scaling laws: 10x size became 100x more capable

## Determinism

- Temp controls randomness
  - 0 == deterministic, 2 == chaotic
  - Lower is better for factual tasks, code, data extraction
  - Higher better for creativity e.g. writing, brainstorming, varied solutions
- Top P
  - Alt to temp
  - Cumulative probability cutoff

## Tokens & context windows

- Tokens are roughly .75 words (but not always!)
- Cumulative tokens = input + output history
- Context window: max tokens the model can "remember"
- Once limits are hit, oldest context drops off silently

## System message

- "Invisible personality" behind every AI interaction
- Set by provider
- Takes up part of context window
- Reason same model acts differently in different tools

## Standard prompt

- _Your_ direct question or instruction to the AI
- Simplest form of prompting (just ask)
- Foundation everything else builds on
- Quality of question directly relates to quality of the answer

## Zero shot

- Direct task request _without_ any examples
- Model relies entirely on pre-training knowledge
- Works well for common tasks
- Quality varies based on task complexity & specificity

## One shot

- Provide exactly _one_ example with your request
- Model learns pattern, format, and style from example
- Useful for established format
- Show, don't tell

Research paper on AI generating prompts: <https://arxiv.org/abs/2211.01910>

## Few shot

- Provides 2+ examples to establish patterns & edge cases
- Model learns nuances and variations from diverse examples
- Include variety: different inputs, outputs, & edge cases
- More effective as models get larger

Research paper: <https://arxiv.org/abs/2005.14165>

OpenAPI tokenizer: <https://platform.openai.com/tokenizer>

TIL: type "Continue" or press Continue button if output suddenly stops.

## Context placement

- Where context is placed in prompts is _important_
- Beginning > End > Middle for info retention
- Models struggle with the middle of long contexts
- Critical info should go first, supporting detail last

Research paper: <https://arxiv.org/abs/2307.03172>
Primacy bias: <https://en.wikipedia.org/wiki/Serial-position_effect#Primacy_effect>
Recency bias: <https://en.wikipedia.org/wiki/Recency_bias>

## Structured output

- Get consistent formats every time
- Tell the model exactly how you want information
- Use examples, templates, or schemas to enforce format
- Test cases, documentation, data extraction, code generation

## Chain of thought (CoT)

- Ask the model to show it's reasoning step-by-step
- Breaks complex problems into intermediate steps
- CoT (zero shot): "Let's think step by step"
- Few shot: including reasoning steps in your examples

Research paper: <https://arxiv.org/abs/2205.11916>

Research paper on emotion: <https://arxiv.org/abs/2307.11760>

## Delimiters & XML tags

- Characters that create boundaries in prompts
- Triple quotes, dashes, XML tags, Markdown
- Supports nesting & attributes for complex data organization
- Be _semantic_ e.g. `<requirements>`, `<constraints>`, `<examples>`

## Personas

- "You are a {role}"
- Gives the model a perspective
- Sleeper agent like activates knowledge & vocabulary
- Works mainly for expertise, tone, & style
