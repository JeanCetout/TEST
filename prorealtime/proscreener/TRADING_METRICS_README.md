# ProScreener : M\u00e9triques de Qualit\u00e9 de Trading

## Description

Ce script ProScreener calcule automatiquement plusieurs m\u00e9triques importantes pour \u00e9valuer la qualit\u00e9 d'un instrument financier pour le trading intraday. Il g\u00e9n\u00e8re un **score de qualit\u00e9** de 0 \u00e0 10 bas\u00e9 sur diff\u00e9rents crit\u00e8res techniques.

## M\u00e9triques Calcul\u00e9es

### 1. **Volume / M\u00e9diane** (Vol/Med)
- **Calcul** : Ratio entre le volume actuel et la m\u00e9diane du volume sur 100 p\u00e9riodes
- **Interpr\u00e9tation** :
  - `> 1.0` : Volume sup\u00e9rieur \u00e0 la normale (bon signe)
  - `> 1.5` : Volume \u00e9lev\u00e9 (excellent pour le trading)
  - `< 0.5` : Volume faible (\u00e0 \u00e9viter)
- **Points** : +1 si \u2265 1.0, +1 bonus si \u2265 1.5

### 2. **Spread Ratio** (Spread%)
- **Calcul** : `(High - Low) / Close × 100`
- **Approximation** : Repr\u00e9sente la volatilit\u00e9 de la bougie en % du prix
- **Interpr\u00e9tation** :
  - Plus faible que la moyenne = co\u00fbts de transaction r\u00e9duits
  - Valeur typique : 0.1% - 1% selon l'actif
- **Points** : +1 si inf\u00e9rieur \u00e0 la moyenne
- **\u26a0\ufe0f Limitation** : Ce n'est PAS le spread bid/ask r\u00e9el (non disponible dans ProRealTime)

### 3. **ATR / M\u00e9diane** (ATR/Med)
- **Calcul** : ATR(14) divis\u00e9 par la m\u00e9diane de l'ATR
- **Interpr\u00e9tation** :
  - `~ 1.0` : Volatilit\u00e9 normale
  - `> 1.5` : Volatilit\u00e9 \u00e9lev\u00e9e (risque accru)
  - `< 0.5` : Volatilit\u00e9 faible (mouvements limit\u00e9s)
- **Points** : +1 si entre 0.8 et 1.2 (volatilit\u00e9 stable)

### 4. **Ratio Corps / M\u00e8che** (Corps%)
- **Calcul** : `|Close - Open| / (High - Low) × 100`
- **Interpr\u00e9tation** :
  - `> 70%` : Corps fort, conviction directionnelle
  - `50-70%` : Corps moyen
  - `< 30%` : Indecision (doji, spinning top)
- **Points** : +1 si \u2265 50%

### 5. **Chevauchement Corps** (Chevauche%)
- **Calcul** : Pourcentage de chevauchement entre le corps actuel et le pr\u00e9c\u00e9dent
- **Interpr\u00e9tation** :
  - `30-70%` : Continuation saine
  - `> 90%` : Consolidation forte
  - `< 10%` : Gap ou mouvement explosif
- **Points** : +1 si entre 30% et 70%

### 6. **Run Directionnel** (Run)
- **Calcul** : Nombre de bougies cons\u00e9cutives dans la m\u00eame direction (max 10)
- **Interpr\u00e9tation** :
  - `\u2265 3` : Tendance claire en cours
  - `1-2` : Pas de tendance nette
  - `0` : Bougie doji (close = open)
- **Points** : +1 si \u2265 3

### 7. **Distance au VWAP** (VWAP%)
- **Calcul** : `(Close - VWAP) / VWAP × 100`
- **Interpr\u00e9tation** :
  - `> 0` : Prix au-dessus du VWAP (force acheteuse)
  - `< 0` : Prix en-dessous du VWAP (force vendeuse)
  - Proche de 0 (\u00b10.5%) : Respecte le VWAP (bon signe)
- **Points** : +1 si \u00e0 \u00b10.5% du VWAP

### 8. **Slippage / ATR** (Slip/ATR)
- **Calcul** : Approximation du slippage potentiel comme ratio du spread sur l'ATR
- **Interpr\u00e9tation** :
  - `< 0.05` : Slippage tr\u00e8s faible
  - `0.05-0.1` : Slippage acceptable
  - `> 0.1` : Slippage potentiellement \u00e9lev\u00e9
- **Points** : +1 si < 0.1
- **\u26a0\ufe0f Limitation** : Approximation bas\u00e9e sur le spread, pas le slippage r\u00e9el

### 9. **Flux R\u00e9gulier** (Bonus)
- **Calcul** : Coefficient de variation du volume (StdDev / Moyenne)
- **Interpr\u00e9tation** :
  - `< 0.5` : Volume r\u00e9gulier et pr\u00e9visible
  - `> 1.0` : Volume erratique
- **Points** : +1 si < 0.5

### 10. **Score de Qualit\u00e9 Global** (Score)
- **Calcul** : Somme des points (maximum 10)
- **Interpr\u00e9tation** :
  - `8-10` : Excellente qualit\u00e9 de trading
  - `6-7` : Bonne qualit\u00e9
  - `4-5` : Qualit\u00e9 moyenne
  - `0-3` : Qualit\u00e9 faible (\u00e0 \u00e9viter)

## Installation et Utilisation

### \u00c9tape 1 : Cr\u00e9er le ProScreener

1. Ouvrez **ProRealTime**
2. Allez dans **Outils** → **ProScreener**
3. Cliquez sur **Nouveau Screener**
4. Nommez-le "M\u00e9triques Qualit\u00e9 Trading"

### \u00c9tape 2 : Copier le Code

1. Ouvrez le fichier `trading_quality_metrics.prt`
2. **Copiez TOUT le contenu**
3. **Collez-le** dans l'\u00e9diteur de code du screener

### \u00c9tape 3 : Configuration Recommand\u00e9e

**Pour le trading intraday 1 minute :**
```
lookbackPeriod = 100
atrPeriod = 14
minBodyRatio = 0.5
minVolRatio = 1.0
```

**Pour le trading 5 minutes :**
```
lookbackPeriod = 200
atrPeriod = 14
minBodyRatio = 0.4
minVolRatio = 0.8
```

**Pour le trading 15 minutes :**
```
lookbackPeriod = 300
atrPeriod = 20
minBodyRatio = 0.3
minVolRatio = 0.7
```

### \u00c9tape 4 : Lancer le Screener

1. S\u00e9lectionnez votre **liste d'instruments** (watchlist)
2. Choisissez l'**unit\u00e9 de temps** (1 min recommand\u00e9)
3. Cliquez sur **Lancer**

## Interpr\u00e9tation des R\u00e9sultats

### Exemple de R\u00e9sultat

| Instrument | Score | Vol/Med | Spread% | ATR/Med | Corps% | Chevauche% | Run | VWAP% | Slip/ATR |
|-----------|-------|---------|---------|---------|--------|------------|-----|-------|----------|
| AAPL      | 8     | 2.1     | 0.12    | 1.05    | 75     | 45         | 4   | 0.2   | 0.04     |
| TSLA      | 6     | 1.8     | 0.35    | 1.45    | 65     | 55         | 3   | -0.8  | 0.08     |
| SPY       | 4     | 0.6     | 0.08    | 0.85    | 40     | 85         | 1   | 0.05  | 0.02     |

**Analyse :**

**AAPL (Score 8/10)** - Excellente qualit\u00e9 ✅
- Volume 2x la m\u00e9diane : tr\u00e8s liquide
- Spread faible : co\u00fbts r\u00e9duits
- Run de 4 : tendance claire
- Proche VWAP : prix \u00e9quilibr\u00e9
- **Action** : Excellent candidat pour un trade

**TSLA (Score 6/10)** - Bonne qualit\u00e9 \u26a0\ufe0f
- Volume bon mais spread \u00e9lev\u00e9
- ATR au-dessus de la m\u00e9diane : volatil
- \u00c9loign\u00e9 du VWAP
- **Action** : Tradable mais avec prudence (stops plus larges)

**SPY (Score 4/10)** - Qualit\u00e9 moyenne \u274c
- Volume faible : peu d'int\u00e9r\u00eat
- Pas de run directionnel
- Beaucoup de chevauchement : consolidation
- **Action** : Attendre un meilleur setup

## Strat\u00e9gies d'Utilisation

### Strat\u00e9gie 1 : Filtre de Qualit\u00e9

**Objectif** : S\u00e9lectionner uniquement les meilleurs instruments

1. Lancez le screener toutes les 15-30 minutes
2. Ne tradez QUE les instruments avec **Score \u2265 7**
3. V\u00e9rifiez que :
   - `Vol/Med \u2265 1.5` (liquidit\u00e9)
   - `Run \u2265 3` (tendance)
   - `Spread% < 0.2` (co\u00fbts faibles)

### Strat\u00e9gie 2 : Signal Haussier

**Conditions** :
- Score \u2265 7
- Run haussier \u2265 3
- VWAP% > 0 (prix au-dessus du VWAP)
- Corps% > 70 (conviction)

**Setup** :
- Entr\u00e9e : Breakout du high de la derni\u00e8re bougie
- Stop-loss : Sous le VWAP ou le low de la bougie
- Target : 2x l'ATR

### Strat\u00e9gie 3 : Signal Baissier

**Conditions** :
- Score \u2265 7
- Run baissier \u2265 3
- VWAP% < 0 (prix en-dessous du VWAP)
- Corps% > 70 (conviction)

**Setup** :
- Entr\u00e9e : Breakdown du low de la derni\u00e8re bougie
- Stop-loss : Au-dessus du VWAP ou du high de la bougie
- Target : 2x l'ATR

### Strat\u00e9gie 4 : Retour au VWAP

**Conditions** :
- Score \u2265 6
- VWAP% entre 1% et 3% (extension)
- Corps% < 30 (indecision)

**Setup** :
- Entr\u00e9e : Quand le prix revient vers le VWAP
- Stop-loss : Au-del\u00e0 de l'extension (ATR)
- Target : Le VWAP

## Limitations et Avertissements

### \u26a0\ufe0f Donn\u00e9es NON Disponibles dans ProRealTime

Les m\u00e9triques suivantes **ne peuvent PAS** \u00eatre calcul\u00e9es avec pr\u00e9cision dans ProRealTime :

1. **Profondeur L2 (Carnet d'ordres)** - ProRealTime ne donne pas acc\u00e8s au Level 2
2. **Spread Bid/Ask r\u00e9el** - Le script utilise une approximation via High-Low
3. **Slippage r\u00e9el** - Approxim\u00e9 mais variable selon le broker
4. **Vitesse du flux en temps r\u00e9el** - Approxim\u00e9 par la r\u00e9gularit\u00e9 du volume
5. **Corr\u00e9lation secteur/indice en direct** - N\u00e9cessiterait des donn\u00e9es multi-instruments

### Solutions Alternatives

Pour ces donn\u00e9es, vous devez :
- **Profondeur L2** : Consulter votre plateforme de trading (Level 2 / Carnet)
- **Spread r\u00e9el** : V\u00e9rifier sur votre broker
- **Corr\u00e9lation** : Utiliser des graphiques s\u00e9par\u00e9s ou TradingView

### \u26a0\ufe0f Avertissements G\u00e9n\u00e9raux

- \u26a0\ufe0f **Aucun syst\u00e8me n'est parfait** : Le score ne garantit pas la rentabilit\u00e9
- \u26a0\ufe0f **Gestion du risque** : Ne risquez jamais plus de 1-2% par trade
- \u26a0\ufe0f **Backtest** : Testez sur historique avant utilisation r\u00e9elle
- \u26a0\ufe0f **Conditions de march\u00e9** : Moins efficace en p\u00e9riode de faible volatilit\u00e9
- \u26a0\ufe0f **Latence** : ProRealTime a un d\u00e9lai vs plateformes professionnelles

## Param\u00e8tres Avanc\u00e9s

### Pour des signaux STRICTS (moins de faux positifs) :

```javascript
lookbackPeriod = 200     // Plus de donn\u00e9es historiques
minBodyRatio = 0.7       // Corps tr\u00e8s forts uniquement
minVolRatio = 1.5        // Volume \u00e9lev\u00e9 requis
```

Dans le code, changez aussi :
```javascript
highQuality = qualityScore >= 8  // Au lieu de 7
```

### Pour PLUS de signaux (exploration) :

```javascript
lookbackPeriod = 50      // Analyse plus courte
minBodyRatio = 0.3       // Corps faibles accept\u00e9s
minVolRatio = 0.5        // Volume faible accept\u00e9
```

Dans le code :
```javascript
highQuality = qualityScore >= 5  // Au lieu de 7
```

## D\u00e9pannage

### Le screener ne retourne aucun r\u00e9sultat

**Solutions** :
1. R\u00e9duire `qualityScore >= 7` \u00e0 `qualityScore >= 5` (ligne 278)
2. R\u00e9duire `minVolRatio` \u00e0 `0.5`
3. Augmenter `lookbackPeriod` \u00e0 `200`
4. V\u00e9rifier que vous \u00eates sur une unit\u00e9 de temps avec assez de donn\u00e9es

### Trop de r\u00e9sultats

**Solutions** :
1. Augmenter `qualityScore >= 7` \u00e0 `qualityScore >= 8`
2. Augmenter `minVolRatio` \u00e0 `2.0`
3. Ajouter des filtres suppl\u00e9mentaires (voir strat\u00e9gies)

### Erreurs de syntaxe

**V\u00e9rifications** :
1. Tout le code a \u00e9t\u00e9 copi\u00e9 (du d\u00e9but \u00e0 la fin)
2. Pas de caract\u00e8res sp\u00e9ciaux alt\u00e9r\u00e9s
3. Version ProRealTime compatible (v11+)

### Le VWAP semble incorrect

**Cause** : Le VWAP se r\u00e9initialise chaque jour
- V\u00e9rifiez que vous avez assez de donn\u00e9es intraday
- Sur Forex, ajustez `vwapStart` pour l'heure d'ouverture de session

## Ressources Compl\u00e9mentaires

- [Documentation ProRealTime](https://www.prorealtime.com/fr/support)
- [ProRealCode Forum](https://www.prorealcode.com/)
- [Langage ProBuilder](https://www.prorealtime.com/fr/probuilder)

## Compatibilit\u00e9

- **Version ProRealTime** : v11.0+
- **Types d'instruments** : Actions, Indices, Forex, Crypto, Commodities
- **Unit\u00e9s de temps** : 1min, 5min, 15min, 1H (1min recommand\u00e9 pour ATR 1m)
- **Plateformes** : Premium, Ultimate (acc\u00e8s ProScreener requis)

## Support

Pour toute question ou am\u00e9lioration, consultez :
- Les forums ProRealCode
- La documentation officielle ProRealTime
- Les tutoriels ProBuilder

---

**\u26a0\ufe0f Disclaimer** : Ce script est fourni \u00e0 des fins \u00e9ducatives uniquement. Le trading comporte des risques. N'investissez que ce que vous pouvez vous permettre de perdre. Testez toujours vos strat\u00e9gies sur compte de d\u00e9monstration avant utilisation r\u00e9elle.

---

**Cr\u00e9\u00e9 pour ProRealTime v11+**
**Compatible avec toutes les unit\u00e9s de temps**
**Optimis\u00e9 pour le trading intraday 1 minute**
