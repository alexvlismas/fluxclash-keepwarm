# fluxclash-keepwarm

One scheduled GitHub Action that pings `https://fluxclash.com/api/health` so the
Render free-tier instance behind fluxclash.com does not idle out.

It exists as its own **public** repository for one reason: Actions minutes are
free and unmetered for public repos and billed for private ones, and the FLUX
repositories are private. Nothing sensitive lives here — the workflow curls a
URL that is already public.

It replaces `com.fluxclash.keepwarm`, a LaunchAgent on a MacBook Air. That agent
worked, but `StartInterval` jobs do not fire while the machine sleeps: measured
over 15-20 Sep 2026, 44 of 478 intervals exceeded Render's ~15-minute idle
window and the instance was cold-eligible for 25.0 of 109.4 hours (22.8%).

If the ping fails, the run fails and GitHub emails — so this doubles as a
minimal uptime alarm.
