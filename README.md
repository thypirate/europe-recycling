# Europe Recycling

An interactive 3D globe visualising municipal waste recycling rates across 31 European countries, built with React, Three.js and [react-globe.gl](https://github.com/vasturiano/react-globe.gl).

**Live demo: [thypirate.github.io/europe-recycling](https://thypirate.github.io/europe-recycling/)**

![recycling globe](https://media0.giphy.com/media/v1.Y2lkPTc5MGI3NjExemNhdHBzYzhxN3VyNDN3cDQ5M282bmh0anN1ajl3Y2dnbDAxcHAzZiZlcD12MV9pbnRlcm5hbF9naWZfYnlfaWQmY3Q9Zw/OcdBzXdTXBoAXWzV7N/giphy.gif)

## What you're looking at

### The globe points

Each dot represents a country. Its size and colour reflect the national municipal waste recycling rate:

| Colour       | Rate   |
| ------------ | ------ |
| Green        | ≥ 50%  |
| Yellow-green | 35–50% |
| Yellow       | 20–35% |
| Orange       | 10–20% |
| Red          | < 10%  |

### What about the arcs you say?

The animated arcs are the 40 largest cross-border waste shipments between countries on the globe in 2024, taken from Eurostat's [`env_wasship`](https://ec.europa.eu/eurostat/databrowser/view/env_wasship/default/table?lang=en) dataset (_Transboundary shipments of notified waste by partner, hazardousness and waste management operations_). Each flow is the exporting country's reported tonnage, hazardous and non-hazardous combined. This covers **all notified waste**, not only municipal waste, so the arcs and the dots measure different things. Arc thickness scales with tonnage. Hover over an arc to see its tonnes, the recovery/disposal split and the source.

Each arc is coloured by the treatment the shipment was notified for:

| Colour | Treatment                                                                         |
| ------ | --------------------------------------------------------------------------------- |
| Green  | Recovery (R-codes) is at least 75% of the flow                                    |
| Red    | Disposal (D-codes) is at least 75% of the flow                                    |
| Amber  | Mixed: neither recovery nor disposal reaches 75%                                  |

In 2024 the largest flow is Belgium → Netherlands (3.4 Mt), followed by Netherlands → Germany (2.3 Mt). Luxembourg exports by far the most waste per capita: about 3,150 kg per person, against 354 kg for Belgium, the next highest. None of the 40 largest flows is mostly disposal. Italy's exports to Germany, Sweden and France are mixed.

The arc data in `src/data/wasteTrade.ts` is generated, so don't edit it by hand. To rebuild it from the Eurostat API:

```bash
npx tsx scripts/fetch-waste-trade.ts              # latest year, 40 largest flows
npx tsx scripts/fetch-waste-trade.ts --year 2023 --top 30
```

## Getting started

```bash
npm ci
npm run dev
```

The production build is a single ~2 MB JavaScript bundle, most of which is three.js. That's acceptable for a demo. Code-splitting the globe would be the next step.

## License

Licensed under MIT
