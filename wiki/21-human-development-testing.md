# Human Development Testing (HDT)

HDT is an optional AAW checkpoint for changes that require real human/runtime evidence.

## Use HDT when

- UI behavior must be observed in a real runtime;
- an extension/browser/IDE workflow needs manual interaction;
- an integration depends on an environment that automated checks do not fully reproduce;
- user-visible behavior is central to the acceptance criteria.

Skip HDT when automated verification is enough, such as many docs-only, typo-only, formatting-only, or purely internal changes.

## Flow

```text
implement
  -> automated checks
  -> decide whether HDT is relevant
  -> ask once
  -> give beginner-friendly steps + expected result
  -> user reports observations
  -> agent evaluates evidence
  -> PASS -> commit checkpoint
  -> FAIL / unclear -> investigate and re-verify
```

HDT is a verification gate, not a second requirements interview.

## Report format

Tell the user:

1. what to open/run;
2. what action to perform;
3. what should happen;
4. what information to report on failure.

Treat the user's report as evidence, not as an unconditional PASS/FAIL command.
