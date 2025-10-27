# 📊 ProRealTime Trading Quality Metrics - Version 2.2

**Screener ProRealTime avancé pour analyser la qualité de trading et classifier automatiquement les types de marchés (Bull/Bear/Range).**

[![Version](https://img.shields.io/badge/version-2.2-blue.svg)](https://github.com)
[![ProRealTime](https://img.shields.io/badge/ProRealTime-V12%2B-green.svg)](https://www.prorealtime.com)
[![License](https://img.shields.io/badge/license-Educational-orange.svg)](https://github.com)

---

## 🎯 Qu'est-ce que ce screener fait ?

Ce **ProScreener** analyse en temps réel la qualité de trading de vos instruments financiers et vous aide à :

✅ **Identifier les meilleures opportunités** grâce à un score de qualité sur 13 points
✅ **Classifier automatiquement le type de marché** (Bull Fort/Modéré, Bear Fort/Modéré, Range/Neutre)
✅ **Analyser 10 métriques techniques** (volume, volatilité, momentum, VWAP, slippage, etc.)
✅ **Détecter l'alignement des tendances** sur 3 timeframes (court/moyen/long terme)
✅ **Filtrer rapidement** selon votre stratégie (LONG, SHORT, ou RANGE trading)

---

## 🆕 Nouveautés Version 2.1

### Critère `marketType` - Classification Bull/Bear/Range

Le screener classe désormais **automatiquement** chaque instrument selon 5 catégories :

| Valeur | Classification | Signification | Utilisation |
|--------|----------------|---------------|-------------|
| **+2** | 🔥 **Bull Fort** | Toutes les EMA haussières | Position LONG privilégiée |
| **+1** | 🟢 **Bull Modéré** | 2+ EMA haussières | Position LONG possible |
| **0** | ⚪ **Range/Neutre** | Tendances mixtes | Range trading ou attente |
| **-1** | 🟠 **Bear Modéré** | 2+ EMA baissières | Position SHORT possible |
| **-2** | 🔴 **Bear Fort** | Toutes les EMA baissières | Position SHORT privilégiée |

**Filtrage ultra-rapide** :
- `marketType >= +1` → Affiche uniquement les marchés haussiers
- `marketType <= -1` → Affiche uniquement les marchés baissiers
- `marketType = 0` → Marchés en range (stratégies support/résistance)

---

## 📋 Les 9 Critères Affichés

Le screener affiche **9 colonnes** dans ProRealTime :

| # | Critère | Description | Plage | Optimal |
|---|---------|-------------|-------|---------|
| **1** | `qualityScore` | Score global de qualité | 0-13 | ≥ 10 |
| **2** | `volumeRatio` | Volume/Moyenne (100 périodes) | 0-∞ | ≥ 1.5 |
| **3** | `atrRatio` | Volatilité actuelle/moyenne | 0-∞ | 0.8-1.2 |
| **4** | `directionalRun` | Bougies consécutives même direction | 0-10 | ≥ 3 |
| **5** | `alignmentScore` | Nombre d'EMA alignées | 0-3 | 3 |
| **6** | `marketType` | **🆕 Bull/Bear/Range** | -2 à +2 | ±2 |
| **7** | `trend1` | Tendance EMA 20 (court terme) | -1/0/+1 | ±1 |
| **8** | `trend2` | Tendance EMA 50 (moyen terme) | -1/0/+1 | ±1 |
| **9** | `trend3` | Tendance EMA 100 (long terme) | -1/0/+1 | ±1 |

**Condition de filtrage par défaut** : `qualityScore >= 7`

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

## 🚀 Installation et Utilisation

### Prérequis
- **ProRealTime V12+** (version gratuite ou premium)
- **ProScreener** activé dans votre plateforme

### Étape 1 : Créer le Screener

1. Ouvrez **ProRealTime**
2. Menu **Outils** → **ProScreener** → **Nouveau Screener**
3. Nommez-le : `Trading Quality V2.1`

### Étape 2 : Copier le Code

1. Ouvrez le fichier **`proscreener/trading_quality_metrics_v2_FINAL.prt`**
2. **Copiez tout le contenu** (308 lignes)
3. **Collez** dans la fenêtre ProScreener

### Étape 3 : Configuration Recommandée

| Paramètre | Valeur Recommandée | Description |
|-----------|-------------------|-------------|
| **Unité de temps** | **1 minute** | Optimal pour analyse intraday |
| **Liste** | Votre watchlist | CAC40, NASDAQ100, Forex, Crypto |
| **Condition** | `qualityScore >= 7` | Déjà configuré (ligne 304) |

### Étape 4 : Lancer le Scan

1. Cliquez sur **Lancer le Screener**
2. Les résultats s'affichent avec les 9 colonnes
3. **Triez par colonne** pour filtrer :
   - Colonne 1 (qualityScore) : Trier décroissant → meilleurs scores
   - Colonne 6 (marketType) : Trier par valeur → regrouper bulls/bears

---

## 📈 Exemples d'Interprétation

### Exemple 1 : Signal d'Achat Optimal ⭐⭐⭐

```
1. qualityScore:     12/13    → Excellente qualité
2. volumeRatio:      2.3      → Volume x2.3 (forte participation)
3. atrRatio:         1.0      → Volatilité normale
4. directionalRun:   4        → 4 bougies haussières consécutives
5. alignmentScore:   3        → Toutes les EMA alignées
6. marketType:       +2       → BULL FORT confirmé ✅
7. trend1:           +1       → Court terme haussier
8. trend2:           +1       → Moyen terme haussier
9. trend3:           +1       → Long terme haussier
```

**Interprétation** :
- 🟢 **Action** : **ACHAT fort** avec SL serré
- 🎯 **Probabilité** : Très élevée (score 12/13 + toutes tendances alignées)
- 📊 **Stratégie** : Momentum trading / Scalping haussier

---

### Exemple 2 : Signal à Éviter ❌

```
1. qualityScore:     8/13     → Qualité moyenne
2. volumeRatio:      0.7      → Volume faible (30% sous moyenne)
3. atrRatio:         1.8      → Volatilité élevée (risque)
4. directionalRun:   2        → Pas de momentum clair
5. alignmentScore:   1        → Une seule EMA alignée
6. marketType:       0        → RANGE/Neutre ⚠️
7. trend1:           +1       → Court terme haussier
8. trend2:           -1       → Moyen terme BAISSIER (conflit!)
9. trend3:           0        → Long terme neutre
```

**Interprétation** :
- 🔴 **Action** : **ÉVITER** - Signaux contradictoires
- ⚠️ **Problème** : Tendances opposées (CT hausse, MT baisse)
- 📊 **Stratégie** : Attendre clarification du marché

---

### Exemple 3 : Signal de Vente ⬇️

```
1. qualityScore:     11/13    → Haute qualité
2. volumeRatio:      1.9      → Volume élevé
3. atrRatio:         0.9      → Volatilité normale
4. directionalRun:   5        → 5 bougies baissières consécutives
5. alignmentScore:   3        → Toutes les EMA alignées
6. marketType:       -2       → BEAR FORT confirmé ✅
7. trend1:           -1       → Court terme baissier
8. trend2:           -1       → Moyen terme baissier
9. trend3:           -1       → Long terme baissier
```

**Interprétation** :
- 🔴 **Action** : **VENTE/SHORT** avec confirmation
- 🎯 **Probabilité** : Très élevée (score 11/13 + bear fort)
- 📊 **Stratégie** : Momentum baissier / Short selling

---

## 💡 Stratégies d'Utilisation

### 1. Trading de Momentum (Scalping/Intraday)

**Objectif** : Capturer les mouvements forts intraday

**Filtres** :
- `qualityScore >= 9`
- `marketType = +2` (bull fort) OU `marketType = -2` (bear fort)
- `directionalRun >= 3`

**Entrée** :
- Bull fort (+2) → Position LONG
- Bear fort (-2) → Position SHORT

**Stop-Loss** : Basé sur ATR (ex: 1.5 x ATR)

---

### 2. Trading Directionnel Simplifié

**Objectif** : Ne trader que dans UN sens (LONG ou SHORT)

**Pour LONG uniquement** :
- Filtrer `marketType >= +1`
- Entrée sur pullback ou cassure
- Stop sous dernier bas

**Pour SHORT uniquement** :
- Filtrer `marketType <= -1`
- Entrée sur retracement ou cassure
- Stop au-dessus dernier haut

---

### 3. Range Trading (Support/Résistance)

**Objectif** : Profiter des oscillations en range

**Filtres** :
- `marketType = 0` (neutre)
- `qualityScore >= 7`
- Identifier supports/résistances

**Stratégie** :
- Achat au support + confirmation
- Vente à la résistance + confirmation
- Stops serrés hors de la range

---

### 4. Trading de Qualité Pure

**Objectif** : Trader uniquement les setups parfaits

**Filtres** :
- `qualityScore >= 11`
- `alignmentScore = 3`
- Ignorer la direction initialement

**Entrée** :
- Suivre la direction du `marketType`
- Attendre confirmation (volume, pattern)

---

### 5. Gestion de Risque

**Réduction de position** :
- `atrRatio > 1.5` → Réduire taille de 50%
- `volumeRatio < 1.0` → Réduire taille de 30%

**Éviter complètement** :
- `alignmentScore < 2` → Pas de clarté
- `marketType = 0` ET pas de stratégie range
- `qualityScore < 7` → Déjà filtré par défaut

---

## ⚙️ Paramètres Configurables

Tous les paramètres sont dans le fichier `.prt` (lignes 6-13) :

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
```

### Ajuster le seuil de filtrage

**Ligne 304** - Modifier le seuil qualityScore :

```prorealtime
condition = (qualityScore >= 7)  // Changer 7 pour filtrer +/- strict
```

**Exemples** :
- `>= 9` → Très strict, signaux rares mais fiables
- `>= 5` → Plus permissif, beaucoup de résultats
- `>= 11` → Ultra strict, perfection uniquement

### Modifier les colonnes affichées

**Ligne 307** - Personnaliser la sortie SCREENER :

```prorealtime
SCREENER[condition](qualityScore, volumeRatio, atrRatio, directionalRun, alignmentScore, marketType, trend1, trend2, trend3)
```

**Variables disponibles** à ajouter :
- `spreadRatio` - Spread en %
- `vwapDistance` - Distance au VWAP en %
- `bodyWickRatio` - Ratio corps/mèche
- `volumeCV` - Coefficient de variation du volume
- `slippageRatio` - Slippage estimé

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

**Pour changer** : Modifier `emaPeriod1`, `emaPeriod2`, `emaPeriod3` dans les paramètres.

---

## 📊 Métriques Détaillées

### 1. Volume (volumeRatio)
**Calcul** : `volume / AVERAGE[100](volume)`
**Signification** : Participation du marché
**Optimal** : ≥ 1.5 (volume 50% supérieur à la moyenne)

### 2. Spread (spreadRatio)
**Calcul** : `((high - low) / close) * 100`
**Signification** : Coûts de transaction estimés
**Optimal** : < moyenne (spread serré)

### 3. ATR (atrRatio)
**Calcul** : `AverageTrueRange[14] / AVERAGE[100](ATR)`
**Signification** : Volatilité actuelle vs historique
**Optimal** : 0.8 - 1.2 (volatilité normale)

### 4. Corps Bougie (bodyWickRatio)
**Calcul** : `ABS(close - open) / (high - low)`
**Signification** : Force directionnelle
**Optimal** : ≥ 0.5 (corps représente 50%+ de la bougie)

### 5. Chevauchement (bodyOverlapPercent)
**Calcul** : `Overlap actuel / Corps précédent * 100`
**Signification** : Continuation ou hésitation
**Optimal** : 30-70% (continuité modérée)

### 6. Run Directionnel (directionalRun)
**Calcul** : Compte bougies consécutives même direction (max 10)
**Signification** : Momentum et tendance
**Optimal** : ≥ 3 (tendance confirmée)

### 7. VWAP (vwapDistance)
**Calcul** : `((close - vwap) / vwap) * 100`
**Signification** : Position vs prix moyen pondéré
**Optimal** : Distance ≤ 0.5% (proche équilibre)

### 8. Slippage (slippageRatio)
**Calcul** : `spreadRatio / atrPercent`
**Signification** : Slippage potentiel vs volatilité
**Optimal** : < 0.1 (slippage faible)

### 9. Régularité (volumeCV)
**Calcul** : `STD[20](volume) / AVERAGE[100](volume)`
**Signification** : Stabilité du flux de volume
**Optimal** : < 0.5 (flux régulier)

---

## 📝 Notes Importantes

### Limitations Techniques

1. **VWAP se réinitialise chaque jour** (ligne 94)
   - Le calcul redémarre à chaque nouvelle session

2. **Runs directionnels limités à 10 bougies** (lignes 68-86)
   - Maximum analysé : 10 bougies consécutives

3. **Multi-tendance désactivable** (ligne 10)
   - Mettre `enableMTF = 0` pour désactiver les EMA

4. **Filtrage automatique actif** (ligne 304)
   - Seuls les `qualityScore >= 7` s'affichent

5. **Calculs temps réel uniquement**
   - Aucune fonction look-ahead (pas de biais futur)

### Compatibilité

✅ **Compatible avec** :
- ProRealTime V12+
- ProScreener (mode gratuit et premium)
- Tous les instruments (Actions, Indices, Forex, Crypto, Matières premières)
- Tous les timeframes (1min à Daily)

❌ **Non compatible avec** :
- ProRealTime V11 et antérieur (syntaxe différente)
- ProBacktest (ce n'est pas un backtest, c'est un screener)

---

## 🔍 Dépannage

### Problème : Aucun résultat

**Solutions** :
1. Réduire le seuil : `condition = (qualityScore >= 5)` (ligne 304)
2. Vérifier la watchlist : Contient-elle des instruments actifs ?
3. Vérifier le timeframe : Essayer 5min ou 15min
4. Augmenter `lookbackPeriod` à 200

### Problème : Trop de résultats

**Solutions** :
1. Augmenter le seuil : `condition = (qualityScore >= 9)`
2. Filtrer par marketType : Ajouter `AND ABS(marketType) >= 1`
3. Réduire la watchlist : Sélectionner moins d'instruments

### Problème : Erreur de syntaxe

**Solutions** :
1. Vérifier que TOUT le code est copié (308 lignes)
2. Vérifier qu'aucun caractère spécial n'est altéré
3. Copier-coller à nouveau depuis le fichier source
4. Vérifier version ProRealTime (V12+ requis)

### Problème : Valeurs aberrantes

**Vérifications** :
- `atrRatio` > 5 → Probable gap ou événement exceptionnel
- `volumeRatio` > 10 → Volume anormal (news, annonce)
- `directionalRun` = 10 → Maximum atteint, tendance très forte
- `marketType` oscille → Marché en indécision

---

## 📚 Documentation Complémentaire

### Fichiers du Projet

1. **`trading_quality_metrics_v2_FINAL.prt`** (308 lignes)
   - Code source ProScreener V2.1

2. **`LEGENDE_CRITERES.md`**
   - Documentation détaillée des 9 critères
   - Exemples concrets
   - Stratégies avancées

3. **`README.md`** (ce fichier)
   - Guide d'installation et utilisation
   - Vue d'ensemble du projet

### Ressources Externes

- [Documentation ProRealTime](https://www.prorealtime.com/fr/support)
- [Forum ProRealCode](https://www.prorealcode.com/forum/)
- [Langage ProBuilder](https://www.prorealtime.com/fr/probuilder)
- [Guide ProScreener](https://www.prorealtime.com/fr/proscreener)

---

## 📜 Changelog

### Version 2.2 (2025-10-26) - Actuelle

**📝 Améliorations de Nomenclature** :
- ✅ **En-tête détaillé** : Légende complète des 9 colonnes dans le code source
- ✅ **Noms explicites** : Chaque critère nommé clairement (qualityScore, volumeRatio, etc.)
- ✅ **Commentaires enrichis** : Documentation inline pour meilleure lisibilité
- ✅ **Légende marketType** : Ajout de la signification directement dans le code

**Objectif** :
- Faciliter la compréhension du code pour les utilisateurs
- Clarifier la correspondance colonnes SCREENER ↔ noms de critères
- Améliorer la maintenabilité du script

### Version 2.1 (2025-10-26)

**🆕 Nouveautés** :
- ✅ **Critère `marketType`** : Classification Bull/Bear/Range automatique
- ✅ **9 colonnes** au lieu de 8 (ajout marketType en position 6)
- ✅ **Filtrage directionnel** : Facilite le trading LONG/SHORT uniquement
- ✅ **Documentation enrichie** : LEGENDE_CRITERES.md étendue
- ✅ **Stratégies mises à jour** : Nouvelles stratégies utilisant marketType

**Améliorations** :
- 📊 Décalage trend1/trend2/trend3 vers critères 7/8/9
- 📖 README V2.1 complet rédigé
- 🎯 Exemples mis à jour avec marketType

### Version 2.0 (2025-10-26)

**Réécriture complète** :
- ✅ Compatibilité 100% ProScreener V12
- ✅ Suppression fonctions incompatibles (TIMEFRAME, median, ELSIF)
- ✅ Système EMA multi-tendance (proxy 3 timeframes)
- ✅ Score 0-13 (10 base + 3 bonus)
- ✅ Code épuré (suppression variables inutilisées)
- ✅ 8 colonnes SCREENER

### Version 1.x (archives)

Versions antérieures avec erreurs de syntaxe et incompatibilités.

---

## ⚠️ Avertissements et Disclaimers

### Risques du Trading

- ⚠️ **Le trading comporte des risques** : Vous pouvez perdre tout ou partie de votre capital
- ⚠️ **Aucun système n'est infaillible** : Même un score 13/13 ne garantit pas le profit
- ⚠️ **Gestion du risque obligatoire** : Ne risquez jamais plus de 1-2% par trade
- ⚠️ **Backtesting recommandé** : Testez sur historique avant trading réel
- ⚠️ **Éducation continue** : Formez-vous avant de trader avec argent réel

### Conditions de Marché

- 📉 **Gap et news** : Le screener ne prédit pas les gaps ou annonces
- 📊 **Slippage réel** : Le slippage calculé est une estimation
- 💰 **Frais non inclus** : Commissions, spreads réels non calculés
- ⏰ **Heures de marché** : Privilégier les heures liquides

### Utilisation du Code

- 📝 **Licence éducative** : Code fourni à des fins d'apprentissage
- 🚫 **Aucune garantie** : Fourni "tel quel" sans garantie
- 🔧 **Modifications autorisées** : Vous pouvez adapter selon vos besoins
- 📢 **Partage encouragé** : Vous pouvez partager avec attribution

---

## 🎓 Pour Aller Plus Loin

### Optimisations Possibles

1. **Ajouter des patterns** : Hammer, Engulfing, Doji
2. **Intégrer RSI/MACD** : Confirmation momentum
3. **Détection support/résistance** : Niveaux clés
4. **Stop-Loss/Take-Profit auto** : Calculs basés ATR
5. **Filtres horaires** : Éviter heures creuses

### Backtesting

Pour tester l'efficacité historique :
1. Utiliser ProBacktest (nécessite réécriture en ProBuilder)
2. Exporter résultats screener vers Excel
3. Analyser performances des signaux qualityScore >= 10
4. Calculer win rate par marketType

### Automatisation

Possibilités avec ProOrder (compte réel uniquement) :
- Entrées automatiques sur `qualityScore >= 11`
- Filtrage par `marketType` selon stratégie
- Stops basés sur `atrRatio`

---

## 💬 Support et Contact

### Problèmes ou Questions ?

1. **Vérifiez la section Dépannage** ci-dessus
2. **Consultez LEGENDE_CRITERES.md** pour détails techniques
3. **Forum ProRealCode** pour aide communauté
4. **GitHub Issues** (si applicable) pour bugs/suggestions

### Contributions

Améliorations bienvenues ! Idées :
- Nouveaux critères de qualité
- Optimisations performance
- Stratégies additionnelles
- Traductions

---

## 🏆 Résumé Rapide (TL;DR)

**Ce que fait le screener** :
- ✅ Calcule un score de qualité 0-13 pour chaque instrument
- ✅ Classe automatiquement : Bull Fort/Modéré, Bear Fort/Modéré, Range/Neutre
- ✅ Affiche 9 critères : score, volume, volatilité, momentum, alignement, type marché, 3 tendances

**Comment l'utiliser** :
1. Copier le code `.prt` dans ProScreener
2. Lancer sur timeframe 1 minute
3. Trier par `qualityScore` (colonne 1) décroissant
4. Filtrer par `marketType` (colonne 6) selon stratégie

**Meilleures pratiques** :
- 🎯 Score ≥ 10 + marketType = ±2 → Signaux les plus fiables
- ⚠️ marketType = 0 → Éviter ou faire du range trading
- 📊 Combiner avec analyse technique classique (S/R, patterns)
- 💰 Gestion de risque stricte (max 1-2% par trade)

---

**Version**: 2.2
**Date**: 2025-10-26
**Compatibilité**: ProRealTime V12+ / ProScreener
**Auteur**: Script généré avec Claude Code
**Licence**: Éducatif - Utilisez à vos propres risques

---

**⭐ Si ce screener vous aide, n'hésitez pas à le partager !**

🚀 **Bon trading et que les probabilités soient avec vous !**
