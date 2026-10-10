# sf-tech-week-data

Open data for **SF Tech Week 2026** (Oct 5–11, San Francisco): every event on the official calendar and the hosts and speakers named on it. It is the same information the [techweek.wiki](https://techweek.wiki) guide showed on screen, nothing more.

**This is the final snapshot (v1.0).** The week is over and the data will not be updated. Cite or pin the [v1.0 release](../../releases/tag/v1.0) if you need a fixed version.

## Files

| file | rows | what |
|---|---|---|
| `events.jsonl` / `events.csv` | 1,593 | one event per row |
| `people.jsonl` / `people.csv` | 3,424 | one person per row |
| `event_people.csv` | 3,994 | who is named on which event (join table for the CSVs) |
| `metadata.json` | | when the snapshot was made and row counts |

The JSONL and CSV files hold the same data. In the CSVs, lists (tags) are joined with `; `, and an event's people are in `event_people.csv` instead of a nested list.

## `events`

| field | meaning |
|---|---|
| `id` | stable event id (the official calendar's id) |
| `title`, `headline` | name as listed; short takeaway |
| `summary` | the host's own opening paragraph; `null` when the listing had none or only the calendar's stock line |
| `date`, `start`, `end` | day and San Francisco time as ISO 8601 with offset (`null` when unknown) |
| `area`, `address` | neighborhood; street address only when the host published one |
| `host` | host name as listed |
| `registration` | `RSVP`, `Application` or `Unknown`; `needsApproval` is `true` for `Application` |
| `availability` | `SoldOut`, `LimitedAvailability` or `null` when captured |
| `rsvpCount` | RSVP count when captured, or `null` |
| `intents`, `topics`, `formats` | tags: what a visitor may want, subject areas, event formats |
| `people` (JSONL) / `peopleCount` (CSV) | hosts and speakers named on the event: `[{name, role, title, company, profile}]` |
| `url` | the host's public page (where to RSVP or apply, and the full description) |

## `people`

| field | meaning |
|---|---|
| `id` | stable id within this snapshot, used by `event_people.csv` |
| `name`, `title`, `company` | as published or matched; `title`/`company` may be `null` |
| `profile` | a public profile link: LinkedIn (2,587), Partiful host page (259), personal site (75), or `null` (503) |
| `events` (JSONL) / `eventCount` (CSV) | the events they are named on, with their role (`host` or `speaker`) |

People are merged by profile link, otherwise by name and company. Biographies and contact details are deliberately not included.

## How it was made

- **Events:** the official SF Tech Week calendar as of 2026-10-04, enriched with each event's public registration page (mostly Partiful). Titles and times follow the official calendar.
- **People:** hosts and speakers named on the event pages; **not attendees**. Profiles were matched by searching public sources, then reviewed; weak matches were left out rather than guessed.
- **Tags:** keyword and tag matches from the listings, not categories chosen by hosts.

## Known limitations

- Times, admission and availability changed during the week. Always confirm on the host page (`url`).
- `rsvpCount` is a single capture taken before the week, not a final attendance figure.
- Events delisted before 2026-10-04 and events added after it are not included.
- Profile matching can be wrong, especially for common names. Report mistakes (see below).
- Event descriptions are not included because they belong to their hosts; `url` links to them.

## Corrections and removal

Something wrong, or listed and want your entry removed? Open an issue with the event or person id and, for corrections, a link to the source. Removal requests are honored without questions.

## License

Data: [CC BY 4.0](https://creativecommons.org/licenses/by/4.0/). Please credit "sf-tech-week-data". Event names belong to their hosts. This project is independent and not affiliated with or endorsed by SF Tech Week or its organizers.
