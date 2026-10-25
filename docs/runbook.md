# Runbook: RobotShopAvailabilityLow

## What it means
More than 5% of requests to the shop are failing. Customers can't browse or buy.

## What to do first
Get the shop working again. Find the real cause later.

1. Open the Grafana dashboard and check which route has errors.
2. Check the pods: `kubectl get pods -n robot-shop`
3. Fix what you see:
   - Pod missing: `kubectl scale deployment <name> -n robot-shop --replicas=1`
   - Pod stuck or restarting: `kubectl rollout restart deployment/<name> -n robot-shop`
   - Broke after a deploy: `helm rollback robot-shop -n robot-shop`
4. Wait for the RESOLVED message in Slack.

## Finding the cause
- Logs in Grafana (Explore, Loki): `{service="<name>"} | detected_level="error"`
- Why a pod restarted: `kubectl describe pod <pod> -n robot-shop`
- Slow requests: check the trace in Jaeger

## After
Write a short postmortem: what happened, when, why, and what we'll change.
