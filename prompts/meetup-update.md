I need you to collect data from the Meetup groups I belong to. Don't join, leave, RSVP to, message, or change anything on Meetup. Only read pages.

## Step 1: Find my groups
1. Go to meetup.com. I'm already logged in. Open my profile menu and go to "Your groups" (the page that lists the groups I'm a member of). Scroll or page until every group has loaded.
2. Keep only groups that meet in San Diego County. Sort each one into a bucket:
   - **gaming**: board games, chess, tabletop RPGs, mahjong, pinball, puzzles, video games/LAN, trivia, card games, and social groups whose main activity is game nights.
   - **sports**: soccer, running, pickleball, tennis, golf, fencing, volleyball, yoga, sailing, hiking, cycling, climbing, and other physical activity.
   - **makers_and_hobbies**: robotics, 3D printing, fabrication, makerspaces, electronics/Arduino, drones, VR/AR, and other hands-on hobbies.
   - **skip**: everything else, and groups outside San Diego County. List these by name at the end so I can see what you left out.

## Step 2: Visit each group you didn't skip
Open the group's main page, its "About" section, and its "Events" tab (upcoming events). Record:
- The group's full name, exactly as Meetup shows it. If the name is cut off on the groups list, take it from the group's own page. Then a 1–2 sentence description in plain language. Write it yourself; don't paste marketing text. Say who it's for and what happens there.
- Where it meets: a specific venue and street address if there's one regular spot, otherwise "Various (venue A, venue B, ...)".
- How often it meets, in a short readable form like "Every Saturday 10:00 AM–12:00 PM" or "Wednesdays 6:00 PM, Sundays 11:00 AM". Leave it as "" if there's no regular pattern.
- Cost: free, a per-event fee, or a membership/dues. Include the dollar amounts if they're shown.
- Links: the Meetup URL, plus any website, Instagram, Facebook, or Discord the group lists.
- Upcoming events over the next 4 weeks. If an event repeats on a regular schedule (for example weekly on Tuesdays), record it once with a recurrence rule instead of listing every date.

Only record what the pages actually show. If you can't find something, leave it empty. Don't guess.

## Step 3: Output
Give me ONE JSON code block in exactly this shape and nothing else, except for the skipped-groups list after it. Include all three buckets, even the empty ones.

```json
{
  "collected_at": "<ISO 8601 UTC timestamp, e.g. 2026-10-31T18:00:00Z>",
  "gaming": { "groups": [ ... ], "events": [ ... ] },
  "sports": { "groups": [ ... ], "events": [ ... ] },
  "makers_and_hobbies": { "groups": [ ... ], "events": [ ... ] }
}
```

Each **group**:
```json
{
  "id": "<a prefix for the bucket ('games-' for gaming, 'sports-' for sports, 'hobby-' for makers_and_hobbies), then the Meetup URL slug, lowercased, e.g. games-san-diego-social-chess-club>",
  "name": "San Diego Social Chess Club",
  "description": "Casual, friendly chess for beginners through masters at outdoor shaded tables. Just show up and play.",
  "neighborhood": "<one lowercase-hyphenated value, see below>",
  "address": "Clairemont Town Square, 4705 Clairemont Dr, San Diego",
  "frequency": "Every Saturday 10:00 AM–12:00 PM",
  "cost": { "kind": "free | fee | membership", "note": "optional detail, e.g. $5 per event" },
  "categories": ["chill"],
  "tags": ["chess", "beginner friendly", "outdoor"],
  "links": [
    { "kind": "meetup", "url": "https://www.meetup.com/san-diego-social-chess-club/" },
    { "kind": "instagram | facebook | discord | website | other", "url": "..." }
  ],
  "last_verified": "<today's date, YYYY-MM-DD>"
}
```

Each **event**:
```json
{
  "id": "<group id>-<short suffix like 'sat' or 'tue', or the date for one-off events, e.g. 2026-11-08>",
  "group_id": "<the group's id>",
  "title": "Social Chess at Clairemont Town Square",
  "description": "",
  "neighborhood": "clairemont",
  "location": "Clairemont Town Square, 4705 Clairemont Dr, San Diego",
  "start": "2026-11-07T10:00:00",
  "duration_minutes": 120,
  "rrule": "FREQ=WEEKLY;BYDAY=SA",
  "cost": { "kind": "free" },
  "url": "https://www.meetup.com/<group>/events/<event id>/"
}
```

Rules:
- `start` is local San Diego time with no time zone suffix. For recurring events, use the next upcoming date.
- `rrule` uses iCalendar RRULE format, e.g. `FREQ=WEEKLY;BYDAY=TU`, `FREQ=WEEKLY;BYDAY=MO;INTERVAL=2` for every other Monday, or `FREQ=MONTHLY;BYDAY=1SA` for the first Saturday of each month. Leave out the `rrule` key for one-off events.
- Leave out `cost` and `url` on an event if they aren't known. Leave out `cost` on a group if it isn't shown.
- `categories`: gaming groups get `["chill"]`, sports groups get `["active"]`, and makers_and_hobbies groups get `["chill"]`. A gaming or makers_and_hobbies group that's physically active (e.g. dancing, or flying drones outdoors) can get `["chill", "active"]`.
- `tags`: 2–5 short lowercase tags such as the activity, "beginner friendly", "all ages", "21+", "outdoor", "lgbtq+", or "coed".
- `neighborhood`: use one of these if it fits: alpine, balboa-park, bay-park, carlsbad, carmel-valley, chula-vista, clairemont, coronado, del-mar, downtown, el-cajon, encinitas, escondido, fallbrook, grantville, hillcrest, imperial-beach, kearny-mesa, la-jolla, la-mesa, lakeside, little-italy, mira-mesa, mission-bay, mission-beach, mission-valley, national-city, normal-heights, north-park, ocean-beach, oceanside, pacific-beach, point-loma, rancho-bernardo, san-diego-bay, san-marcos, santee, solana-beach, south-park, spring-valley, university-city, vista. Use "countywide" for groups that meet in several areas or whose location isn't clear. Don't use "san-diego"; pick the specific neighborhood or use "countywide". Use "online" for online-only events and groups. If none of these fit, make a new lowercase-hyphenated name for the city or neighborhood.
- If a group has no upcoming events, still include the group and give it no events.
- If several of my groups post the same event (same venue, date and time), list it only once, under the group that hosts it. If you can't tell which group hosts it, use the first group you found it under.
