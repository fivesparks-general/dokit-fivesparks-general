+++
kind = "step"
created = 2026-11-11T20:54:01Z
state = "open"
priority = "normal"
+++
# andon watches presence and pushes it live

**Delivers:** andon, the fivesparks domain's page host, serves presence on the estate's pages as dokit's PLAN-005 designs it (dokit ARCH-004 §11): it runs `dokit presence` when a file in /Users/Shared/presence changes or a live holder's process exits (kqueue exit notice, else a poll of a few seconds), writes presence.json beside each site's page, and pushes it to open pages as server-sent events from the page's own origin.

**After:** dokit's join (`dokit:6un5`, read and join presence) for the command; dokit's page unit (`dokit:w80i`) for what the page reads. The preview site takes it first, against a scratch store, before the release (`dokit:70b9`).

**Done when:** on the preview site, a session taking an ask, idling and ending shows within seconds without a reload; andon's config names each site's presence command beside its refresh command.
