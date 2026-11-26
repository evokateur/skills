---
name: hrvst
description: Use the hrvst CLI for Harvest operations or questions about how to perform them. Reuse and maintain command recipes as requests come in.
---

# Harvest CLI

1. Look for the requested outcome in `recipes.md` beside this file. Create it when saving the first recipe.
2. If the recipe is missing or stale, start with `hrvst --help` and follow the subcommand help down to the operation. Check the arguments and flags against the installed CLI.
3. Match the request. For a how-to question, show the command. For an action, run it with the requested inputs and check the result. If a write has an uncertain outcome, inspect the resulting Harvest state before retrying.
4. Save each newly requested operation under a heading phrased as the user's goal in `recipes.md`. Include the verified command in a shell block, describe its variable inputs, and mention any prerequisite that affected the result. Replace account-specific values with named shell variables and omit credentials and private output. If only the syntax was checked, say so. Update an existing recipe in place when the workflow changes.
