# beacon-2026

Emission anchor for the year.

This is an **anchor** repository: it holds timestamped cryptographic proofs, and its entire value
depends on **nothing that enters it ever being modified afterwards**.

> 🇪🇸 En espanol: [`README.es.md`](README.es.md)

## What is inside

Each turn leaves two signed files:

```
emissions/YYYY/MM/DD/HHMM-commitment.jws   the commitment, published BEFORE the input exists
emissions/YYYY/MM/DD/HHMM-emission.jws     the result, published after
```

When a turn cannot be completed, a `-failure.jws` takes the place of the `-emission`. It states why,
and reveals the seed so anyone can compute what the result would have been.

## How to check this is append-only

You do not have to take our word for it. Ask:

```bash
# The branch is protected — no credentials needed
curl -s https://api.github.com/repos/utc24h-test/beacon-2026/branches/main

# Nothing was modified after publication: additions only
git log --diff-filter=M --oneline -- emissions/
```

The second command **must return nothing**. If it returns anything, a file was touched after it was
signed.

## Cloning on Windows

The `.gitattributes` at the root already handles this. Do not change `core.autocrlf` and do not
convert the files: `.jws` files are verified **byte for byte**, and a single converted line ending
breaks the signature.

---

Created by `provision/`, not by hand.
