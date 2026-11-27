# hrvst recipes

## Check the last time entry

```sh
hrvst time-entries list --per_page 1 --fields id,spent_date,hours,started_time,ended_time,notes,project.name,task.name --output json
```

Returns the most recent entry (newest spent_date first). Add `--user_id "$USER_ID"` to limit it to one user; get your ID from `hrvst users me --fields id`.

## Add a new task to a project

```sh
hrvst projects list --fields id,name                     # find $PROJECT_ID
hrvst tasks list --per_page 2000 --fields id,name        # check the task doesn't already exist
hrvst tasks create --name "$TASK_NAME" --billable_by_default false --fields id,name   # -> $TASK_ID
hrvst projects task-assignments create --project_id "$PROJECT_ID" --task_id "$TASK_ID" --billable false --fields id,project.name,task.name
```

Run each command as its own call. Tasks are account-wide, and a task must be assigned to a project before entries can use it. Personal projects are tracked as tasks under the "Dev Learning" project.

## Change the task of a time entry

```sh
hrvst time-entries update --time_entry_id "$ENTRY_ID" --task_id "$TASK_ID" --fields id,project.name,task.name
```

The task must already be assigned to the entry's project (add `--project_id` to move projects too).

## Log a duration

```sh
hrvst log "$HOURS" --project_id "$PROJECT_ID" --task_id "$TASK_ID" --notes "$NOTES"
```

Preferred way to record a finished amount of time.

An alias can replace `--project_id`/`--task_id`.

```sh
hrvst log "$HOURS" "$ALIAS" --notes "$NOTES"                            # e.g. hrvst log .35 skills --notes '...'
```

Aliases are stored locally by hrvst.

```sh
hrvst alias list                                                        # find an existing $ALIAS
```

## Create an alias

```sh
hrvst alias create "$ALIAS" --project_id "$PROJECT_ID" --task_id "$TASK_ID"   # once per project/task pair
```

## Start a timer from a past time, or log an entry with start and end times

```sh
hrvst time-entries create --project_id "$PROJECT_ID" --task_id "$TASK_ID" --spent_date "$DATE" --notes "$NOTES" --fields id,is_running   # -> $ENTRY_ID
hrvst time-entries update --time_entry_id "$ENTRY_ID" --started_time "$START" --fields id,started_time,hours,is_running
hrvst time-entries update --time_entry_id "$ENTRY_ID" --ended_time "$END"   # only to close it at a past time; omit to keep the timer running
```

The account tracks start/end times, so `create --hours` is ignored and the entry starts as a running timer at the current time. `create` has no start/end flags; set them with `update` (format like `1:17am`; Harvest echoes 24-hour times such as `1:17`). After `--ended_time`, the entry stops running and its hours come from start to end.

## Note on help output

In zsh, `hrvst $cmd --help` with a multi-word `$cmd` doesn't split and prints top-level help; use `${=cmd}` or type the words.
