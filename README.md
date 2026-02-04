<p align="center">
  <img src="img%20Scalper.png" alt="SMS Pro — Smart Money Scalper" width="800" />
</p>

<p align="center">
  <img src="https://img.shields.io/badge/Pine_Script-v6-blue?style=for-the-badge&logo=tradingview&logoColor=white" />
  <img src="https://img.shields.io/badge/Platform-TradingView-131722?style=for-the-badge&logo=tradingview&logoColor=white" />
  <img src="https://img.shields.io/badge/Type-Scalping_System-green?style=for-the-badge" />
  <img src="https://img.shields.io/badge/License-Private-red?style=for-the-badge" />
</p>

<h1 align="center">
  📊 SMS Pro — Smart Money Scalper
</h1>

<p align="center">
  <strong>Sistema profesional de scalping basado en conceptos de Smart Money (ICT)</strong><br>
  Indicadores de alta precision para TradingView optimizados por par e instrumento
</p>

<p align="center">
  <a href="#-scripts-disponibles">Scripts</a> •
  <a href="#-arquitectura-del-sistema">Arquitectura</a> •
  <a href="#-guia-de-instalacion-en-tradingview">Instalacion</a> •
  <a href="#-configuracion-por-par">Configuracion</a> •
  <a href="#-sistema-de-confluencias">Confluencias</a> •
  <a href="#-gestion-de-riesgo">Riesgo</a> •
  <a href="#-alertas">Alertas</a>
</p>

---

## 🗂️ Scripts Disponibles

| # | Archivo | Instrumento | Version | FVG | Confluencias | Kill Zones |
|:-:|---------|:-----------:|:-------:|:---:|:------------:|:----------:|
| 1 | `SMS_EURUSD_v3_FVG.pine` | EUR/USD | v3 | ✅ | 8 | London, NY |
| 2 | `SMS_JPY_v3_Fixed.pine` | USD/JPY | v3 | ❌ | 7 | Tokyo, London, NY |
| 3 | `SMS_USDJPY_v4_FVG.pine` | USD/JPY | v4 | ✅ | 8 | Tokyo, London, NY |
| 4 | `SMS_XAUUSD_v3_FVG.pine` | XAU/USD | v3 | ✅ | 8 | London, NY |

---

## 🏗️ Arquitectura del Sistema

Todos los scripts comparten una arquitectura modular basada en 8 pilares de analisis Smart Money:

```
┌─────────────────────────────────────────────────────────────────────┐
│                     📊 SMS Pro — MOTOR CENTRAL                      │
├─────────────┬─────────────┬─────────────┬─────────────┬────────────┤
│   📈 EMAs   │ 🏗️ Market  │  📦 Order   │  🔲 Fair    │ 💧 Liquid. │
│   9/21/200  │  Structure  │   Blocks    │ Value Gaps  │  Sweeps    │
│  Tendencia  │  BOS/CHoCH  │  OB Bull/   │  FVG Bull/  │  SW High/  │
│  principal  │  Reversal   │  OB Bear    │  FVG Bear   │  SW Low    │
├─────────────┼─────────────┼─────────────┼─────────────┼────────────┤
│  📐 Fibo    │ 🕐 Kill     │ 🕯️ Candle  │  🎯 Entry   │ 🛡️ Risk   │
│  50%/61.8%  │   Zones     │  Patterns   │  Confluence │ Management │
│  Discount/  │  LDN/NY/TK  │  Rejection  │  Min 3/8    │  ATR + OB  │
│  Premium    │  Sessions   │  Engulfing  │  Scoring    │  SL & TP   │
└─────────────┴─────────────┴─────────────┴─────────────┴────────────┘
                                    │
                                    ▼
                    ┌───────────────────────────┐
                    │  🚀 SENAL DE ENTRADA      │
                    │  ▲ LONG  o  ▼ SHORT       │
                    │  + SL / TP / Confluencias  │
                    └───────────────────────────┘
```

---

## 📜 Detalle de Cada Script

---

### 1️⃣ SMS Pro EUR/USD v3 — `SMS_EURUSD_v3_FVG.pine`

> 🎯 **Optimizado para el par mas liquido del mercado forex**

```
┌──────────────────────────────────────────────────┐
│  SMS Pro EURUSD v3          Shorttitle: SMS-EUR  │
│  Pine Script v6 | Overlay | FVG Activo           │
├──────────────────────────────────────────────────┤
│  Spread por defecto:  0.8 pips                   │
│  Buffer:              0.3 pips                   │
│  Pip value:           0.0001                     │
│  ATR Multiplicador:   1.2x                       │
│  R:R Ratio:           2:1                        │
│  Confluencias:        8 max                      │
└──────────────────────────────────────────────────┘
```

**Modulos activos:**

| Modulo | Descripcion | Visual en Chart |
|--------|-------------|:---------------:|
| EMA 9/21/200 | Tendencia corta, media y larga plazo | Lineas verde/roja/blanca |
| Market Structure | Detecta BOS (continuacion) y CHoCH (reversal) | Labels en chart |
| Order Blocks | Zonas de oferta/demanda institucional (max 3) | Cajas verde/roja semi-transparentes |
| FVG | Fair Value Gaps — desequilibrios de precio | Cajas azul/naranja |
| Liquidity Sweeps | Barren de liquidez sobre highs/lows recientes | Labels "SW" |
| Fibonacci | Niveles 50% y 61.8% (discount/premium) | Linea blanca punteada |
| Kill Zones | London (02-05 EST) y NY (07-10 EST) | Fondo azul/verde |
| Candle Patterns | Rejection y Engulfing (bull/bear) | Parte del scoring |

**Panel informativo (esquina superior derecha):**

```
┌──────────────────────────┐
│  SMS-EUR v3    FVG+      │
├──────────────────────────┤
│  Trend:     🟢 BULL      │
│  KZ:        London       │
│  Fibo:      DISCOUNT     │
│  ATR:       5.2 pips     │
│  OB:        Bull activo  │
│  FVG:       Bear activo  │
│  Conf L:    5/8          │
│  Conf S:    2/8          │
│  Spread:    0.8p         │
│  SL Mode:   ATR          │
│  Alerts:    ON           │
│  FVG Conf:  ON           │
└──────────────────────────┘
```

---

### 2️⃣ SMS Pro USD/JPY v3 — `SMS_JPY_v3_Fixed.pine`

> 🇯🇵 **Version estable para pares yen — sin FVG, con Tokyo Kill Zone**

```
┌──────────────────────────────────────────────────┐
│  SMS Pro USDJPY v3          Shorttitle: SMS-JPY  │
│  Pine Script v6 | Overlay | Sin FVG              │
├──────────────────────────────────────────────────┤
│  Spread por defecto:  1.5 pips                   │
│  Buffer:              0.5 pips                   │
│  Pip value:           0.01                       │
│  ATR Multiplicador:   1.2x                       │
│  R:R Ratio:           2:1                        │
│  Confluencias:        7 max                      │
└──────────────────────────────────────────────────┘
```

**Diferencias clave vs EUR/USD:**

```
  EUR/USD                              USD/JPY v3
  ───────                              ──────────
  Pip = 0.0001                    →    Pip = 0.01
  Spread = 0.8 pips               →    Spread = 1.5 pips
  Sin Tokyo Kill Zone             →    Tokyo KZ: 19:00-02:00 EST ⭐
  FVG activo como confluencia     →    Sin FVG
  8 confluencias                  →    7 confluencias
  Sweeps simples                  →    Sweeps con filtro ATR avanzado ⚡
```

**Filtrado avanzado de Liquidity Sweeps:**
- El sweep debe ser significativo vs ATR (> 0.3x ATR)
- Se filtra por: proximidad a Equal H/L, cercanía a Order Block, o estar en Kill Zone
- Sweeps clave marcados con ⚡ (lightning bolt)

**Kill Zones con Tokyo:**

```
  UTC-5 (EST)
  ├── 19:00 ─────── 02:00 ──→  🟡 Tokyo Kill Zone (sesion asiatica)
  ├── 02:00 ─────── 05:00 ──→  🔵 London Kill Zone
  ├── 07:00 ─────── 10:00 ──→  🟢 New York Kill Zone
  └── 08:00 ─────── 11:00 ──→  🟢 NY Overlap
```

---

### 3️⃣ SMS Pro USD/JPY v4 — `SMS_USDJPY_v4_FVG.pine`

> 🚀 **Version mejorada del JPY con FVG integrado como confluencia**

```
┌──────────────────────────────────────────────────┐
│  SMS Pro USDJPY v4          Shorttitle: SMS-JPY  │
│  Pine Script v6 | Overlay | FVG Activo           │
├──────────────────────────────────────────────────┤
│  Spread por defecto:  1.5 pips                   │
│  Buffer:              0.5 pips                   │
│  Pip value:           0.01                       │
│  ATR Multiplicador:   1.2x                       │
│  R:R Ratio:           2:1                        │
│  Confluencias:        8 max                      │
└──────────────────────────────────────────────────┘
```

**Mejoras sobre v3:**

```
  v3 (Fixed)                            v4 (FVG)
  ──────────                            ────────
  7 confluencias                  →     8 confluencias (+FVG)
  Sin Fair Value Gaps             →     FVG Bull (azul) + FVG Bear (naranja)
  Panel de 12 filas               →     Panel de 14 filas
  Sin indicador FVG               →     Funciones inBullFVG() / inBearFVG()
  Senales sin "+FVG"              →     Labels muestran "+FVG" si aplica
  Tokyo KZ basico                 →     Tokyo KZ con toggle independiente
```

**Sistema de confluencias completo (v4):**

```
  ┌─────────────────────────────────────────────────────────┐
  │              CONFLUENCIAS PARA LONG (8 max)              │
  ├─────┬───────────────────────────────────────────────────┤
  │  1  │  EMA 9 > EMA 21 (tendencia corta alcista)        │
  │  2  │  Precio > EMA 200 (tendencia larga alcista)      │
  │  3  │  Precio dentro de Order Block alcista             │
  │  4  │  Precio en zona DISCOUNT de Fibonacci             │
  │  5  │  Patron de vela alcista (rejection/engulfing)     │
  │  6  │  Liquidity Sweep en low reciente (1-2 velas)     │
  │  7  │  Estructura: CHoCH bull o BOS bull reciente      │
  │  8  │  Precio dentro de FVG alcista ⭐ NUEVO            │
  ├─────┴───────────────────────────────────────────────────┤
  │  Minimo requerido: 3/8 (configurable hasta 7)          │
  └─────────────────────────────────────────────────────────┘
```

---

### 4️⃣ SMS Pro XAU/USD v3 — `SMS_XAUUSD_v3_FVG.pine`

> 🥇 **Optimizado para trading de Oro — spreads y volatilidad ajustados**

```
┌──────────────────────────────────────────────────┐
│  SMS Pro XAUUSD v3          Shorttitle: SMS-XAU  │
│  Pine Script v6 | Overlay | FVG Activo           │
├──────────────────────────────────────────────────┤
│  Spread por defecto:  $3.0 (dolares, no pips)    │
│  Buffer:              $1.0                       │
│  Sin conversion a pips (precio absoluto)         │
│  ATR Multiplicador:   1.5x ⬆️ (mayor que forex) │
│  R:R Ratio:           2:1                        │
│  Confluencias:        8 max                      │
│  FVG Min Size:        0.15% ⬆️ (mayor que forex) │
└──────────────────────────────────────────────────┘
```

**Adaptaciones especificas para Oro:**

```
                    FOREX (EUR/JPY)          ORO (XAU/USD)
                    ───────────────          ─────────────
  Unidad SL/TP:    Pips                     Dolares ($)
  Spread:          0.8 - 1.5 pips           $3.0
  ATR Mult:        1.2x                     1.5x (mas volatil)
  FVG Min:         0.03%                    0.15% (gaps mayores)
  OB Threshold:    0.3 x ATR               0.5 x ATR (mas conservador)
  Labels:          "SL: 12.5 pips"          "SL: $8.50"
  Alertas:         "@ 1.0850"              "@ $2,145.30"
```

**Por que 1.5x ATR para Oro?**
El oro tiene una volatilidad intradia significativamente mayor que los pares forex. Un multiplicador de 1.2x resultaria en stop-losses demasiado ajustados que serian barridos por el ruido normal del precio. El 1.5x proporciona el colchon necesario para la accion de precio tipica del gold.

---

## 📊 Tabla Comparativa Completa

```
┌─────────────────┬───────────┬───────────┬───────────┬───────────┐
│    PARAMETRO     │  EUR/USD  │  JPY v3   │  JPY v4   │  XAU/USD  │
│                  │   v3 FVG  │  Fixed    │   FVG     │  v3 FVG   │
├─────────────────┼───────────┼───────────┼───────────┼───────────┤
│ FVG Support     │    ✅     │    ❌     │    ✅     │    ✅     │
│ Confluencias    │    8      │    7      │    8      │    8      │
│ Tokyo KZ        │    ❌     │    ✅     │    ✅     │    ❌     │
│ Spread          │  0.8 pip  │  1.5 pip  │  1.5 pip  │   $3.0    │
│ ATR Mult.       │   1.2x    │   1.2x    │   1.2x    │   1.5x    │
│ Pip Value       │  0.0001   │   0.01    │   0.01    │    N/A    │
│ FVG Min Size    │  0.03%    │    N/A    │  0.03%    │   0.15%   │
│ SL/TP Unit      │   Pips    │   Pips    │   Pips    │  Dolares  │
│ Sweep Filter    │  Simple   │ Avanzado  │ Avanzado  │  Simple   │
│ Panel Rows      │    13     │    12     │    14     │    13     │
│ Kill Zones      │  LDN, NY  │ TK,LDN,NY│ TK,LDN,NY│  LDN, NY  │
│ OB Threshold    │  0.3 ATR  │  0.3 ATR  │  0.3 ATR  │  0.5 ATR  │
└─────────────────┴───────────┴───────────┴───────────┴───────────┘
```

---

## 🚀 Guia de Instalacion en TradingView

### Paso 1 — Abrir Pine Script Editor

```
TradingView  →  Abrir cualquier grafico  →  Parte inferior de la pantalla
                                              │
                                              ▼
                                    Click en "Pine Editor"
                                    (icono de codigo { } )
```

1. Abre [TradingView](https://www.tradingview.com) e inicia sesion
2. Abre un grafico del par que deseas operar (ej: EURUSD)
3. En la barra inferior, haz click en **"Pine Editor"** o el icono `</>`

---

### Paso 2 — Copiar el Script

```
  📁 Este repositorio
  │
  ├── SMS_EURUSD_v3_FVG.pine    ← Para EUR/USD
  ├── SMS_JPY_v3_Fixed.pine      ← Para USD/JPY (sin FVG)
  ├── SMS_USDJPY_v4_FVG.pine     ← Para USD/JPY (con FVG) ⭐ Recomendado
  └── SMS_XAUUSD_v3_FVG.pine     ← Para XAU/USD (Oro)
```

1. Abre el archivo `.pine` correspondiente al par que quieres operar
2. Selecciona **TODO** el contenido del archivo (`Ctrl + A`)
3. Copia el contenido (`Ctrl + C`)

---

### Paso 3 — Pegar en Pine Editor

```
  ┌──────────────────────────────────────────────────────────┐
  │  Pine Editor                                    [x]      │
  ├──────────────────────────────────────────────────────────┤
  │                                                          │
  │  1│ // Borra todo el contenido que haya aqui             │
  │  2│ // y pega el script copiado                          │
  │  3│                                                      │
  │   │  Ctrl + A  (seleccionar todo lo existente)           │
  │   │  Ctrl + V  (pegar el nuevo script)                   │
  │                                                          │
  └──────────────────────────────────────────────────────────┘
```

1. En el Pine Editor, selecciona todo el texto existente (`Ctrl + A`)
2. Pega el script copiado (`Ctrl + V`)

---

### Paso 4 — Guardar y Agregar al Grafico

```
  ┌─────────────────────────────────────────────────────────────┐
  │  Pine Editor                                                │
  │                                                             │
  │  [💾 Guardar]    [▶ Anadir al grafico]    [📋 ...]         │
  │                                                             │
  │   Paso 4a: Click "Guardar" (o Ctrl+S)                      │
  │   Paso 4b: Click "Anadir al grafico"                       │
  └─────────────────────────────────────────────────────────────┘
                          │
                          ▼
              ✅ El indicador aparece en el grafico
              con todos los elementos visuales activos
```

1. Haz click en **"Guardar"** (icono de disquete o `Ctrl + S`)
2. Asignale un nombre descriptivo (ej: "SMS Pro EURUSD v3")
3. Haz click en **"Anadir al grafico"** (boton con icono ▶)

---

### Paso 5 — Configurar el Timeframe Correcto

```
  ⚠️  IMPORTANTE: Estos indicadores estan optimizados para SCALPING

  Timeframes recomendados:

  ┌─────────────────────────────────────────────────┐
  │                                                 │
  │   ⭐ 1 minuto  (M1)  — Precision maxima        │
  │   ⭐ 3 minutos (M3)  — Balance precision/ruido │
  │   ✅ 5 minutos (M5)  — Menos ruido             │
  │   ✅ 15 minutos(M15) — Scalping conservador    │
  │   ⚠️ 1 hora   (H1)  — No recomendado          │
  │   ❌ Diario   (D1)  — No usar                  │
  │                                                 │
  └─────────────────────────────────────────────────┘
```

---

### Paso 6 — Ajustar Configuracion (Gear Icon ⚙️)

```
  Click en el nombre del indicador en el grafico
         │
         ▼
    ⚙️ Icono de engranaje  →  Se abre panel de configuracion
         │
         ▼
  ┌──────────────────────────────────────────────────────┐
  │  Configuracion del Indicador                         │
  ├──────────────────────────────────────────────────────┤
  │                                                      │
  │  📂 EMAs                                             │
  │     EMA Rapida .......... [9]                        │
  │     EMA Lenta ........... [21]                       │
  │     EMA 200 ............. [200]                      │
  │     Mostrar EMA 200 ..... [✅]                       │
  │                                                      │
  │  📂 Structure                                        │
  │     Swing Lookback ...... [5]                        │
  │     Mostrar BOS ......... [✅]                       │
  │     Mostrar CHoCH ....... [✅]                       │
  │                                                      │
  │  📂 Order Blocks                                     │
  │     Mostrar OB .......... [✅]                       │
  │     Max OB visibles ..... [3]                        │
  │                                                      │
  │  📂 FVG                                              │
  │     Mostrar FVG ......... [✅]                       │
  │     Tamano minimo % ..... [0.03]                     │
  │     Max FVG visibles .... [3]                        │
  │     Usar como Confluencia [✅]                       │
  │                                                      │
  │  📂 Liquidez                                         │
  │     Mostrar Sweeps ...... [✅]                       │
  │     Filtrar en KZ ....... [❌]                       │
  │                                                      │
  │  📂 Kill Zones                                       │
  │     Mostrar KZ .......... [✅]                       │
  │     Solo senales en KZ .. [❌]                       │
  │                                                      │
  │  📂 Senales                                          │
  │     Min Confluencias .... [3]                        │
  │     Mostrar Labels ...... [✅]                       │
  │                                                      │
  │  📂 Risk Management                                  │
  │     ATR Period .......... [14]                       │
  │     SL Multiplier ....... [1.2]                      │
  │     Risk:Reward ......... [2.0]                      │
  │     Spread .............. [0.8]                       │
  │     Usar OB como SL ..... [✅]                       │
  │                                                      │
  └──────────────────────────────────────────────────────┘
```

---

### Paso 7 — Configurar Alertas

```
  En TradingView:

  1.  Click en el icono de 🔔 (campana) en la barra superior
  2.  O click derecho en el grafico → "Agregar alerta"

  ┌──────────────────────────────────────────────────────────┐
  │  Crear Alerta                                            │
  ├──────────────────────────────────────────────────────────┤
  │                                                          │
  │  Condicion:  SMS Pro EURUSD v3                           │
  │              │                                           │
  │              ├── 🟢 LONG Signal     ← Senal de compra   │
  │              ├── 🔴 SHORT Signal    ← Senal de venta    │
  │              ├── 🔄 CHoCH Bullish   ← Cambio a alcista  │
  │              ├── 🔄 CHoCH Bearish   ← Cambio a bajista  │
  │              ├── 📊 BOS Bullish     ← Quiebre alcista   │
  │              ├── 📊 BOS Bearish     ← Quiebre bajista   │
  │              ├── 💧 Sweep Bullish   ← Barrida alcista   │
  │              └── 💧 Sweep Bearish   ← Barrida bajista   │
  │                                                          │
  │  Frecuencia: "Una vez por cierre de barra"               │
  │  Expiracion: Configurar segun tu plan                    │
  │                                                          │
  │  Notificaciones:                                         │
  │     [✅] Popup en pantalla                               │
  │     [✅] Notificacion push (app movil)                   │
  │     [  ] Email                                           │
  │     [  ] Webhook (para bots/automatizacion)              │
  │                                                          │
  └──────────────────────────────────────────────────────────┘
```

**Ejemplo de mensaje de alerta recibido:**

```
🟢 LONG 5/8 +FVG
Entry: 1.08520
SL: 1.08410 (11.0 pips) [OB]
TP: 1.08740 (22.0 pips)
ATR: 6.2 pips | KZ: London
```

---

## 🎯 Sistema de Confluencias

El motor del sistema requiere un minimo de confluencias alineadas antes de generar una senal. Esto reduce drasticamente las senales falsas.

```
  ┌────────────────────────────────────────────────────────────────┐
  │                    FLUJO DE DECISION                           │
  └────────────────────────────────────────────────────────────────┘

                         Mercado en tiempo real
                                │
                    ┌───────────┴───────────┐
                    ▼                       ▼
             ¿Tendencia UP?          ¿Tendencia DOWN?
              EMA 9 > 21              EMA 9 < 21
                    │                       │
                    ▼                       ▼
            +1 Confluencia           +1 Confluencia
                    │                       │
           ┌───────┴───────┐       ┌───────┴───────┐
           ▼               ▼       ▼               ▼
      ¿Close>EMA200?  ¿En OB?  ¿Close<EMA200? ¿En OB?
           │               │       │               │
           ▼               ▼       ▼               ▼
    +1 Confluencia  +1 Conflu. +1 Confluencia  +1 Conflu.
           │               │       │               │
           └───────┬───────┘       └───────┬───────┘
                   ▼                       ▼
           ¿Zona Discount?          ¿Zona Premium?
           ¿Patron alcista?         ¿Patron bajista?
           ¿Sweep en low?          ¿Sweep en high?
           ¿CHoCH/BOS bull?         ¿CHoCH/BOS bear?
           ¿Dentro de FVG?         ¿Dentro de FVG?
                   │                       │
                   ▼                       ▼
           Sumar todas las          Sumar todas las
           confluencias             confluencias
                   │                       │
                   ▼                       ▼
          ┌────────────────┐      ┌────────────────┐
          │ ¿>= Minimo(3)? │      │ ¿>= Minimo(3)? │
          └───────┬────────┘      └───────┬────────┘
                  │                       │
           ┌──YES─┴─NO──┐          ┌──YES─┴─NO──┐
           ▼             ▼          ▼             ▼
     ¿Confirmacion?   Ignorar  ¿Confirmacion?  Ignorar
     ¿Vela de                  ¿Vela de
      continuacion?             continuacion?
           │                       │
           ▼                       ▼
    🟢 SENAL LONG            🔴 SENAL SHORT
    con SL + TP              con SL + TP
```

---

## 🛡️ Gestion de Riesgo

Cada senal incluye Stop-Loss y Take-Profit calculados automaticamente:

### Metodo de Stop-Loss

```
  ┌──────────────────────────────────────────────────┐
  │            CALCULO DEL STOP-LOSS                  │
  ├──────────────────────────────────────────────────┤
  │                                                  │
  │  Metodo 1: ATR (por defecto)                     │
  │  ──────────────────────────                      │
  │  SL = Entry ± (ATR × Multiplicador + Spread)    │
  │                                                  │
  │  Ejemplo LONG EUR/USD:                           │
  │  Entry    = 1.08500                              │
  │  ATR(14)  = 0.00052 (5.2 pips)                   │
  │  SL       = 1.08500 - (0.00052 × 1.2 + 0.00011) │
  │  SL       = 1.08500 - 0.00073                    │
  │  SL       = 1.08427  (7.3 pips de riesgo)        │
  │                                                  │
  │  Metodo 2: Order Block (si habilitado)           │
  │  ──────────────────────────────                  │
  │  SL = Fondo del OB mas cercano + Spread         │
  │  (Provee un SL basado en estructura real)        │
  │                                                  │
  ├──────────────────────────────────────────────────┤
  │            CALCULO DEL TAKE-PROFIT               │
  ├──────────────────────────────────────────────────┤
  │                                                  │
  │  TP = Entry + (Distancia SL × Risk:Reward)       │
  │                                                  │
  │  Ejemplo (R:R = 2:1):                            │
  │  Riesgo = 7.3 pips                               │
  │  TP     = 1.08500 + (0.00073 × 2.0)             │
  │  TP     = 1.08500 + 0.00146                      │
  │  TP     = 1.08646  (14.6 pips de ganancia)       │
  │                                                  │
  └──────────────────────────────────────────────────┘
```

---

## 🔔 Alertas

Cada script tiene **8 condiciones de alerta** configurables:

| Alerta | Descripcion | Uso Recomendado |
|--------|-------------|-----------------|
| 🟢 LONG Signal | Senal de compra confirmada | **Principal** — Notificacion push |
| 🔴 SHORT Signal | Senal de venta confirmada | **Principal** — Notificacion push |
| 🔄 CHoCH Bullish | Cambio de caracter alcista | Contexto — Cambio de tendencia |
| 🔄 CHoCH Bearish | Cambio de caracter bajista | Contexto — Cambio de tendencia |
| 📊 BOS Bullish | Break of Structure alcista | Opcional — Confirmacion de tendencia |
| 📊 BOS Bearish | Break of Structure bajista | Opcional — Confirmacion de tendencia |
| 💧 Sweep Bullish | Barrida de liquidez en lows | Avanzado — Posible reversal |
| 💧 Sweep Bearish | Barrida de liquidez en highs | Avanzado — Posible reversal |

---

## 📐 Elementos Visuales en el Grafico

```
  Precio
    │
    │         ┌─────────┐
    │         │ FVG Bear │ ← Caja naranja semi-transparente
    │         │ (orange) │
    │  ───────┴─────────┴───────  ← EMA 21 (roja)
    │
    │    ▼ SHORT 4/8                ← Label rojo (senal de venta)
    │    SL: 1.0865 (8.5p) [ATR]
    │    TP: 1.0830 (17.0p)
    │
    │  ════════════════════════  ← EMA 9 (verde)
    │
    │     [CHoCH ▼]                 ← Label de cambio de estructura
    │
    │  ┌──────────┐
    │  │  OB Bull  │ ← Caja verde semi-transparente
    │  │  (green)  │
    │  └──────────┘
    │         ┌─────────┐
    │         │ FVG Bull │ ← Caja azul semi-transparente
    │         │  (blue)  │
    │         └─────────┘
    │
    │    ▲ LONG 5/8 +FVG            ← Label verde (senal de compra)
    │    SL: 1.0810 (6.2p) [OB]
    │    TP: 1.0835 (12.4p)
    │
    │     SW ▲                      ← Label de liquidity sweep
    │
    │  ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─  ← Fibonacci 50% (blanca punteada)
    │
    │  ════════════════════════════  ← EMA 200 (blanca)
    │
    └──────────────────────────────────── Tiempo

    ░░░░░░░░░░░░░  ← Fondo azul: London Kill Zone
              ░░░░░░░░░░░░░  ← Fondo verde: NY Kill Zone
```

---

## ⚡ Guia Rapida por Instrumento

### Si operas EUR/USD:
```
1. Usa:  SMS_EURUSD_v3_FVG.pine
2. TF:   M1 - M5
3. KZ:   London (02-05 EST) y NY (07-10 EST)
4. Tip:  El EUR/USD tiene spreads bajos, ideal para scalping agresivo
         Mantener min confluencias en 3-4 para mas senales
```

### Si operas USD/JPY:
```
1. Usa:  SMS_USDJPY_v4_FVG.pine  (recomendado sobre v3)
2. TF:   M1 - M5
3. KZ:   Tokyo (19-02 EST), London (02-05 EST), NY (07-10 EST)
4. Tip:  Activar el filtro de Tokyo Kill Zone para la sesion asiatica
         USD/JPY responde muy bien a las sesiones de Tokyo y NY
```

### Si operas XAU/USD (Oro):
```
1. Usa:  SMS_XAUUSD_v3_FVG.pine
2. TF:   M3 - M15 (el oro es mas volatil, menos ruido en TF mayores)
3. KZ:   London (02-05 EST) y NY (07-10 EST)
4. Tip:  El oro requiere stops mas amplios — el ATR mult ya esta en 1.5x
         Considerar subir min confluencias a 4 para filtrar senales debiles
         Los mejores movimientos del oro ocurren en la apertura de NY
```

---

## 🔧 Consejos de Configuracion Avanzada

### Modo Conservador (menos senales, mayor calidad)
```
  Min Confluencias:    5
  Solo senales en KZ:  ✅ Activado
  Usar OB como SL:     ✅ Activado
  Risk:Reward:          2.5 o 3.0
```

### Modo Agresivo (mas senales, requiere mas experiencia)
```
  Min Confluencias:    3
  Solo senales en KZ:  ❌ Desactivado
  Usar OB como SL:     ❌ Desactivado (usa ATR)
  Risk:Reward:          1.5 o 2.0
```

### Para Backtesting Visual
```
  Mostrar BOS:         ✅
  Mostrar CHoCH:       ✅
  Mostrar OB:          ✅
  Mostrar FVG:         ✅
  Mostrar Sweeps:      ✅
  Mostrar KZ:          ✅
  Mostrar Labels:      ✅
  (Activar todo para analizar el comportamiento historico)
```

---

## ⚠️ Disclaimer

> **Estos indicadores son herramientas de analisis tecnico, NO sistemas automaticos de trading.**
>
> - No garantizan ganancias ni resultados especificos
> - El trading de forex y commodities conlleva un alto riesgo de perdida
> - Siempre opera con capital que puedas permitirte perder
> - Se recomienda practicar en cuenta demo antes de operar en real
> - Los rendimientos pasados no garantizan resultados futuros
> - Cada trader es responsable de sus propias decisiones de inversion

---

<p align="center">
  <strong>SMS Pro — Smart Money Scalper</strong><br>
  <em>Pine Script v6 | TradingView | Scalping System</em><br><br>
  Desarrollado con conceptos de Smart Money / ICT
</p>
