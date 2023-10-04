# Events

The purpose of this repository is to record attended events and associates notes and assets.

## Data model

The data is structured in three types of entities which have the following relations among each other:

```
┌─────────┐               ┌─────────┐               ┌─────────┐
│         │ 1        1..* │         │ 1           * │         │
│ event   ├───────────────┤ session ├───────────────┤ asset   │
│         │               │         │               │         │
└─────────┘               └─────────┘               └─────────┘
```

- An **event** is an event such as a meetup, a conference, a hackathon, a workshop, a panel discussion, etc. Every event may have one or more sessions (it may seem redundant for events that naturally only have a single type of activity, such as a hackathon, to have a session, however, requiring every event to consist of a session makes the data model simpler).
- A **session** is an activity during this event such as a presentation at a meetup or conference, the actual hackathon or workshop content at a hackathon or workshop, or the actual discussion at a panel discussion. Every session must be associated with exactly one event. A session may have any number of assets.
- An **asset** is file associated with a session, such as a slide deck of a presentation, instructions and example code for a hackathon, etc. An asset must be associated with exactly one session.

## Data representation

Each entity is represented as either a YAML or Markdown file:

- **Event:** Markdown file with metadata in the YAML frontmatter and notes about the event as the main content
- **Session:** Markdown file with metadata in the YAML frontmatter and notes about the session as the main content
- **Asset:** YAML file with metadata about the asset (no notes about assets)

### Metadata formats

The metadata formats for the three types of entities are shown below. Metadata is always represented as YAML, either in the YAML frontmatter of a Markdown file or as a standalone YAML file.

#### Event

```yaml
meta:
  created: 
  edited:
data:
  name:
  date:
    from:
    to:
  location:
  remote:
  url:
  sessions:
```

Notes:

- `date` may be either a string or a dictionary with a `from` and `to` field. In the first case, the string should contain the date that the event took place, if it was a single-day event. In the latter case, the `from` and `to` fields should contain the start and end date of the event, if it was a multi-day event. All date strings must have the format `YYYY-mm-dd`.
- `location` is a free-form string describing the location of the event. If it's a online-only event, location can be set to "Online".
- `remote` is an optional boolean. It should be set to `true` if the entire event has been attended remotely rather than on-site, and `false` or unset otherwise.
- `url` is optional and may contain a URL pointing to some form of home page of the event 
- `sessions` is a list of session IDs with at least one element. This information is redundant because every session also points exactly one event. However, including event-to-sessions links in the events may make navigating the data files easiser. For presentation purposes, the pointers in the sessions can be used to collect all sessions of an event since there each session must have exactly one event links, which can be enforced with a schema.

#### Session

```yaml
meta:
  created: 
  edited:
data:
  name:
  event:
  date:
  speakers:
    - name:
      affiliation:
  recording:
  remote:
```

Notes:

- `event` is required and is the ID of the event that the session belongs to.
- `date` is required and must contain the date of the session (format `YYYY-mmm-dd`).
- `speakers` is optional, however, it should be included for sessions that have one or more speakers, such as presentations or panel discussions. It can be omitted for sessions that have no speakers, such as hackathons.
- `recording` is optional and may contain an URL pointing to a recording of the session (e.g. on YouTube)
  - If a recording is downloaded and self-hosted, then it should be represented as an asset
- `remote` is an optional boolean. It should be set to `true` if the session has been attended remotely rather than on-site, and `false` or unset otherwise.

#### Asset

```yaml
meta:
  created: 
  edited:
data:
  name:
  type:
  url:
  session:
```

Notes:

- `type` is required and is the file type of the assets. Possible values may be `pdf`, `zip`, `avi`, etc.
- `url` is required and is the URL of the asset in the backend storage (e.g. in an Amazon S3 bucket)
- `session` is required and is the ID of the session that the asset belongs to

## TODO

- Eliminate metadata (`created` and `edited`)? These dates are not really useful as the information is about a specific event with a date and is not intended to evolve over time.
