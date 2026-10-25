# SLO: Robot Shop availability

## What I measure
How many requests to the shop work without a 5xx error.
Traefik counts the requests and Prometheus works out the percentage.

## Target
99% of requests should work, over 30 days.

## Error budget
1% of requests can fail. That's about 7 hours of downtime in a month.

## Alert
If more than 5% of requests fail for 2 minutes, Slack gets an alert
with a link to the runbook.

## What I do with the budget
- Plenty of budget left: keep shipping changes as normal.
- Less than half left: only small changes, fix problems first.
- Budget used up: no new features until the shop is stable again.
- A big incident (more than 20% of the budget): write a postmortem.

## Notes
- I turned off load-gen's fake errors (ERROR=0) so only real failures count.
- Prometheus only keeps 2 days of data on my laptop, so the 30-day number is an estimate.
