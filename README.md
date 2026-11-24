# robbo-prompts

The prompts and the site notes of [Robbo](https://github.com/gbajson/robbo), the agent that drives Firefox for a user.

- `prompts/`: `system.md` (how Robbo works: what the agent sees, the actions), `planner.md` (splits a goal into stages and writes the guidance), `reader.md`, `judge.md`, `answer.md`, and `user.md` (a Go `text/template` of each screen's request).
- `sites/<domain>/`: everything about one site, in one directory named after one of its domains (a site with several domains, facebook.com and fb.com, has one directory):
  - `notes.md`: notes about the site. The first line is `domains: facebook.com, fb.com` (all its registrable domains, the directory's name among them), the rest are the notes, at most 3000 bytes. Only screens whose page is on one of the domains get them.
  - `abilities.yaml`: what Robbo can do on the site (like a post, write a comment), each ability a goal of Robbo's regression set (`just regress`), with the check of its result and the step that undoes it. The comment at the top of the file says how they are run.

## Abilities

The id of an ability is `<site>.<verb>-<object>`, such as `facebook.get-comments`:

- `site`: the directory's name without its last part, dots as dashes (`facebook.com` → `facebook`, `news.ycombinator.com` → `news-ycombinator`);
- `verb`: `get` when Robbo only reads and answers (no `undo`); any other verb (`like`, `write`, `delete`, `send`) changes the site, and the ability needs `undo`, so that the next batch starts from the same state;
- `object`: what it is about, singular for one thing (`post-url`), plural for a list (`comments`).

Robbo's regression set refuses an id that does not follow this.

An ability may have `options`: a `{{name}}` of its texts with a default, either one value (`count: 10`) or the list of the allowed values, the first being the default (`order: [All comments, Most relevant, Newest]`). `ROBBO_REGRESS_<NAME>` of Robbo's `.env` or environment overrides the default; a value that is not in the list is refused.

Robbo reads these files again for every call (`ROBBO_AGENT_PROMPTS`, `ROBBO_AGENT_SITES`), so an edit works for the next screen. The prompts name the actions that Robbo's code runs: use the revision that Robbo's checkout pins (it includes this repository as a submodule).

Keep `system.md` as short as possible: it is sent with every screen. What is true of one site goes to `sites/<domain>/notes.md`, what is true of one kind of goal to `planner.md`.
