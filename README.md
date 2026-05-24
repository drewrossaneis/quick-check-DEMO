# Quick Action Helper — Fewer Healthy Instances

A fictional prototype created only to demonstrate the on-call alert flow for the **Fewer Healthy Instances** scenario.

No real company data, names, links, schedules, or credentials are included. Not connected to any internal system.

## What it does

When a *Fewer Healthy Instances* alert arrives, the operator selects the affected country. The helper immediately:

- Calculates the **local time** and determines whether the country is within or outside **working hours** (Mon–Fri 09:00–18:00 local time).
- Surfaces the country-specific **Ops Chat** link so the operator can check for planned restart notices or known issues before acting.
- Shows the appropriate **action path** — inform the wider team (working hours) or follow the call-out procedure (outside hours).
- For outside-hours scenarios, displays a **3-minute countdown timer** for healthy instances = 1, and an immediate call prompt for healthy instances = 0.
- Shows the **on-call engineer** for the day and a **CALL button** already linked to their contact, loaded from `oncall.json`.

Up to four country cards can be active simultaneously.

## On-call data

On-call names and contact details are stored in **`oncall.json`**, separate from the application code. Edit that file to update the current on-call engineer without touching `index.html`.

```json
{
  "countries": {
    "AR": {
      "oncall": {
        "name": "Engineer Name",
        "phone": "tel:+00000000000"
      }
    }
  }
}
```

## Running locally

The app loads `oncall.json` via `fetch`, which requires a local HTTP server (browsers block `fetch` on `file://` URLs).

```bash
# Python 3
python -m http.server 8080
# then open http://localhost:8080
```

Alternatively, use any static server (e.g. `npx serve .`). The app falls back to built-in sample data if `oncall.json` cannot be fetched.

