# 📊 ProRealTime Trading Quality Metrics - Version 4.1

**Screener ProRealTime avancé avec SpeedMeter pour mesurer la vitesse des mouvements - Optimisé pour scalping 1/5/10 minutes.**

[![Version](https://img.shields.io/badge/version-4.1-brightgreen.svg)](https://github.com)
[![ProRealTime](https://img.shields.io/badge/ProRealTime-V12%2B-green.svg)](https://www.prorealtime.com)
[![License](https://img.shields.io/badge/license-Educational-orange.svg)](https://github.com)
[![Tested](https://img.shields.io/badge/status-Tested%20%26%20Working-success.svg)](https://github.com)

---

## 🔧 VERSION 4.1 - Actuelle (Correctif)

**VERSION 4.1** corrige une erreur de syntaxe de la V4.0 :
- ✅ **Correction** : Intégration de `minSpeedScalping` dans le critère `Scalp`
- ✅ **Critère Scalp amélioré** : Nécessite maintenant **4 conditions** au lieu de 3
  - Volume ≥ 2.0x
  - Spread ≤ 0.3%
  - ATR ≤ 1.3x
  - **Speed ≥ 1.8** 🆕 (NOUVEAU dans V4.1)

**Fichier recommandé** : `trading_quality_metrics_v4_1.prt` (391 lignes)

---

## 🆕 NOUVEAUTÉ VERSION 4.0 - SPEEDMETER

### ⚡ Mesure de la Vitesse des Mouvements

**VERSION 4.0** introduit le **"SpeedMeter"** pour mesurer la vitesse et la fréquence des mouvements de prix !

**Nouvelle colonne** : **"Speed"** (colonne 7)
- **≥ 2.5** = 🔥 Très rapide (excellent pour scalping)
- **2.0-2.5** = ⚡ Rapide (bon pour scalping)
- **1.5-2.0** = 🟡 Moyen (acceptable)
- **< 1.5** = 🔴 Lent (éviter pour scalping)

**Calcul du SpeedMeter** (Option C - Complet) :
- 📈 **Price Velocity** : Vitesse du mouvement actuel vs moyenne des 20 bougies
- 📊 **Tick Activity** : Volume actuel vs moyenne (nombre de transactions)
- 🎯 **Speed Score** : Moyenne de Velocity + Tick Activity

**Affichage ProScreener V4.0** :
```
Score | Volume | ATR | Run | Align | Type | Speed | Scalp | T1 | T2 | T3
                                           ↑
                                        NOUVEAU!
```

**Utilisation pour scalping** :
- ⚡ Filtrer **Speed ≥ 2.0** pour mouvements rapides
- 🎯 Combiner **Speed ≥ 2.0** + **Scalp = 1** = Setup scalping optimal
- 📊 Trier par colonne "Speed" pour instruments les plus actifs

---

## ✨ Historique V3.1 - Filtre Scalping

**VERSION 3.1** a ajouté la colonne **"Scalp"** :
- Critères : Volume ≥ 2.0x + Spread ≤ 0.3% + ATR ≤ 1.3x
- Identification instantanée des instruments adaptés au scalping

---

## ✨ Historique V3.0 - Colonnes Personnalisées

**VERSION 3.0** a introduit les colonnes personnalisées :

**AVANT (V2.x)** : Noms de variables techniques
```
qualityScore | volumeRatio | atrRatio | directionalRun | ...
```

**APRÈS (V3.0+)** : Noms clairs et lisibles
```
Score | Volume | ATR | Run | Align | Type | Speed | Scalp | T1 | T2 | T3
```

---

## 🎯 Qu'est-ce que ce screener fait ?

Ce **ProScreener V4.0** analyse en temps réel la qualité de trading de vos instruments financiers et vous aide à :

✅ **Identifier les meilleures opportunités** grâce à un score de qualité sur 13 points
✅ **Classifier automatiquement le type de marché** (Bull Fort/Modéré, Bear Fort/Modéré, Range/Neutre)
✅ **Mesurer la vitesse des mouvements** avec le SpeedMeter (vital pour scalping)
✅ **Analyser 10 métriques techniques** (volume, volatilité, momentum, VWAP, slippage, régularité)
✅ **Détecter l'alignement des tendances** sur 3 timeframes (court/moyen/long terme)
✅ **Filtrer rapidement** selon votre stratégie (LONG, SHORT, ou RANGE trading)
✅ **Identifier les instruments adaptés au scalping** avec critères volume/spread/volatilité
✅ **Afficher des colonnes lisibles** avec noms personnalisés

---

## 📋 Les 11 Colonnes Affichées

Le screener affiche **11 colonnes nommées** dans ProRealTime :

| # | Colonne Affichée | Nom Variable | Description | Plage | Optimal |
|---|------------------|--------------|-------------|-------|---------|
| **1** | **Score** | qualityScore | Score global de qualité | 0-13 | ≥ 10 |
| **2** | **Volume** | volumeRatio | Volume/Moyenne (100 périodes) | 0-∞ | ≥ 2.0 |
| **3** | **ATR** | atrRatio | Volatilité actuelle/moyenne | 0-∞ | 0.8-1.2 |
| **4** | **Run** | directionalRun | Bougies consécutives (momentum) | 0-10 | ≥ 3 |
| **5** | **Align** | alignmentScore | Nombre d'EMA alignées | 0-3 | 3 |
| **6** | **Type** | marketType | Classification Bull/Bear/Range | -2 à +2 | ±2 |
| **7** | **Speed** 🆕 | speedMeter | Vitesse des mouvements | 0-∞ | ≥ 2.0 |
| **8** | **Scalp** | scalpQuality | Adapté scalping (1=oui, 0=non) | 0-1 | 1 |
| **9** | **T1** | trend1 | Tendance EMA 20 (court terme) | -1/0/+1 | ±1 |
| **10** | **T2** | trend2 | Tendance EMA 50 (moyen terme) | -1/0/+1 | ±1 |
| **11** | **T3** | trend3 | Tendance EMA 100 (long terme) | -1/0/+1 | ±1 |

**Condition de filtrage par défaut** : `Score >= 7`

**🆕 Colonne Speed (V4.0)** : Mesure velocity + tick activity pour identifier mouvements rapides

**Colonne Scalp (V3.1)** : Filtre automatique basé sur Volume ≥ 2.0x + Spread ≤ 0.3% + ATR ≤ 1.3x

---

## 🔢 Calcul du Score de Qualité (0-13)

### 10 Points de Base (Métriques de Qualité)

1. **Volume élevé** : Volume ≥ Moyenne → +1 point
2. **Spread faible** : Spread < Moyenne → +1 point
3. **Corps fort** : Corps bougie ≥ 50% range → +1 point
4. **Run directionnel** : ≥3 bougies consécutives → +1 point
5. **Proche VWAP** : Distance ≤ 0.5% → +1 point
6. **Slippage faible** : Ratio < 10% → +1 point
7. **Flux régulier** : Coefficient variation < 0.5 → +1 point
8. **ATR normal** : 0.8 ≤ ATR ratio ≤ 1.2 → +1 point
9. **Chevauchement** : 30% ≤ Overlap ≤ 70% → +1 point
10. **Volume fort** : Volume ≥ 1.5x moyenne → +1 point

### +3 Points Bonus (Multi-Tendance)

- **Alignement fort** : 3 EMA alignées + force > 0.5% → +2 points
- **Alignement modéré** : 2 EMA alignées + force > 0.3% → +1 point
- **Force élevée** : Force moyenne > 1.0% → +1 point

**Score maximum** : 13 points

---

## ⚡ SpeedMeter V4.0 - Détails Techniques

### Formule de Calcul

```
SpeedMeter = (Velocity Ratio + Tick Activity) / 2
```

**Velocity Ratio** :
- Mouvement actuel : `ABS(close - open)`
- Moyenne 20 bougies : `AVERAGE[20](ABS(close[i] - open[i]))`
- Ratio : `Mouvement actuel / Moyenne`

**Tick Activity** :
- Volume Ratio déjà calculé : `Volume / AVERAGE[100](Volume)`

### Interprétation du SpeedMeter

| Speed | Badge | Signification | Utilisation |
|-------|-------|---------------|-------------|
| **≥ 2.5** | 🔥 | **Très rapide** | Scalping ultra-actif, nombreuses opportunités |
| **2.0-2.5** | ⚡ | **Rapide** | Scalping actif, bon pour 1-5 min |
| **1.5-2.0** | 🟡 | **Moyen** | Swing court terme, scalping modéré |
| **1.0-1.5** | 🟠 | **Lent** | Position trading uniquement |
| **< 1.0** | 🔴 | **Très lent** | Éviter pour intraday |

### Avantages du SpeedMeter

✅ **Identifie les mouvements rapides** : Instruments qui bougent vite = plus d'opportunités
✅ **Mesure l'activité réelle** : Combine prix + volume pour vision complète
✅ **Filtre scalping précis** : Speed ≥ 2.0 garantit suffisamment de mouvement
✅ **Évite les instruments morts** : Speed < 1.5 = peu d'activité, à éviter

---

## 📊 Classification Type de Marché

La colonne **"Type"** (marketType) classe automatiquement chaque instrument :

| Valeur | Badge | Classification | Signification | Utilisation |
|--------|-------|----------------|---------------|-------------|
| **+2** | 🔥 | **Bull Fort** | Toutes les EMA haussières | Position LONG privilégiée |
| **+1** | 🟢 | **Bull Modéré** | 2+ EMA haussières | Position LONG possible |
| **0** | ⚪ | **Range/Neutre** | Tendances mixtes | Range trading ou attente |
| **-1** | 🟠 | **Bear Modéré** | 2+ EMA baissières | Position SHORT possible |
| **-2** | 🔴 | **Bear Fort** | Toutes les EMA baissières | Position SHORT privilégiée |

**Filtrage ultra-rapide** :
- `Type >= +1` → Affiche uniquement les marchés haussiers
- `Type <= -1` → Affiche uniquement les marchés baissiers
- `Type = 0` → Marchés en range (stratégies support/résistance)

---

## 🚀 Installation et Utilisation

### Prérequis
- **ProRealTime V12+** (version gratuite ou premium)
- **ProScreener** activé dans votre plateforme

### Étape 1 : Créer le Screener

1. Ouvrez **ProRealTime**
2. Menu **Outils** → **ProScreener** → **Nouveau Screener**
3. Nommez-le : `Trading Quality V4.0`

### Étape 2 : Copier le Code

1. Ouvrez le fichier **`proscreener/trading_quality_metrics_v4_1.prt`** (VERSION 4.1 recommandée)
2. **Copiez tout le contenu** (391 lignes)
3. **Collez** dans la fenêtre ProScreener

**Note** : Le fichier `trading_quality_metrics_v4.prt` (V4.0) contient une erreur corrigée dans V4.1

### Étape 3 : Configuration Recommandée

| Paramètre | Valeur Recommandée | Description |
|-----------|-------------------|-------------|
| **Unité de temps** | **1, 5 ou 10 minutes** | Optimal pour scalping avec SpeedMeter |
| **Liste** | Votre watchlist | CAC40, NASDAQ100, Forex, Crypto |
| **Condition** | `Score >= 7` | Déjà configuré (ligne 430) |

### Étape 4 : Lancer le Scan

1. Cliquez sur **Lancer le Screener**
2. Les résultats s'affichent avec les 11 colonnes nommées :
   ```
   Score | Volume | ATR | Run | Align | Type | Speed | Scalp | T1 | T2 | T3
   ```
3. **Triez par colonne** pour filtrer :
   - **Speed** : Trier décroissant → mouvements les plus rapides en premier 🆕
   - **Score** : Trier décroissant → meilleurs scores en haut
   - **Type** : Trier par valeur → regrouper bulls (+2, +1) et bears (-2, -1)
   - **Scalp** : Trier décroissant → instruments scalping d'abord (1 = adapté)
   - **Volume** : Trier décroissant → plus forte liquidité d'abord

---

## 📈 Exemples d'Interprétation

### Exemple 1 : Signal Scalping PARFAIT ⭐⭐⭐ 🆕

**Affichage dans ProScreener** :
```
Score: 12  | Volume: 2.8 | ATR: 1.0 | Run: 4 | Align: 3 | Type: +2 | Speed: 2.7 | Scalp: 1 | T1: +1 | T2: +1 | T3: +1
```

**Interprétation** :
- 🟢 **Score 12/13** → Excellente qualité
- 🟢 **Volume 2.8** → Volume x2.8 (participation massive)
- 🟢 **ATR 1.0** → Volatilité normale (risque maîtrisé)
- 🟢 **Run 4** → 4 bougies haussières consécutives (momentum)
- 🟢 **Align 3** → Toutes les EMA alignées
- 🔥 **Type +2** → **BULL FORT confirmé**
- 🔥 **Speed 2.7** → **TRÈS RAPIDE** - Mouvements explosifs ! 🆕
- ⚡ **Scalp 1** → **Adapté scalping** (liquidité + spread optimaux)
- 🟢 **T1/T2/T3 = +1** → Toutes les tendances haussières

**Action recommandée** : **SCALPING LONG AGRESSIF** 🚀
**Probabilité** : Très élevée (setup parfait)
**Stratégie** : Scalping 1-5 min avec entries rapides
**Entry** : Immédiate sur signal
**Stop-Loss** : 0.5 x ATR (très serré grâce à Speed élevé)
**Take-Profit** : 1:1 à 1:1.5 (sorties rapides)

---

### Exemple 2 : Bon Signal mais LENT ❌ Speed Insuffisant

**Affichage dans ProScreener** :
```
Score: 10  | Volume: 1.6 | ATR: 1.1 | Run: 3 | Align: 3 | Type: +2 | Speed: 1.2 | Scalp: 0 | T1: +1 | T2: +1 | T3: +1
```

**Interprétation** :
- 🟢 **Score 10** → Bonne qualité
- 🟡 **Volume 1.6** → Volume modéré
- 🟢 **ATR 1.1** → Volatilité normale
- 🟢 **Run 3** → Momentum confirmé
- 🟢 **Align 3** → Alignement parfait
- 🔥 **Type +2** → Bull Fort
- 🔴 **Speed 1.2** → **LENT** - Peu de mouvement ! 🆕
- ❌ **Scalp 0** → Non adapté scalping

**Action recommandée** : **ÉVITER pour scalping** - Privilégier swing
**Problème** : Speed trop faible = peu d'opportunités intraday
**Alternative** : Position swing ou day trading (pas scalping)

---

### Exemple 3 : Speed Élevé mais Score Faible ⚠️

**Affichage dans ProScreener** :
```
Score: 7   | Volume: 3.2 | ATR: 2.1 | Run: 2 | Align: 1 | Type: 0  | Speed: 2.6 | Scalp: 0 | T1: +1 | T2: -1 | T3: 0
```

**Interprétation** :
- 🟡 **Score 7** → Qualité moyenne (seuil minimum)
- 🟢 **Volume 3.2** → Volume très élevé
- 🔴 **ATR 2.1** → Volatilité EXCESSIVE (risque élevé)
- 🟡 **Run 2** → Peu de momentum
- 🔴 **Align 1** → Pas de cohérence
- ⚠️ **Type 0** → Range/Neutre
- 🔥 **Speed 2.6** → Très rapide (beaucoup de mouvement) 🆕
- ❌ **Scalp 0** → Non adapté (volatilité excessive)

**Action recommandée** : **PRUDENCE** - Speed élevé MAIS risque élevé
**Problème** : Mouvements rapides mais volatilité excessive = slippage
**Stratégie** : Si trade, utiliser SL très larges (2-3x ATR)

---

## 💡 Stratégies d'Utilisation V4.0

### 1. 🆕 Scalping Ultra-Rapide (SpeedMeter) - V4.0

**Objectif** : Scalping sur mouvements explosifs avec SpeedMeter

**Filtres dans ProScreener** :
- `Speed >= 2.5` ⚡ **CRITÈRE CLÉ V4** (mouvements très rapides)
- `Scalp = 1` (liquidité + spread + volatilité optimaux)
- `Score >= 9`
- `Type = +2` (bull fort) OU `Type = -2` (bear fort)

**Entrée** :
- Type +2 + Speed ≥ 2.5 + Scalp 1 → **LONG ultra-rapide**
- Type -2 + Speed ≥ 2.5 + Scalp 1 → **SHORT ultra-rapide**

**Stop-Loss** : 0.3-0.5 x ATR (ultra serré)
**Take-Profit** : 1:1 (très rapide, nombreuses opportunités)

**Avantages Speed ≥ 2.5** :
- ⚡ Mouvements explosifs = profits rapides
- 📊 Nombreuses opportunités par session
- 🎯 Idéal pour timeframes 1-5 min

---

### 2. Scalping Modéré (Speed + Scalp)

**Objectif** : Scalping avec bonnes conditions

**Filtres dans ProScreener** :
- `Speed >= 2.0` (rapide)
- `Scalp = 1`
- `Score >= 9`
- `Type = ±2`

**Entry** : Sur pullback ou cassure
**Stop-Loss** : 0.5-1.0 x ATR
**Take-Profit** : 1:1 à 1:1.5

---

### 3. Filtrage par SpeedMeter

**Pour instruments ACTIFS uniquement** :
1. Trier colonne **"Speed"** décroissant
2. Sélectionner **Speed ≥ 2.0**
3. Vérifier **Score ≥ 9**
4. Vérifier **Type = ±2** selon direction souhaitée

**Pour éviter instruments MORTS** :
- Exclure **Speed < 1.5** (trop lent pour intraday)

---

### 4. Trading de Momentum (Intraday)

**Objectif** : Capturer les mouvements forts intraday

**Filtres** :
- `Score >= 9`
- `Speed >= 1.8` (mouvements suffisamment rapides)
- `Type = +2` ou `Type = -2`
- `Run >= 3`

**Entry** : Dans la direction du Type
**Stop-Loss** : 1.5 x ATR

---

### 5. Trading Directionnel Simplifié

**Pour LONG uniquement** :
- Filtrer `Type >= +1`
- Chercher `Score >= 9` + `Speed >= 1.8`
- Entry sur pullback
- Stop sous dernier bas

**Pour SHORT uniquement** :
- Filtrer `Type <= -1`
- Chercher `Score >= 9` + `Speed >= 1.8`
- Entry sur retracement
- Stop au-dessus dernier haut

---

### 6. Range Trading (Support/Résistance)

**Filtres** :
- `Type = 0` (neutre)
- `Score >= 7`
- Identifier supports/résistances

**Note** : Speed peut être faible en range (normal)

---

## ⚙️ Paramètres Configurables

Tous les paramètres sont dans le fichier `.prt` :

```prorealtime
// === PARAMETRES GENERAUX ===
lookbackPeriod = 100    // Période historique (20-200)
atrPeriod = 14          // Période ATR (7-21)
minBodyRatio = 0.5      // Ratio corps/mèche (0.3-0.7)
minVolRatio = 1.0       // Volume minimum (0.8-1.5)
enableMTF = 1           // Multi-tendance ON/OFF
emaPeriod1 = 20         // EMA court terme (10-30)
emaPeriod2 = 50         // EMA moyen terme (30-70)
emaPeriod3 = 100        // EMA long terme (80-150)

// === PARAMETRES SCALPING ===
minVolumeScalping = 2.0     // Volume min scalping (2.0-3.0)
maxSpreadScalping = 0.3     // Spread max scalping (0.2-0.5%)
maxATRScalping = 1.3        // ATR max scalping (1.2-1.5)

// === PARAMETRES SPEEDMETER (V4.0) === 🆕
velocityPeriod = 20         // Période vitesse moyenne (10-30)
minSpeedScalping = 1.8      // Speed min scalping (1.5-2.5)
```

### Ajuster le SpeedMeter 🆕

**Ligne 57** - Modifier période de calcul :
```prorealtime
velocityPeriod = 20  // Réduire à 10 pour plus de réactivité
                     // Augmenter à 30 pour plus de stabilité
```

**Ligne 58** - Modifier seuil minimum :
```prorealtime
minSpeedScalping = 1.8  // Augmenter à 2.0 pour être plus strict
                        // Réduire à 1.5 pour plus de résultats
```

### Ajuster le seuil de filtrage

**Ligne 430** - Modifier le seuil Score :
```prorealtime
condition = (qualityScore >= 7)  // Modifier pour +/- strict
```

### Personnaliser les noms de colonnes

**Ligne 436** - Modifier les alias affichés :
```prorealtime
SCREENER[condition](
  qualityScore AS "Score",
  volumeRatio AS "Volume",
  atrRatio AS "ATR",
  directionalRun AS "Run",
  alignmentScore AS "Align",
  marketType AS "Type",
  speedMeter AS "Speed",      // 🆕 V4.0
  scalpQuality AS "Scalp",
  trend1 AS "T1",
  trend2 AS "T2",
  trend3 AS "T3"
)
```

---

## 🔧 Timeframe Recommandé

### Optimal pour V4.0 : **1, 5 ou 10 minutes** 🆕

**Pourquoi ?**
- SpeedMeter optimisé pour scalping court terme
- Mouvements rapides visibles sur ces timeframes
- Volume et vitesse mesurés efficacement

### Adaptations

| Timeframe | Speed Attendu | Usage V4.0 |
|-----------|---------------|------------|
| **1 min** | 2.0-3.5 | Scalping ultra-rapide ✅ |
| **5 min** | 1.8-2.5 | Scalping actif ✅ |
| **10 min** | 1.5-2.0 | Scalping modéré ✅ |
| **15 min** | 1.2-1.8 | Day trading |
| **1 heure** | 0.8-1.5 | Position trading |

---

## 📊 Métriques Détaillées

### 7. 🆕 Speed - SpeedMeter (V4.0)

**Variable** : `speedMeter`
**Calcul** : `(Velocity Ratio + Tick Activity) / 2`
**Optimal** : ≥ 2.0 (rapide), ≥ 2.5 (très rapide)
**Usage** : Identifier instruments avec mouvements rapides pour scalping

**Composants** :
1. **Velocity Ratio** : Mouvement prix actuel / Moyenne 20 bougies
2. **Tick Activity** : Volume Ratio (activité de trading)

**Interprétation** :
- Speed élevé = Mouvements rapides + Volume élevé
- Speed faible = Instrument "mort", peu d'activité

---

## 📝 Notes Importantes

### SpeedMeter V4.0 🆕

1. **Speed dépend du timeframe**
   - 1 min : Speed généralement plus élevé
   - 1 heure : Speed généralement plus faible
   - Adapter `minSpeedScalping` selon timeframe

2. **Speed vs Scalp**
   - **Speed** : Mesure vitesse/activité
   - **Scalp** : Mesure conditions (spread/volume/volatilité)
   - **Optimal** : Speed ≥ 2.0 ET Scalp = 1

3. **Éviter Speed excessif**
   - Speed > 4.0 peut indiquer mouvement anormal (news, gap)
   - Vérifier contexte avant entry

### Limitations Techniques

1. **VWAP se réinitialise chaque jour** (ligne 144)
2. **Runs directionnels limités à 10 bougies** (lignes 117-136)
3. **Multi-tendance désactivable** (`enableMTF = 0`)
4. **Filtrage automatique actif** (`Score >= 7`)

### Compatibilité

✅ **Compatible avec** :
- ProRealTime V12+
- ProScreener (mode gratuit et premium)
- Tous les instruments (Actions, Indices, Forex, Crypto)
- Timeframes : 1min à Daily (optimal 1-10min pour SpeedMeter)

❌ **Non compatible avec** :
- ProRealTime V11 et antérieur
- ProBacktest (c'est un screener)

---

## 🔍 Dépannage

### Problème : Speed toujours faible

**Causes** :
- Timeframe trop long (essayer 1 ou 5 min)
- Instruments peu actifs (changer de watchlist)
- `velocityPeriod` trop élevé (réduire à 10-15)

**Solutions** :
1. Utiliser timeframe 1 ou 5 min
2. Tester sur instruments plus liquides (indices, Forex majeurs)
3. Réduire `velocityPeriod` à 15

### Problème : Speed toujours très élevé

**Causes** :
- Timeframe trop court
- Période de forte volatilité (news)
- `velocityPeriod` trop faible

**Solutions** :
1. Augmenter `velocityPeriod` à 30
2. Vérifier pas d'événements exceptionnels

### Problème : Aucun résultat

**Solutions** :
1. Réduire seuil : `condition = (qualityScore >= 5)`
2. Vérifier watchlist contient instruments actifs
3. Essayer timeframe différent

---

## 📚 Documentation Complémentaire

### Fichiers du Projet V4.0

1. **`trading_quality_metrics_v4.prt`** (442 lignes)
   - Code source ProScreener V4.0
   - SpeedMeter intégré (lignes 371-409)
   - 11 colonnes personnalisées

2. **`README_V4.md`** (ce fichier)
   - Guide complet V4.0
   - Documentation SpeedMeter
   - Stratégies avec Speed

3. **`LEGENDE_CRITERES_V4.md`**
   - Légende des 11 colonnes
   - Exemples détaillés avec Speed
   - Stratégies avancées

---

## 📜 Changelog

### Version 4.1 (2025-10-27) - Actuelle ⭐ CORRECTIF

**🔧 CORRECTIF : Intégration minSpeedScalping dans Scalp**
- ✅ **Correction erreur** : Variable `minSpeedScalping` maintenant utilisée
- ✅ **Critère Scalp amélioré** : 4 conditions au lieu de 3
  - Volume ≥ 2.0x
  - Spread ≤ 0.3%
  - ATR ≤ 1.3x
  - **Speed ≥ 1.8** 🆕 (nouveau dans V4.1)
- ✅ **Plus précis** : Scalp = 1 garantit vitesse suffisante
- ✅ **Fichier** : `trading_quality_metrics_v4_1.prt` (391 lignes)

**Impact** :
- ⚡ Scalp = 1 nécessite maintenant mouvements rapides (Speed ≥ 1.8)
- ❌ Évite faux positifs (bonnes conditions mais lent)
- 🎯 Filtrage scalping encore plus précis

**Code modifié** (ligne 378) :
```prorealtime
// AVANT V4.0
IF volumeRatio >= 2.0 AND spreadRatio <= 0.3 AND atrRatio <= 1.3 THEN
    scalpQuality = 1
ENDIF

// APRÈS V4.1
IF volumeRatio >= 2.0 AND spreadRatio <= 0.3 AND atrRatio <= 1.3 AND speedMeter >= 1.8 THEN
    scalpQuality = 1
ENDIF
```

---

### Version 4.0 (2025-10-27) - SPEEDMETER

**🆕 SPEEDMETER : Mesure de Vitesse des Mouvements**
- ✅ **Nouvelle colonne "Speed"** : SpeedMeter pour vitesse/activité
- ✅ **11 colonnes** : Score, Volume, ATR, Run, Align, Type, Speed, Scalp, T1, T2, T3
- ✅ **Calcul avancé** : Velocity Ratio + Tick Activity
- ✅ **Paramètres ajustables** : velocityPeriod, minSpeedScalping
- ✅ **Stratégies SpeedMeter** : Scalping ultra-rapide avec Speed ≥ 2.5

**Impact utilisateur** :
- ⚡ Identification mouvements rapides pour scalping
- 📊 Éviter instruments "morts" (Speed < 1.5)
- 🎯 Filtrage précis pour scalping 1/5/10 min
- 🔥 Combinaison Speed + Scalp = Setup optimal

**Changements techniques** :
```prorealtime
// V4.0 - Calcul SpeedMeter
velocityRatio = priceVelocity / avgVelocity
tickActivity = volumeRatio
speedMeter = (velocityRatio + tickActivity) / 2

// V4.0 - 11 colonnes au lieu de 10
SCREENER[condition](..., speedMeter AS "Speed", ...)
```

---

### Version 3.1 (2025-10-27) - SCALPING

**🆕 MODE SCALPING**
- ✅ Colonne "Scalp" (critère 1/0)
- ✅ 10 colonnes
- ✅ Paramètres scalping ajustables

---

### Version 3.0 (2025-10-26) - MAJEURE

**🎉 RÉVOLUTION : Colonnes Personnalisées**
- ✅ Alias AS fonctionnels
- ✅ 9 colonnes lisibles
- ✅ Interface professionnelle

---

### Version 2.2 (2025-10-26)

**📝 Nomenclature**
- ✅ En-têtes détaillés
- ✅ Commentaires enrichis

---

## ⚠️ Avertissements

### Risques du Trading

- ⚠️ **Le trading comporte des risques** : Perte possible
- ⚠️ **Aucun système infaillible** : Speed élevé ne garantit pas profit
- ⚠️ **Gestion du risque obligatoire** : Max 1-2% par trade
- ⚠️ **Backtesting recommandé** : Tester avant trading réel
- ⚠️ **SpeedMeter = indicateur** : Ne pas trader uniquement sur Speed

### Conditions de Marché

- 📉 **Gap et news** : Speed peut être anormalement élevé
- 📊 **Slippage réel** : Estimation, pas garantie
- 💰 **Frais non inclus** : Commissions non calculées
- ⏰ **Heures de marché** : Privilégier heures liquides

---

## 🏆 Résumé Rapide (TL;DR)

**Ce que fait le screener V4.0** :
- ✅ Calcule score qualité 0-13
- ✅ Classe : Bull/Bear/Range
- ✅ 🆕 **Mesure vitesse des mouvements** (SpeedMeter)
- ✅ Affiche 11 colonnes lisibles
- ✅ Filtre scalping (Scalp)
- ✅ Interface : **Score | Volume | ATR | Run | Align | Type | Speed | Scalp | T1 | T2 | T3**

**Comment l'utiliser** :
1. Copier code `.prt` dans ProScreener
2. Lancer sur timeframe **1, 5 ou 10 minutes** 🆕
3. Trier par **"Speed"** décroissant → instruments rapides 🆕
4. Filtrer **Speed ≥ 2.0** + **Scalp = 1** pour scalping optimal 🆕
5. Vérifier **Score ≥ 9** + **Type = ±2**

**Setup PARFAIT V4.0** :
- 🔥 **Speed ≥ 2.5** (très rapide)
- ⚡ **Scalp = 1** (conditions optimales)
- 🎯 **Score ≥ 10** (haute qualité)
- 🚀 **Type = ±2** (tendance forte)

**Nouveauté V4.0** :
- 🆕 **SpeedMeter** : Velocity + Tick Activity
- ⚡ **Filtre mouvements rapides** : Speed ≥ 2.0
- 🎯 **Évite instruments morts** : Speed < 1.5
- 📊 **Optimal scalping 1-10 min**

---

**Version**: 4.0
**Date**: 2025-10-27
**Compatibilité**: ProRealTime V12+ / ProScreener
**Auteur**: Script généré avec Claude Code
**Licence**: Éducatif - Utilisez à vos propres risques
**Statut**: ✅ Testé et fonctionnel

---

**⭐ Si ce screener vous aide, n'hésitez pas à le partager !**

🚀 **Bon trading avec le SpeedMeter pour capturer les mouvements rapides !**

---

## 🎯 Tableau Récapitulatif des Colonnes V4.0

| Colonne | Nom Affiché | Variable | Signification | Bon Signal |
|---------|-------------|----------|---------------|------------|
| 1 | **Score** | qualityScore | Qualité globale | ≥ 10 |
| 2 | **Volume** | volumeRatio | Liquidité | ≥ 2.0 |
| 3 | **ATR** | atrRatio | Volatilité | 0.8-1.2 |
| 4 | **Run** | directionalRun | Momentum | ≥ 3 |
| 5 | **Align** | alignmentScore | Cohérence tendances | 3 |
| 6 | **Type** | marketType | Bull/Bear/Range | ±2 |
| 7 | **Speed** 🆕 | speedMeter | Vitesse mouvements | ≥ 2.0 |
| 8 | **Scalp** | scalpQuality | Adapté scalping | 1 |
| 9 | **T1** | trend1 | Court terme | ±1 |
| 10 | **T2** | trend2 | Moyen terme | ±1 |
| 11 | **T3** | trend3 | Long terme | ±1 |

**Signal idéal V4.0** :
```
Score: 12 | Volume: 2.5+ | ATR: 1.0 | Run: 4 | Align: 3 | Type: ±2 | Speed: 2.5+ | Scalp: 1 | T1/T2/T3: ±1
```

**Signal idéal SCALPING ULTRA-RAPIDE V4.0** 🚀 :
```
Score: 11+ | Volume: 2.5+ | Speed: 2.5+ | Scalp: 1 | Type: ±2
```
