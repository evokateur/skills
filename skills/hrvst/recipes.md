# hrvst recipes

Prerequisite: `hrvst` must work in the Claude Code sandbox, and `"sandbox": {"excludedCommands": ["hrvst *"]}` in `~/.claude/settings.json` is one way of doing it. Inside the sandbox it fails with "fetch failed", because Node's built-in `fetch` ignores the sandbox's `HTTPS_PROXY`. The exclusion only applies when the whole call is `hrvst …`, so don't pipe the output, chain commands, or `cd` first. Use `--fields` (dotted paths such as `task.name` work) and `--output json|table` to shape the output.

## Check the last time entry

```sh
hrvst time-entries list --per_page 1 --fields id,spent_date,hours,started_time,ended_time,notes,project.name,task.name --output json
```

Returns the most recent entry (newest spent_date first). Add `--user_id "$USER_ID"` to limit it to one user; get your ID from `hrvst users me --fields id`. Verified.

## Add a new task to a project

```sh
hrvst projects list --fields id,name                     # find $PROJECT_ID
hrvst tasks list --per_page 2000 --fields id,name        # check the task doesn't already exist
hrvst tasks create --name "$TASK_NAME" --billable_by_default false --fields id,name   # -> $TASK_ID
hrvst projects task-assignments create --project_id "$PROJECT_ID" --task_id "$TASK_ID" --billable false --fields id,project.name,task.name
```

Run each command as its own call. Tasks are account-wide, and a task must be assigned to a project before entries can use it. Personal projects are tracked as tasks under the "Dev Learning" project. Verified.

## Change the task of a time entry

```sh
hrvst time-entries update --time_entry_id "$ENTRY_ID" --task_id "$TASK_ID" --fields id,project.name,task.name
```

The task must already be assigned to the entry's project (add `--project_id` to move projects too). Verified.

## Log a duration

```sh
hrvst alias list                                                        # find an existing $ALIAS
hrvst alias create "$ALIAS" --project_id "$PROJECT_ID" --task_id "$TASK_ID"   # once per project/task pair
hrvst log "$HOURS" "$ALIAS" --notes "$NOTES"                            # e.g. hrvst log .35 skills --notes '...'
```

Preferred way to record a finished amount of time. `--project_id`/`--task_id` can replace the alias. Aliases are stored locally by hrvst. Provided by the user; syntax checked against `--help`, not yet run.

## Start a timer from a past time

```sh
hrvst time-entries create --project_id "$PROJECT_ID" --task_id "$TASK_ID" --spent_date "$DATE" --notes "$NOTES" --fields id,is_running   # -> $ENTRY_ID
hrvst time-entries update --time_entry_id "$ENTRY_ID" --started_time "$START" --fields id,started_time,hours,is_running
hrvst time-entries update --time_entry_id "$ENTRY_ID" --ended_time "$END"   # only to close it at a past time; omit to keep the timer running
```

The account tracks start/end times, so `create --hours` is ignored and the entry starts as a running timer at the current time. `create` has no start/end flags; set them with `update` (format like `1:17am`). Verified through setting `--started_time`; closing with `--ended_time` is syntax-checked only.

## Note on help output

In zsh, `hrvst $cmd --help` with a multi-word `$cmd` doesn't split and prints top-level help; use `${=cmd}` or type the words.
