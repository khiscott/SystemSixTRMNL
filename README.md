# SystemSix TRMNL

A retro Macintosh System 6 desktop for your [TRMNL](https://usetrmnl.com) e-ink display. Inspired by [SystemSix](https://github.com/EngineersNeedArt/SystemSix) by EngineersNeedArt.

Displays:
- Classic Mac desktop with daily-rotating icon set
- Large date with day/month/year
- Current temperature and weather condition
- Moon phase with image
- Trash can (empty or full based on your trash day)
- Retro Mac menu bar with live clock

Compatible with **TRMNL** (800×480, 1-bit) and **TRMNL X** (4-bit, landscape + portrait).

---

## Setup

### 1. Push this repo to GitHub

```bash
git remote add origin https://github.com/khiscott/SystemSixTRMNL.git
git push -u origin main
```

### 2. Update the CDN URL in the template

### 3. Create a Private Plugin in TRMNL

1. Go to [usetrmnl.com](https://usetrmnl.com) → **Plugins** → **New Private Plugin**
2. Give it a name (e.g. "System Six")
3. Paste the contents of `templates/full.liquid` into the **Markup** field
4. Under **Polling URL**, enter:
   ```
   https://api.open-meteo.com/v1/forecast?latitude=##{{latitude}}&longitude=##{{longitude}}&current=temperature_2m,weather_code&timezone=auto&temperature_unit=##{{temperature_unit}}
   ```
5. Under **Settings**, paste the contents of `settings.yml`
6. Save and add the plugin to your playlist

### 4. Configure your settings

In the plugin settings, enter:
- **Latitude / Longitude** — your location (e.g. `40.7128` / `-74.0060` for New York)
- **Temperature Unit** — Fahrenheit or Celsius
- **Trash Day** — the day your trash goes out, or "None" to disable

---

## How It Works

- **Weather** is fetched directly from [Open-Meteo](https://open-meteo.com) — free, no API key required. TRMNL polls the URL on your configured refresh interval and injects `temperature_2m` and `weather_code` as template variables.
- **Moon phase** is calculated in the template using the same algorithm as the original SystemSix Python code (days since known new moon modulo lunar cycle).
- **Icons** are served from this GitHub repo via jsDelivr CDN. There are 147 classic Mac icons across 6 categories (art, dev, game, office, system, utilities). The icon set rotates daily based on day-of-year.
- **Trash day** compares today's day-of-week against your configured trash day and shows a full or empty trash can.

---

## Credits

- Original [SystemSix](https://github.com/EngineersNeedArt/SystemSix) by John Calhoun (EngineersNeedArt) — artwork, moon phase algorithm, concept
- [ChiKareGo2](https://github.com/IdreesInc/Monocraft) font (Creative Commons)
- Weather data by [Open-Meteo](https://open-meteo.com)
