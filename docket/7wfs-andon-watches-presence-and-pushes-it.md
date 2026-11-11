+++
kind = "step"
created = 2026-11-11T20:54:01Z
state = "open"
priority = "normal"
+++
# andon serves presence on request

**Delivers:** andon, the fivesparks domain's page host, serves presence on the estate's pages as dokit's PLAN-005 designs it (dokit ARCH-004 §11), by its own existing pattern: a request for a site's `presence.json` runs the site's presence command first when the last run is more than about 2 s old, then serves the file. The page polls it every 2 to 3 s from its own origin. No watcher, no process tracking, no event stream: a lease change or a holder's exit shows within a few seconds because each poll re-joins. Jim chose this simple start on 2026-11-11.

**Config:** each site names its presence command beside its refresh command, e.g. `presence = ["/Users/Shared/host-warden/bin/dokit", "presence", "--workspace", "estate.toml", "--out", "page/presence.json"]`.

**Later, if a few seconds feels slow:** watch /Users/Shared/presence and the live holders' processes (kqueue exit notice), re-join on change, and push to open pages as server-sent events. A separate ask then.

**After:** dokit's join (`dokit:6un5`, read and join presence) for the command; dokit's page unit (`dokit:w80i`) for the polling page. The preview site takes it first, against a scratch store, before the release (`dokit:70b9`).

**Done when:** on the preview site, a session taking an ask, idling and ending shows within a few seconds without a reload.
