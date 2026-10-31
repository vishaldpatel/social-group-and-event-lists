# Social Group and Event Lists

JSON lists of social groups and events, hosted on GitHub Pages so they can be imported as Lists into the Social Activities project.

To import a list, copy its URL from the tables below and paste it into Social Activities.

A machine-readable catalog of every list is at [`index.json`](https://vishaldpatel.github.io/social-group-and-event-lists/index.json).

## San Diego County

| List | Description | URL |
| --- | --- | --- |
| [Cars & Coffee Meetups](https://vishaldpatel.github.io/social-group-and-event-lists/SanDiegoCounty/cars-and-coffee.json) | Cars and coffee meetups around San Diego County. | `https://vishaldpatel.github.io/social-group-and-event-lists/SanDiegoCounty/cars-and-coffee.json` |
| [Game Nights](https://vishaldpatel.github.io/social-group-and-event-lists/SanDiegoCounty/game-nights.json) | Trivia and bingo nights around San Diego County. | `https://vishaldpatel.github.io/social-group-and-event-lists/SanDiegoCounty/game-nights.json` |
| [Group Classes](https://vishaldpatel.github.io/social-group-and-event-lists/SanDiegoCounty/group-classes.json) | Hands-on classes you take with others, like cooking classes. | `https://vishaldpatel.github.io/social-group-and-event-lists/SanDiegoCounty/group-classes.json` |
| [Meetup Groups - Gaming](https://vishaldpatel.github.io/social-group-and-event-lists/SanDiegoCounty/meetup-groups-for-gaming.json) | Board game, chess, RPG, mahjong, pinball, puzzle and video game groups around San Diego County, collected from their Meetup pages. | `https://vishaldpatel.github.io/social-group-and-event-lists/SanDiegoCounty/meetup-groups-for-gaming.json` |
| [Meetup Groups - Sports](https://vishaldpatel.github.io/social-group-and-event-lists/SanDiegoCounty/meetup-groups-for-sports.json) | Soccer, running, pickleball, tennis, golf, fencing and beach volleyball groups around San Diego County, found through Meetup's sports searches. | `https://vishaldpatel.github.io/social-group-and-event-lists/SanDiegoCounty/meetup-groups-for-sports.json` |
| [Meetup Groups - Makers and Hobbies](https://vishaldpatel.github.io/social-group-and-event-lists/SanDiegoCounty/meetup-groups-for-makers-and-hobbies.json) | Robotics, 3D printing, fabrication, drone and VR groups around San Diego County, collected from their Meetup pages. | `https://vishaldpatel.github.io/social-group-and-event-lists/SanDiegoCounty/meetup-groups-for-makers-and-hobbies.json` |
| [Run Clubs](https://vishaldpatel.github.io/social-group-and-event-lists/SanDiegoCounty/run-clubs.json) | Run clubs around San Diego County. | `https://vishaldpatel.github.io/social-group-and-event-lists/SanDiegoCounty/run-clubs.json` |

## Adding a list

Put each list in a directory named for its region (for example, `SanDiegoCounty/`), then add a row for it to this README and an entry for it to `index.json`.

## Updating the Meetup lists

[`prompts/meetup-update.md`](prompts/meetup-update.md) is a prompt for the Claude browser extension. It reads the Meetup groups you belong to and returns JSON in the same format as the Meetup lists, ready to merge into the gaming, sports, and makers and hobbies lists.
