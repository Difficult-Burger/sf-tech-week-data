# sf-tech-week-data

Open data for **SF Tech Week 2026** (Oct 5–11, San Francisco): every event and the people named on it, as plain JSON Lines. It is the same information the [Lychee](https://techweek.wiki) guide shows on screen, nothing more.

- `events.jsonl`: one event per line
- `people.jsonl`: one person per line, with the events they are named on
- `metadata.json`: when this snapshot was made and how many rows it has

Times are San Francisco time (ISO 8601 with offset). The data is a dated snapshot of public listings: times, admission and availability change, so always confirm on the host page (`url`).

## `events.jsonl`

| field | meaning |
|---|---|
| `id` | stable event id |
| `title`, `headline`, `summary` | name, one-line takeaway, short description (English) |
| `date`, `start`, `end` | day and Pacific-time ISO timestamps (`null` when unknown) |
| `area`, `address` | neighborhood; street address only when the host publishes one |
| `host` | host name as listed |
| `registration` | `RSVP`, `Application` or `Unknown`; `needsApproval` is `true` for `Application` |
| `availability` | `SoldOut`, `LimitedAvailability` or `null` at snapshot time |
| `rsvpCount` | RSVP count at snapshot time, or `null` |
| `intents`, `topics`, `formats` | tags: what a visitor may want, subject areas, event formats |
| `people` | `[{name, role, title, company, profile}]` hosts and speakers named on the event |
| `url` | the host's public page: where to RSVP or apply |

## `people.jsonl`

`name`, `title`, `company`, `profile` (a public profile link, mostly LinkedIn) and `events`: `[{id, role}]`. People are merged by profile link, otherwise by name and company. Biographies are deliberately not included.

## Corrections

Something wrong? Open an issue with the event id, what is wrong and a link to the source. A person reviews every report.

## License

Data: [CC BY 4.0](https://creativecommons.org/licenses/by/4.0/). Please credit "sf-tech-week-data". Event descriptions and names belong to their hosts; this project is independent and not affiliated with or endorsed by SF Tech Week or its organizers.

The snapshot is generated from the Lychee site's own data by an allow-list, so a field that is not on screen there is not here.
