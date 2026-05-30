# ∞Dx MCP Server

**Real-time street-level infrastructure intelligence for LATAM cities — powered by Artificial Infinity.**

Query road health, utility anomalies, signage, and asset conditions across Bogotá, Medellín, and other Colombian cities via natural language through any MCP-compatible AI agent.

---

## What is ∞Dx?

∞Dx is a street-level intelligence platform that turns continuous dashcam video into structured, decision-ready infrastructure intelligence. We continuously detect, monitor, and classify every road and utility asset across thousands of km of corridors.

This MCP server exposes that intelligence as callable tools for any AI agent — Claude, Cursor, GPT, or any local LLM.

---

## Quick Start

### Claude Desktop

Add to your `claude_desktop_config.json`:

```json
{
  "mcpServers": {
    "infinitydx": {
      "command": "npx",
      "args": ["-y", "@modelcontextprotocol/server-fetch"],
      "env": {
        "MCP_SERVER_URL": "https://jvf8mfmdqb.execute-api.us-east-1.amazonaws.com/production",
        "X_API_KEY": "your-api-key-here"
      }
    }
  }
}
```

### Cursor / Other MCP Clients

Connect to the remote MCP server:

```
URL: https://jvf8mfmdqb.execute-api.us-east-1.amazonaws.com/production
Header: X-Api-Key: your-api-key-here
```

Get your API key at **[artinfinitydx.com/mcp](https://artinfinitydx.com/mcp)**

---

## Available Tools

### `get_health_summary`
Get the infrastructure health picture for a city or neighborhood.

```
What is the infrastructure state of Bogotá?
Show me the anomaly rate for energy assets in Medellín
What is the road condition in the Chapinero neighborhood?
```

**Parameters:**
- `city` (required) — e.g. `Bogota`, `Medellín`, `Stevenage`
- `country` (optional) — ISO code, default `COL`
- `neighborhood` (optional) — e.g. `Chapinero`, `Normandia`
- `asset_group` (optional) — `Road`, `Energy & Utilities`, `Signage`, `Street Furniture`, `Vegetation`

---

### `get_anomalies`
Get active infrastructure anomalies for a city or neighborhood.

```
What infrastructure anomalies exist in Bogotá?
Show me faded road markings in Medellín from the last 90 days
What utility pole issues are in the Aeropuerto el Dorado area?
```

**Parameters:**
- `city` (required)
- `country` (optional) — default `COL`
- `neighborhood` (optional)
- `asset_group` (optional)
- `since_days` (optional) — default 30, max 900

---

### `get_assets_by_radius`
Get all infrastructure assets within a radius of a coordinate.

```
What assets are within 1km of these coordinates: 4.698, -74.109?
Show me road infrastructure near this location in Bogotá
What utility assets exist within 2km of this point in Medellín?
```

**Parameters:**
- `lat` (required) — latitude
- `lng` (required) — longitude
- `radius_km` (required) — 0–50km
- `country` (optional)
- `city` (optional)
- `asset_group` (optional)
- `asset_category` (optional)
- `neighborhood` (optional)

---

### `get_neighborhoods`
Discover available neighborhoods for a city. **No API key required.**

```
What neighborhoods are covered in Bogotá?
Which areas of Medellín do you have data for?
```

**Parameters:**
- `city` (required)
- `country` (optional) — default `COL`

---

## Example Queries

Once connected, ask your AI agent:

```
"What is the overall infrastructure health of Bogotá?"

"Show me the top anomalies in Medellín from the last 60 days"

"What road marking issues exist in the Chapinero neighborhood?"

"What infrastructure assets are within 1km of coordinates 4.698, -74.109?"

"What neighborhoods do you have coverage for in Bogotá?"

"How does the energy infrastructure anomaly rate compare between 
 Bogotá and Medellín?"

"What are the most common utility pole issues in Bogotá?"

"Show me faded road markings and poor sidewalks in Fontibon"
```

---

## Coverage

| City | Frames | Last Updated |
|------|--------|--------------|
| Bogotá, Colombia | 67,000+ | May 2026 |
| Medellín, Colombia | 14,800+ | March 2026 |
| Medellín Metro (Copacabana, Guarne, Itagüí, Envigado, Bello) | 11,400+ | March 2026 |
| Stevenage, UK | 371 | August 2024 |

**Asset categories covered:**
- Energy & Utilities: Streetlights, Utility Poles, Wiring
- Road: Road Markings, Potholes, Sidewalks
- Signage: Traffic Signs
- Street Furniture: Bus Stations, Benches, Bollards, Waste Bins
- Vegetation

---

## Pricing

| Tier | Price | Calls/month | Coordinates |
|------|-------|-------------|-------------|
| Free | $0 | 100 | ❌ |
| Explorer | $49/month | 5,000 | ✅ |
| Pro | $199/month | 50,000 | ✅ |
| Enterprise | Custom | Unlimited | ✅ |

Get your key at **[artinfinitydx.com/mcp](https://artinfinitydx.com/mcp)**

---

## API Endpoints

Base URL: `https://jvf8mfmdqb.execute-api.us-east-1.amazonaws.com/production`

| Endpoint | Auth | Description |
|----------|------|-------------|
| `GET /health` | None | Service status |
| `GET /geo/neighborhoods` | None | List neighborhoods for a city |
| `GET /health/summary` | API Key | City/neighborhood health summary |
| `GET /anomalies` | API Key | Active anomalies |
| `GET /assets/radius` | API Key | Assets within radius |

All authenticated endpoints require `X-Api-Key` header.

---

## About Artificial Infinity

Artificial Infinity is a Physical AI company building the continuously updated street-level intelligence layer that infrastructure operators, cities, and autonomous systems need to understand and act on the physical world.

- Website: [artinfinitydx.com](https://artinfinitydx.com)
- Email: gmo@virtualel.com
- NVIDIA Inception Program Partner
- AWS Startups Partner

---

## License

MIT — free to use, fork, and build on.
