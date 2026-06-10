# Limitations

## Sub-agent visibility

Support for sub-agent visibility is limited. Sessions that spawn sub-agents may not surface the full call tree in the dashboard — you'll see the top-level traffic, but inner sub-agent calls may be incomplete or missing.

## Data does not persist across container restarts

Stopping and removing the containers (`docker compose down`) will wipe all stored data. To preserve your data across restarts, make sure to mount a persistent volume for the Postgres container before you bring the stack up.

## Not intended for wide production deployment

ClaudeCosts is designed for **limited-scale use** — internal teams, pilot rollouts, and evaluation. It is not enabled for high-volume or wide production deployment.

If you need to take it to production — higher availability, larger scale, enterprise SLAs — reach out at **[hello@realmlabs.ai](mailto:hello@realmlabs.ai)** and we'll work with you directly.
