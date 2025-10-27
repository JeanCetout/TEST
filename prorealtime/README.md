# 📊 ProRealTime Trading Quality Metrics - Version 3.1

**Screener ProRealTime avancé avec colonnes personnalisées, optimisé pour le scalping de qualité avec filtres liquidité/spread.**

[![Version](https://img.shields.io/badge/version-3.1-brightgreen.svg)](https://github.com)
[![ProRealTime](https://img.shields.io/badge/ProRealTime-V12%2B-green.svg)](https://www.prorealtime.com)
[![License](https://img.shields.io/badge/license-Educational-orange.svg)](https://github.com)
[![Tested](https://img.shields.io/badge/status-Tested%20%26%20Working-success.svg)](https://github.com)

---

## 🆕 NOUVEAUTÉ VERSION 3.1 - MODE SCALPING

### ⚡ Filtre Scalping de Qualité

**VERSION 3.1** ajoute un critère **"Scalp"** pour identifier les instruments optimaux pour le scalping !

**Nouvelle colonne** : **"Scalp"** (colonne 7)
- **1** = ✅ Adapté scalping (liquidité élevée + spread faible + volatilité maîtrisée)
- **0** = ❌ Non adapté scalping (critères non remplis)

**Critères Scalping** :
- 💰 **Volume ≥ 2.0x** la moyenne (liquidité excellente)
- 📉 **Spread ≤ 0.3%** du prix (coûts minimaux)
- 📊 **ATR ≤ 1.3x** la moyenne (volatilité contrôlée)

**Affichage ProScreener V3.1** :
```
Score | Volume | ATR | Run | Align | Type | Scalp | T1 | T2 | T3
                                           ↑
                                        NOUVEAU!
```

**Impact pour scalpers** :
- ⚡ **Filtrage instantané** : Tri par colonne "Scalp" = 1
- 💰 **Coûts minimisés** : Spread faible = plus de profit net
- 🎯 **Exécution optimale** : Volume élevé = slippage réduit
- 📊 **Risque maîtrisé** : Volatilité contrôlée = stops précis

---

## ✨ Historique V3.0 - Colonnes Personnalisées

**VERSION 3.0** a introduit les colonnes personnalisées :

**AVANT (V2.x)** : Noms de variables techniques
```
qualityScore | volumeRatio | atrRatio | directionalRun | ...
```

**APRÈS (V3.0)** : Noms clairs et lisibles
```
Score | Volume | ATR | Run | Align | Type | T1 | T2 | T3
```

---

## 🎯 Qu'est-ce que ce screener fait ?

Ce **ProScreener V3.1** analyse en temps réel la qualité de trading de vos instruments financiers et vous aide à :

✅ **Identifier les meilleures opportunités** grâce à un score de qualité sur 13 points
✅ **Classifier automatiquement le type de marché** (Bull Fort/Modéré, Bear Fort/Modéré, Range/Neutre)
✅ **Analyser 10 métriques techniques** (volume, volatilité, momentum, VWAP, slippage, régularité)
✅ **Détecter l'alignement des tendances** sur 3 timeframes (court/moyen/long terme)
✅ **Filtrer rapidement** selon votre stratégie (LONG, SHORT, ou RANGE trading)
✅ **Identifier les instruments adaptés au scalping** avec critères volume/spread/volatilité
✅ **Afficher des colonnes lisibles** avec noms personnalisés (Score, Volume, ATR, Run, Scalp, etc.)

---

## 📋 Les 10 Colonnes Affichées

Le screener affiche **10 colonnes nommées** dans ProRealTime :

| # | Colonne Affichée | Nom Variable | Description | Plage | Optimal |
|---|------------------|--------------|-------------|-------|---------|
| **1** | **Score** | qualityScore | Score global de qualité | 0-13 | ≥ 10 |
| **2** | **Volume** | volumeRatio | Volume/Moyenne (100 périodes) | 0-∞ | ≥ 2.0 |
| **3** | **ATR** | atrRatio | Volatilité actuelle/moyenne | 0-∞ | 0.8-1.2 |
| **4** | **Run** | directionalRun | Bougies consécutives (momentum) | 0-10 | ≥ 3 |
| **5** | **Align** | alignmentScore | Nombre d'EMA alignées | 0-3 | 3 |
| **6** | **Type** | marketType | Classification Bull/Bear/Range | -2 à +2 | ±2 |
| **7** | **Scalp** 🆕 | scalpQuality | Adapté scalping (1=oui, 0=non) | 0-1 | 1 |
| **8** | **T1** | trend1 | Tendance EMA 20 (court terme) | -1/0/+1 | ±1 |
| **9** | **T2** | trend2 | Tendance EMA 50 (moyen terme) | -1/0/+1 | ±1 |
| **10** | **T3** | trend3 | Tendance EMA 100 (long terme) | -1/0/+1 | ±1 |

**Condition de filtrage par défaut** : `Score >= 7`

**🆕 Colonne Scalp (V3.1)** : Filtre automatique basé sur Volume ≥ 2.0x + Spread ≤ 0.3% + ATR ≤ 1.3x

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
3. Nommez-le : `Trading Quality V3.1`

### Étape 2 : Copier le Code

1. Ouvrez le fichier **`proscreener/trading_quality_metrics_v2_FINAL.prt`**
2. **Copiez tout le contenu** (352 lignes)
3. **Collez** dans la fenêtre ProScreener

### Étape 3 : Configuration Recommandée

| Paramètre | Valeur Recommandée | Description |
|-----------|-------------------|-------------|
| **Unité de temps** | **1 minute** | Optimal pour analyse intraday |
| **Liste** | Votre watchlist | CAC40, NASDAQ100, Forex, Crypto |
| **Condition** | `Score >= 7` | Déjà configuré (ligne 345) |

### Étape 4 : Lancer le Scan

1. Cliquez sur **Lancer le Screener**
2. Les résultats s'affichent avec les 10 colonnes nommées :
   ```
   Score | Volume | ATR | Run | Align | Type | Scalp | T1 | T2 | T3
   ```
3. **Triez par colonne** pour filtrer :
   - **Score** : Trier décroissant → meilleurs scores en haut
   - **Type** : Trier par valeur → regrouper bulls (+2, +1) et bears (-2, -1)
   - **Scalp** : Trier décroissant → instruments scalping d'abord (1 = adapté)
   - **Volume** : Trier décroissant → plus forte liquidité d'abord

---

## 📈 Exemples d'Interprétation

### Exemple 1 : Signal d'Achat Optimal ⭐⭐⭐

**Affichage dans ProScreener** :
```
Score: 12  | Volume: 2.3 | ATR: 1.0 | Run: 4 | Align: 3 | Type: +2 | Scalp: 1 | T1: +1 | T2: +1 | T3: +1
```

**Interprétation** :
- 🟢 **Score 12/13** → Excellente qualité
- 🟢 **Volume 2.3** → Volume x2.3 (forte participation)
- 🟢 **ATR 1.0** → Volatilité normale (risque maîtrisé)
- 🟢 **Run 4** → 4 bougies haussières consécutives (momentum)
- 🟢 **Align 3** → Toutes les EMA alignées
- 🔥 **Type +2** → **BULL FORT confirmé**
- ⚡ **Scalp 1** → **Adapté scalping** (liquidité + spread optimaux)
- 🟢 **T1/T2/T3 = +1** → Toutes les tendances haussières

**Action recommandée** : **ACHAT fort** avec SL serré
**Probabilité** : Très élevée
**Stratégie** : Momentum trading / Scalping haussier optimal

---

### Exemple 2 : Signal à Éviter ❌

**Affichage dans ProScreener** :
```
Score: 8   | Volume: 0.7 | ATR: 1.8 | Run: 2 | Align: 1 | Type: 0  | Scalp: 0 | T1: +1 | T2: -1 | T3: 0
```

**Interprétation** :
- 🟡 **Score 8** → Qualité moyenne
- 🔴 **Volume 0.7** → Volume faible (30% sous moyenne)
- 🔴 **ATR 1.8** → Volatilité élevée (risque)
- 🟡 **Run 2** → Pas de momentum clair
- 🔴 **Align 1** → Une seule EMA alignée
- ⚠️ **Type 0** → **RANGE/Neutre, pas de direction**
- ❌ **Scalp 0** → **Non adapté scalping** (volume faible + volatilité excessive)
- ⚠️ **T1: +1, T2: -1, T3: 0** → Tendances contradictoires !

**Action recommandée** : **ÉVITER** - Signaux contradictoires
**Problème** : CT haussier vs MT baissier + mauvaises conditions scalping
**Stratégie** : Attendre clarification du marché

---

### Exemple 3 : Signal de Vente ⬇️

**Affichage dans ProScreener** :
```
Score: 11  | Volume: 1.9 | ATR: 0.9 | Run: 5 | Align: 3 | Type: -2 | Scalp: 0 | T1: -1 | T2: -1 | T3: -1
```

**Interprétation** :
- 🟢 **Score 11/13** → Haute qualité
- 🟢 **Volume 1.9** → Volume élevé (pression vendeuse)
- 🟢 **ATR 0.9** → Volatilité normale
- 🟢 **Run 5** → 5 bougies baissières consécutives (fort momentum)
- 🟢 **Align 3** → Toutes les EMA alignées
- 🔴 **Type -2** → **BEAR FORT confirmé**
- 🟡 **Scalp 0** → Non adapté scalping (volume < 2.0x)
- 🔴 **T1/T2/T3 = -1** → Toutes les tendances baissières

**Action recommandée** : **VENTE/SHORT** avec confirmation
**Probabilité** : Très élevée
**Stratégie** : Momentum baissier / Position courte (non scalping)

---

## 💡 Stratégies d'Utilisation

### 1. 🆕 Scalping de Qualité (V3.1)

**Objectif** : Scalping ultra-rapide avec conditions optimales

**Filtres dans ProScreener** :
- `Score >= 9`
- `Scalp = 1` ⚡ **CRITÈRE CLÉ** (liquidité + spread + volatilité optimaux)
- `Type = +2` (bull fort) OU `Type = -2` (bear fort)
- `Run >= 3`

**Entrée** :
- Type +2 + Scalp 1 → Position **LONG** rapide
- Type -2 + Scalp 1 → Position **SHORT** rapide

**Stop-Loss** : Très serré (0.5 à 1.0 x ATR)
**Take-Profit** : Rapide (1:1 ou 1:1.5 risk/reward)

**Avantages Scalp = 1** :
- Volume élevé → Exécution instantanée
- Spread faible → Profit net maximisé
- Volatilité maîtrisée → Stops précis

---

### 2. Trading de Momentum (Intraday)

**Objectif** : Capturer les mouvements forts intraday

**Filtres dans ProScreener** :
- `Score >= 9`
- `Type = +2` (bull fort) OU `Type = -2` (bear fort)
- `Run >= 3`

**Entrée** :
- Type +2 → Position **LONG**
- Type -2 → Position **SHORT**

**Stop-Loss** : Basé sur ATR (ex: 1.5 x ATR)

---

### 3. Trading Directionnel Simplifié

**Objectif** : Ne trader que dans UN sens (LONG ou SHORT)

**Pour LONG uniquement** :
- Filtrer `Type >= +1` dans ProScreener
- Chercher `Score >= 9` + `Run >= 3`
- Entrée sur pullback ou cassure
- Stop sous dernier bas

**Pour SHORT uniquement** :
- Filtrer `Type <= -1` dans ProScreener
- Chercher `Score >= 9` + `Run >= 3`
- Entrée sur retracement ou cassure
- Stop au-dessus dernier haut

---

### 4. Range Trading (Support/Résistance)

**Objectif** : Profiter des oscillations en range

**Filtres dans ProScreener** :
- `Type = 0` (neutre)
- `Score >= 7`
- Identifier supports/résistances visuellement

**Stratégie** :
- Achat au support + confirmation (chandelier, volume)
- Vente à la résistance + confirmation
- Stops serrés hors de la range

---

### 5. Trading de Qualité Pure

**Objectif** : Trader uniquement les setups parfaits

**Filtres dans ProScreener** :
- `Score >= 11`
- `Align = 3`
- Ignorer la direction initialement

**Entrée** :
- Suivre la direction du `Type` (+2 = LONG, -2 = SHORT)
- Attendre confirmation (volume, pattern chandelier)
- Risque minimal, probabilité maximale

---

### 6. Gestion de Risque Dynamique

**Réduction de position selon ATR** :
```
Si ATR > 1.5 → Réduire taille position de 50%
Si ATR > 2.0 → Réduire taille position de 75%
```

**Éviter complètement** :
- `Align < 2` → Pas de clarté tendancielle
- `Type = 0` ET pas de stratégie range définie
- `Volume < 0.8` → Manque de liquidité
- `Score < 7` → Déjà filtré par défaut

---

## ⚙️ Paramètres Configurables

Tous les paramètres sont dans le fichier `.prt` (lignes 33-45) :

```prorealtime
// === PARAMETRES ===
lookbackPeriod = 100    // Période historique pour moyennes (20-200)
atrPeriod = 14          // Période ATR standard (7-21)
minBodyRatio = 0.5      // Ratio corps/mèche minimum (0.3-0.7)
minVolRatio = 1.0       // Volume minimum pour bonus (0.8-1.5)
enableMTF = 1           // Multi-tendance ON/OFF (1/0)
emaPeriod1 = 20         // EMA court terme (10-30)
emaPeriod2 = 50         // EMA moyen terme (30-70)
emaPeriod3 = 100        // EMA long terme (80-150)

// === PARAMETRES SCALPING (V3.1) ===
minVolumeScalping = 2.0     // Volume minimum pour scalping (2.0-3.0)
maxSpreadScalping = 0.3     // Spread maximum pour scalping (0.2-0.5%)
maxATRScalping = 1.3        // ATR maximum pour scalping (1.2-1.5)
```

### Ajuster le seuil de filtrage

**Ligne 345** - Modifier le seuil Score :

```prorealtime
condition = (qualityScore >= 7)  // Changer 7 pour filtrer +/- strict
```

**Exemples** :
- `>= 9` → Très strict, signaux rares mais fiables
- `>= 5` → Plus permissif, beaucoup de résultats
- `>= 11` → Ultra strict, perfection uniquement

### Ajuster les critères scalping

**Lignes 43-45** - Modifier les seuils scalping :

```prorealtime
minVolumeScalping = 2.0     // Augmenter à 3.0 pour être plus strict
maxSpreadScalping = 0.3     // Réduire à 0.2 pour spreads plus serrés
maxATRScalping = 1.3        // Réduire à 1.2 pour moins de volatilité
```

### Personnaliser les noms de colonnes

**Ligne 351** - Modifier les alias affichés :

```prorealtime
SCREENER[condition](
  qualityScore AS "Score",      // Changer "Score" par autre nom
  volumeRatio AS "Volume",      // Changer "Volume" par "Vol"
  atrRatio AS "ATR",            // Changer "ATR" par "Volatilite"
  scalpQuality AS "Scalp",      // Changer "Scalp" par "Scal"
  ...
)
```

**Contraintes** :
- Utiliser des guillemets doubles `"Nom"`
- Éviter les caractères spéciaux (%, /, etc.)
- Noms courts recommandés (max 10 caractères)

---

## 🔧 Timeframe Recommandé

### Optimal : **1 minute**

**Pourquoi ?**
- EMA 20/50/100 représentent ~20min/50min/100min
- Couvre court, moyen, long terme intraday
- Volume et ATR calculés sur base minute
- Idéal pour scalping et day trading

### Adaptations Possibles

| Timeframe | EMA Court | EMA Moyen | EMA Long | Usage |
|-----------|-----------|-----------|----------|-------|
| **1 min** | 20 | 50 | 100 | Scalping/Intraday ✅ |
| **5 min** | 10 | 25 | 50 | Day trading |
| **15 min** | 5 | 10 | 20 | Swing trading |
| **1 heure** | 20 | 50 | 100 | Position trading |
| **Daily** | 10 | 20 | 50 | Swing/Position long terme |

**Pour adapter** : Modifier `emaPeriod1`, `emaPeriod2`, `emaPeriod3` dans les paramètres.

---

## 📊 Métriques Détaillées

### 1. Score - Score Global de Qualité
**Variable** : `qualityScore`
**Calcul** : 10 métriques base + 3 bonus multi-tendance
**Optimal** : ≥ 10 (haute qualité)
**Usage** : Filtrer les meilleures opportunités

### 2. Volume - Volume/Moyenne
**Variable** : `volumeRatio`
**Calcul** : `volume / AVERAGE[100](volume)`
**Optimal** : ≥ 1.5 (volume 50% supérieur)
**Usage** : Confirmer validité du mouvement de prix

### 3. ATR - Volatilité
**Variable** : `atrRatio`
**Calcul** : `AverageTrueRange[14] / AVERAGE[100](ATR)`
**Optimal** : 0.8 - 1.2 (volatilité normale)
**Usage** : Ajuster taille de position et stops

### 4. Run - Bougies Consécutives
**Variable** : `directionalRun`
**Calcul** : Compte bougies consécutives même direction (max 10)
**Optimal** : ≥ 3 (tendance confirmée)
**Usage** : Détecter momentum et continuation

### 5. Align - EMA Alignées
**Variable** : `alignmentScore`
**Calcul** : Nombre d'EMA (20/50/100) alignées dans même direction
**Optimal** : 3 (toutes alignées)
**Usage** : Confirmer force de la tendance

### 6. Type - Classification Marché
**Variable** : `marketType`
**Calcul** : Basé sur `bullishAlign` et `bearishAlign`
**Optimal** : ±2 (bull fort ou bear fort)
**Usage** : Filtrage directionnel rapide

### 7. 🆕 Scalp - Adapté Scalping (V3.1)
**Variable** : `scalpQuality`
**Calcul** : `volumeRatio >= 2.0 AND spreadRatio <= 0.3 AND atrRatio <= 1.3`
**Valeurs** : 1 (adapté), 0 (non adapté)
**Optimal** : 1
**Usage** : Identifier instruments optimaux pour scalping

### 8. T1 - Tendance Court Terme
**Variable** : `trend1`
**Calcul** : Comparaison `close` vs `EMA[20]`
**Valeurs** : +1 (hausse), 0 (neutre), -1 (baisse)
**Usage** : Réactivité court terme

### 9. T2 - Tendance Moyen Terme
**Variable** : `trend2`
**Calcul** : Comparaison `close` vs `EMA[50]`
**Valeurs** : +1 (hausse), 0 (neutre), -1 (baisse)
**Usage** : Confirmation médiane

### 10. T3 - Tendance Long Terme
**Variable** : `trend3`
**Calcul** : Comparaison `close` vs `EMA[100]`
**Valeurs** : +1 (hausse), 0 (neutre), -1 (baisse)
**Usage** : Tendance de fond

---

## 📝 Notes Importantes

### Limitations Techniques

1. **VWAP se réinitialise chaque jour** (ligne 114)
   - Le calcul redémarre à chaque nouvelle session
   - Pertinent uniquement en intraday

2. **Runs directionnels limités à 10 bougies** (lignes 87-106)
   - Maximum analysé : 10 bougies consécutives
   - Au-delà, la valeur reste à 10

3. **Multi-tendance désactivable** (ligne 31)
   - Mettre `enableMTF = 0` pour désactiver les EMA
   - Type, T1, T2, T3 seront tous à 0

4. **Filtrage automatique actif** (ligne 326)
   - Seuls les `Score >= 7` s'affichent par défaut
   - Modifier la ligne pour ajuster le seuil

5. **Calculs temps réel uniquement**
   - Aucune fonction look-ahead (pas de biais futur)
   - Utilisable en live trading

### Compatibilité

✅ **Compatible avec** :
- ProRealTime V12+
- ProScreener (mode gratuit et premium)
- Tous les instruments (Actions, Indices, Forex, Crypto, Matières premières)
- Tous les timeframes (1min à Daily)

❌ **Non compatible avec** :
- ProRealTime V11 et antérieur (syntaxe AS non supportée)
- ProBacktest (c'est un screener, pas un backtest)

---

## 🔍 Dépannage

### Problème : Aucun résultat

**Solutions** :
1. Réduire le seuil : `condition = (qualityScore >= 5)` (ligne 326)
2. Vérifier la watchlist : Contient-elle des instruments actifs ?
3. Vérifier le timeframe : Essayer 5min ou 15min
4. Augmenter `lookbackPeriod` à 200

### Problème : Trop de résultats

**Solutions** :
1. Augmenter le seuil : `condition = (qualityScore >= 9)`
2. Filtrer par Type : Ajouter `AND ABS(marketType) >= 1`
3. Réduire la watchlist : Sélectionner moins d'instruments

### Problème : Erreur de syntaxe sur ligne 351

**Solutions** :
1. Vérifier que TOUT le code est copié (352 lignes)
2. Vérifier qu'aucun caractère spécial n'est altéré
3. Copier-coller à nouveau depuis le fichier source
4. Vérifier version ProRealTime (V12+ requis pour alias AS)

### Problème : Colonnes sans noms personnalisés

**Cause** : Version ProRealTime < V12 ne supporte pas `AS "Alias"`

**Solutions** :
1. Mettre à jour ProRealTime vers V12+
2. OU retirer les alias (revenir à version 2.1)

### Problème : Valeurs aberrantes

**Vérifications** :
- `ATR` > 5 → Probable gap ou événement exceptionnel (news)
- `Volume` > 10 → Volume anormal (annonce, résultats)
- `Run` = 10 → Maximum atteint, tendance très forte (possible surextension)
- `Type` oscille → Marché en indécision (attendre clarification)

---

## 📚 Documentation Complémentaire

### Fichiers du Projet

1. **`trading_quality_metrics_v2_FINAL.prt`** (352 lignes)
   - Code source ProScreener V3.1
   - Alias personnalisés intégrés
   - Critère scalping optimisé

2. **`LEGENDE_CRITERES.md`**
   - Documentation détaillée des 10 colonnes
   - Exemples concrets avec nouveaux noms
   - Stratégies avancées incluant scalping

3. **`README.md`** (ce fichier)
   - Guide d'installation et utilisation V3.1
   - Vue d'ensemble complète du projet

### Ressources Externes

- [Documentation ProRealTime](https://www.prorealtime.com/fr/support)
- [Forum ProRealCode](https://www.prorealcode.com/forum/)
- [Langage ProBuilder](https://www.prorealtime.com/fr/probuilder)
- [Guide ProScreener](https://www.prorealtime.com/fr/proscreener)

---

## 📜 Changelog

### Version 3.1 (2025-10-26) - Actuelle ⭐ SCALPING

**🆕 MODE SCALPING : Filtre Liquidité/Spread/Volatilité**
- ✅ **Nouvelle colonne "Scalp"** : Critère 1/0 pour scalping de qualité
- ✅ **10 colonnes** : Score, Volume, ATR, Run, Align, Type, Scalp, T1, T2, T3
- ✅ **3 critères scalping** : Volume ≥ 2.0x, Spread ≤ 0.3%, ATR ≤ 1.3x
- ✅ **Paramètres ajustables** : minVolumeScalping, maxSpreadScalping, maxATRScalping
- ✅ **Stratégie dédiée** : Section scalping dans les stratégies

**Impact scalpers** :
- ⚡ Identification instantanée des instruments adaptés
- 💰 Coûts minimisés (spread faible)
- 🎯 Exécution optimale (volume élevé)
- 📊 Risque maîtrisé (volatilité contrôlée)

**Changements techniques** :
```prorealtime
// V3.1 - Ajout critère scalping
scalpQuality = 0
IF volumeRatio >= minVolumeScalping AND spreadRatio <= maxSpreadScalping AND atrRatio <= maxATRScalping THEN
    scalpQuality = 1
ENDIF

// V3.1 - 10 colonnes au lieu de 9
SCREENER[condition](..., scalpQuality AS "Scalp", ...)
```

---

### Version 3.0 (2025-10-26) - MAJEURE

**🎉 RÉVOLUTION : Colonnes Personnalisées**
- ✅ **Alias AS fonctionnels** : Noms personnalisés dans ProScreener
- ✅ **9 colonnes lisibles** : Score, Volume, ATR, Run, Align, Type, T1, T2, T3
- ✅ **Interface professionnelle** : Compréhension immédiate des résultats
- ✅ **Testé et validé** : Fonctionne parfaitement sur ProRealTime V12+

**Impact utilisateur** :
- ⚡ Gain de temps énorme (plus besoin de se référer à la doc)
- 📊 Interface épurée et professionnelle
- 🎯 Décisions plus rapides grâce à la clarté

**Changements techniques** :
```prorealtime
// AVANT V3
SCREENER[condition](qualityScore, volumeRatio, ...)

// APRÈS V3
SCREENER[condition](qualityScore AS "Score", volumeRatio AS "Volume", ...)
```

---

### Version 2.2 (2025-10-26)

**📝 Améliorations de Nomenclature** :
- ✅ En-tête détaillé avec légende dans le code
- ✅ Commentaires enrichis
- ✅ Documentation "Colonne X: nomVariable"

---

### Version 2.1 (2025-10-26)

**🆕 Nouveautés** :
- ✅ Critère `marketType` : Classification Bull/Bear/Range automatique
- ✅ 9 colonnes au lieu de 8
- ✅ Filtrage directionnel facilité

---

### Version 2.0 (2025-10-26)

**Réécriture complète** :
- ✅ Compatibilité 100% ProScreener V12
- ✅ Suppression fonctions incompatibles (TIMEFRAME, median, ELSIF)
- ✅ Système EMA multi-tendance (proxy 3 timeframes)
- ✅ Score 0-13 (10 base + 3 bonus)
- ✅ Code épuré

---

### Version 1.x (archives)

Versions antérieures avec erreurs de syntaxe et incompatibilités (obsolètes).

---

## ⚠️ Avertissements et Disclaimers

### Risques du Trading

- ⚠️ **Le trading comporte des risques** : Vous pouvez perdre tout ou partie de votre capital
- ⚠️ **Aucun système n'est infaillible** : Même un Score 13/13 ne garantit pas le profit
- ⚠️ **Gestion du risque obligatoire** : Ne risquez jamais plus de 1-2% par trade
- ⚠️ **Backtesting recommandé** : Testez sur historique avant trading réel
- ⚠️ **Éducation continue** : Formez-vous avant de trader avec argent réel

### Conditions de Marché

- 📉 **Gap et news** : Le screener ne prédit pas les gaps ou annonces importantes
- 📊 **Slippage réel** : Le slippage calculé est une estimation, pas une garantie
- 💰 **Frais non inclus** : Commissions, spreads réels non calculés dans le score
- ⏰ **Heures de marché** : Privilégier les heures liquides (éviter pre-market/after-hours)

### Utilisation du Code

- 📝 **Licence éducative** : Code fourni à des fins d'apprentissage uniquement
- 🚫 **Aucune garantie** : Fourni "tel quel" sans garantie de performance
- 🔧 **Modifications autorisées** : Vous pouvez adapter selon vos besoins
- 📢 **Partage encouragé** : Vous pouvez partager avec attribution

---

## 🎓 Pour Aller Plus Loin

### Optimisations Possibles

1. **Ajouter des patterns chandeliers** : Hammer, Engulfing, Doji, Pin Bar
2. **Intégrer RSI/MACD** : Confirmation momentum et divergences
3. **Détection support/résistance** : Niveaux clés automatiques
4. **Stop-Loss/Take-Profit auto** : Calculs basés ATR et volatilité
5. **Filtres horaires** : Éviter heures creuses (12h-14h, 17h-18h)
6. **Alertes personnalisées** : Notification quand Score >= 11 + Type = ±2

### Backtesting

Pour tester l'efficacité historique :
1. Utiliser ProBacktest (nécessite réécriture partielle en ProBuilder)
2. Exporter résultats screener vers Excel/CSV
3. Analyser performances des signaux Score >= 10
4. Calculer win rate par Type (Bull Fort vs Bear Fort)
5. Optimiser paramètres (lookbackPeriod, EMA, seuils)

### Automatisation

Possibilités avec ProOrder (compte réel uniquement) :
- Entrées automatiques sur `Score >= 11` + `Type = +2`
- Filtrage par `Type` selon stratégie (LONG/SHORT uniquement)
- Stops basés sur `ATR` (ex: 2 x ATR)
- Trailing stop adaptatif selon volatilité

---

## 💬 Support et Contact

### Problèmes ou Questions ?

1. **Vérifiez la section Dépannage** ci-dessus
2. **Consultez LEGENDE_CRITERES.md** pour détails techniques
3. **Forum ProRealCode** pour aide communauté
4. **GitHub Issues** (si applicable) pour bugs/suggestions

### Contributions

Améliorations bienvenues ! Idées :
- Nouveaux critères de qualité (RSI, MACD, Stochastic)
- Optimisations performance
- Stratégies additionnelles
- Traductions (English, Español)
- Versions pour autres timeframes

---

## 🏆 Résumé Rapide (TL;DR)

**Ce que fait le screener V3.1** :
- ✅ Calcule un score de qualité 0-13 pour chaque instrument
- ✅ Classe automatiquement : Bull Fort/Modéré, Bear Fort/Modéré, Range/Neutre
- ✅ Affiche 10 colonnes avec **noms personnalisés lisibles**
- ✅ Interface professionnelle : **Score | Volume | ATR | Run | Align | Type | Scalp | T1 | T2 | T3**
- ✅ 🆕 **Filtre scalping** : Identifie instruments adaptés (liquidité + spread + volatilité)

**Comment l'utiliser** :
1. Copier le code `.prt` dans ProScreener
2. Lancer sur timeframe **1 minute**
3. Trier par **Score** (colonne 1) décroissant
4. Filtrer par **Type** (colonne 6) selon stratégie
5. 🆕 Filtrer par **Scalp = 1** (colonne 7) pour scalping optimal

**Meilleures pratiques** :
- 🎯 **Score ≥ 10** + **Type = ±2** → Signaux les plus fiables
- ⚡ 🆕 **Scalp = 1** → Conditions optimales pour scalping
- ⚠️ **Type = 0** → Éviter ou faire du range trading
- 📊 Combiner avec analyse technique classique (S/R, patterns)
- 💰 Gestion de risque stricte (max 1-2% par trade)

**Nouveauté V3.1** :
- 🆕 **Filtre Scalping** : Colonne "Scalp" pour identifier les meilleurs instruments
- ⚡ **Critères optimisés** : Volume 2x + Spread 0.3% + ATR 1.3x
- 🎯 **10 colonnes** : Une de plus pour le scalping

**Historique V3.0** :
- 🆕 **Colonnes nommées** : Fini les noms de variables techniques !
- ⚡ **Interface claire** : Compréhension immédiate
- 🚀 **Testé et validé** : Fonctionne parfaitement

---

**Version**: 3.1
**Date**: 2025-10-27
**Compatibilité**: ProRealTime V12+ / ProScreener
**Auteur**: Script généré avec Claude Code
**Licence**: Éducatif - Utilisez à vos propres risques
**Statut**: ✅ Testé et fonctionnel

---

**⭐ Si ce screener vous aide, n'hésitez pas à le partager !**

🚀 **Bon trading et que les probabilités soient avec vous !**

---

## 🎯 Tableau Récapitulatif des Colonnes

| Colonne | Nom Affiché | Variable | Signification | Bon Signal |
|---------|-------------|----------|---------------|------------|
| 1 | **Score** | qualityScore | Qualité globale | ≥ 10 |
| 2 | **Volume** | volumeRatio | Liquidité | ≥ 1.5 |
| 3 | **ATR** | atrRatio | Volatilité | 0.8-1.2 |
| 4 | **Run** | directionalRun | Momentum | ≥ 3 |
| 5 | **Align** | alignmentScore | Cohérence tendances | 3 |
| 6 | **Type** | marketType | Bull/Bear/Range | ±2 |
| 7 | **Scalp** 🆕 | scalpQuality | Adapté scalping | 1 |
| 8 | **T1** | trend1 | Court terme | ±1 |
| 9 | **T2** | trend2 | Moyen terme | ±1 |
| 10 | **T3** | trend3 | Long terme | ±1 |

**Signal idéal** : `Score: 12 | Volume: 2.0 | ATR: 1.0 | Run: 4 | Align: 3 | Type: ±2 | Scalp: 1 | T1/T2/T3: ±1`

**Signal idéal SCALPING** : `Score: 11+ | Volume: 2.0+ | ATR: 0.9-1.1 | Run: 3+ | Type: ±2 | Scalp: 1`
