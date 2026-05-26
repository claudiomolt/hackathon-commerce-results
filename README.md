# Hackathon Commerce — Resultados Finales

Presentación HTML estática con los resultados finales de la Hackathon Commerce de La Crypta 2026.

- **Producción:** https://hackathon-commerce-results.vercel.app
- **Repo:** https://github.com/claudiomolt/hackathon-commerce-results
- **Stack:** HTML/CSS/JS vanilla, sin build step
- **Deploy:** Vercel

## Qué contiene

La presentación incluye:

1. Cover de resultados finales
2. Metodología de evaluación con 3 jueces
3. Datos generales del torneo
4. Podio
5. Detalle del 1° puesto: Cursats
6. Detalle del 2° puesto: QRWapu
7. Detalle del 3° puesto: Zaploop
8. Mención fuerte: wapufy
9. Ranking completo
10. Lectura final

## Estructura del proyecto

```text
.
├── index.html              # Presentación completa: estilos, datos inline, slides y navegación
├── data/
│   └── projects.json       # Dataset espejo para continuar el proyecto desde otro IDE
├── docs/
│   └── PRESENTATION.md     # Documentación técnica del render/deploy
├── package.json            # Script mínimo para servir estático
└── README.md
```

## Data principal

La data que renderiza el HTML vive actualmente en el array inline `projects` dentro de `index.html`.

También está espejada en:

```text
data/projects.json
```

Ese JSON existe para que otro IDE/agente pueda entender y modificar rápido el ranking sin leer todo el HTML. Si se cambia el JSON, hay que actualizar también el array inline de `index.html` o refactorizar el HTML para cargar el JSON dinámicamente.

### Campos por proyecto

| Campo | Tipo | Uso |
|---|---|---|
| `rank` | number | Posición final |
| `name` | string | Nombre público del proyecto |
| `team` | string | Equipo / autor |
| `score` | number | Score final renderizado |
| `raw` | number | Promedio bruto antes de penalización |
| `penalty` | number | Penalización aplicada, ej. `2` por no pitch |
| `pitch` | string/null | Timestamp del pitch en CC #161 o `null` |
| `demo` | `sí`/`no` | Si se localizó demo pública |
| `repo` | string | Repo GitHub del proyecto |
| `note` | string | Resumen corto mostrado en slides/tablas |
| `judges` | number[] | Scores de Gorilatron, Gorilator y Claudio |

## Lista de proyectos

| Rank | Proyecto | Equipo | Score | Bruto | Penal. | Pitch | Demo | Repo |
|---:|---|---|---:|---:|---:|---|---|---|
| 1 | Cursats | Anix · Fred · wder | 8.24 | 8.24 | 0 | 77:47 | sí | https://github.com/bitbybit-ar/bitbybit-cursats |
| 2 | QRWapu | CapScabio | 7.80 | 7.80 | 0 | 97:30 | sí | https://github.com/CapScabio/QRWapu |
| 3 | Zaploop | Burgos | 7.52 | 7.52 | 0 | 86:38 | sí | https://github.com/Burgos247/Zaploop |
| 4 | wapufy | Looker | 7.42 | 7.42 | 0 | 59:54 | sí | https://github.com/Lo0ker-Noma/wapify |
| 5 | tiendita | negr0 | 5.36 | 7.36 | 2 | — | sí | https://github.com/Negr087/tiendita |
| 6 | hash 21 | Lai ⚡️ | 4.95 | 6.95 | 2 | — | sí | https://github.com/warrior-lai/hash-21 |
| 7 | SatTope | 13e700e2… | 4.53 | 4.53 | 0 | 69:05 | no | https://github.com/julian2000-code/btcpay-wapu-bridge |
| 8 | AgendaPu | Lalo | 4.23 | 6.23 | 2 | — | sí | https://github.com/Lalo1821/agendapu |
| 9 | WapuBot | nic_o | 2.83 | 4.83 | 2 | — | no | https://github.com/landaverdend/WapuBot |
| 10 | BTCpay Wapu Bridge | 13e700e2… | 2.00 | 4.00 | 2 | — | no | https://github.com/julian2000-code/btcpay-wapu-bridge |
| 11 | wpay | 8cce6d96… | 0.00 | 0.00 | 2 | — | no | https://github.com/unllamas/wpay |

## Criterio de evaluación

- **Gorilatron:** código, build, estructura, tests, seguridad e innovación técnica.
- **Gorilator:** UX, demo, flujo funcional, QR/Lightning y completitud.
- **Claudio:** viabilidad, impacto Bitcoin/Lightning, soberanía y potencial grassroots.

Regla aplicada en la presentación:

```text
Proyecto sin pitch vivo detectado = -2 puntos sobre el promedio bruto.
```

## Desarrollo local

```bash
npm start
```

O sin Node tooling:

```bash
python3 -m http.server 4177
# abrir http://127.0.0.1:4177
```

## Controles de la presentación

- `→`, `PageDown`, `Space`: siguiente slide
- `←`, `PageUp`, `Backspace`: slide anterior
- `F`: fullscreen
- Mobile: swipe horizontal, botones inferiores y zonas invisibles laterales
- Deep links: `#1`, `#2`, etc.

## Deploy

El proyecto está linkeado en Vercel (`.vercel/project.json`).

```bash
vercel deploy --prod
```

Alias de producción:

```text
https://hackathon-commerce-results.vercel.app
```

## Nota importante

No usar `function top()` en el scope global. Choca con `window.top` en Chromium y rompe el render de slides. Usar `renderTop()`.

Más detalles técnicos en [`docs/PRESENTATION.md`](docs/PRESENTATION.md).
