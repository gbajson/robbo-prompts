# robbo-prompts

The prompts and the site notes of [Robbo](https://github.com/gbajson/robbo), the agent that drives Firefox for a user.

- `prompts/`: `system.md` (how Robbo works: what the agent sees, the actions), `planner.md` (splits a goal into stages and writes the guidance), `reader.md`, `judge.md`, `answer.md`, and `user.md` (a Go `text/template` of each screen's request).
- `abilities/<domain>.yaml`: what Robbo can do on a site (like a post, write a comment), each ability a goal of Robbo's regression set (`just regress`), with the check of its result and the step that undoes it. The comment at the top of each file says how they are run.
- `sites/<domain>.md`: notes about one site. The first line is `domains: facebook.com, fb.com` (registrable domains), the rest are the notes, at most 3000 bytes. Only screens whose page is on one of the domains get them.

Robbo reads these files again for every call (`ROBBO_AGENT_PROMPTS`, `ROBBO_AGENT_SITES`), so an edit works for the next screen. The prompts name the actions that Robbo's code runs: use the revision that Robbo's checkout pins (it includes this repository as a submodule).

Keep `system.md` as short as possible: it is sent with every screen. What is true of one site goes to `sites/`, what is true of one kind of goal to `planner.md`.
