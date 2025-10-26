# 📊 Légende des Critères - ProScreener Trading Quality Metrics V2.0

## Vue d'ensemble

Le screener affiche **8 colonnes** numérotées de 1 à 8 dans ProRealTime. Voici leur signification exacte.

---

## 🔢 Colonnes du Screener

### Critère 1 : `qualityScore` - Score Global de Qualité
**Plage**: 0 à 13
**Signification**: Score composite calculé à partir de 10 métriques de qualité + bonus multi-tendance

**Calcul détaillé** (10 points de base):
- ✅ Volume ≥ Moyenne → +1 point
- ✅ Spread < Moyenne → +1 point
- ✅ Corps bougie ≥ 50% → +1 point
- ✅ Run directionnel ≥ 3 bougies → +1 point
- ✅ Distance VWAP ≤ 0.5% → +1 point
- ✅ Slippage faible (< 10%) → +1 point
- ✅ Flux régulier (CV < 0.5) → +1 point
- ✅ ATR normal (0.8-1.2x moyenne) → +1 point
- ✅ Chevauchement corps 30-70% → +1 point
- ✅ Volume fort (≥ 1.5x moyenne) → +1 point

**Bonus Multi-Tendance** (+3 points max):
- 🎯 3 EMA alignées + force > 0.5% → +2 points
- 🎯 2 EMA alignées + force > 0.3% → +1 point
- 🎯 Force moyenne > 1.0% → +1 point

**Interprétation**:
- `≥ 10` → 🟢 Signal haute qualité
- `7-9` → 🟡 Signal acceptable (seuil par défaut)
- `< 7` → 🔴 Non affiché (filtré)

---

### Critère 2 : `volumeRatio` - Volume/Moyenne
**Plage**: 0 à ∞
**Signification**: Ratio du volume actuel par rapport à la moyenne des 100 dernières bougies

**Interprétation**:
- `> 2.0` → 🔥 Volume exceptionnel (+100%)
- `1.5-2.0` → 🟢 Volume fort (+50-100%)
- `1.0-1.5` → 🟡 Volume normal à élevé
- `< 1.0` → 🔴 Volume faible

**Utilisation**: Un volume élevé confirme la validité du mouvement de prix.

---

### Critère 3 : `atrRatio` - ATR Actuel/ATR Moyen
**Plage**: 0 à ∞
**Signification**: Ratio de l'ATR actuel (volatilité sur 14 périodes) par rapport à la moyenne des 100 dernières valeurs

**Interprétation**:
- `> 1.5` → 🔴 Volatilité excessive (risque élevé)
- `1.2-1.5` → 🟡 Volatilité élevée
- `0.8-1.2` → 🟢 Volatilité normale (optimal)
- `< 0.8` → 🟡 Volatilité faible (marché calme)

**Utilisation**: Permet d'ajuster la taille de position et les stops selon la volatilité.

---

### Critère 4 : `directionalRun` - Bougies Consécutives
**Plage**: 0 à 10
**Signification**: Nombre de bougies haussières ou baissières consécutives (max 10 analysées)

**Interprétation**:
- `≥ 5` → 🔥 Tendance très forte (attention au retournement)
- `3-4` → 🟢 Tendance confirmée
- `1-2` → 🟡 Début de mouvement
- `0` → ⚪ Pas de directionnalité

**Utilisation**:
- Run haussier + alignmentScore = 3 → Continuation probable
- Run élevé (≥5) → Attendre pullback avant entrée

---

### Critère 5 : `alignmentScore` - Alignement Multi-Tendance
**Plage**: 0 à 3
**Signification**: Nombre d'EMA (20, 50, 100) alignées dans la même direction

**Interprétation**:
- `3` → 🔥 **TOUTES les tendances alignées** (court + moyen + long terme)
- `2` → 🟢 Alignement partiel (2 timeframes concordants)
- `1` → 🟡 Tendance faible (1 seul timeframe)
- `0` → 🔴 Pas de tendance claire

**Utilisation**:
- Score = 3 → Signal le plus puissant, probabilité max
- Score < 2 → Éviter, signaux contradictoires

---

### Critères 6, 7, 8 : `trend1`, `trend2`, `trend3` - Tendances EMA
**Plage**: -1, 0, +1
**Signification**: Direction de chaque EMA par rapport au prix

| Critère | EMA | Représente |
|---------|-----|------------|
| **6** | EMA 20 | Tendance **court terme** (quelques heures) |
| **7** | EMA 50 | Tendance **moyen terme** (demi-journée) |
| **8** | EMA 100 | Tendance **long terme** (journée complète) |

**Valeurs**:
- `+1` → 🟢 Prix > EMA (tendance **haussière**)
- `0` → ⚪ Prix = EMA (neutre)
- `-1` → 🔴 Prix < EMA (tendance **baissière**)

**Configurations optimales**:
```
Achat fort:  trend1=+1, trend2=+1, trend3=+1 (alignmentScore=3)
Vente forte: trend1=-1, trend2=-1, trend3=-1 (alignmentScore=3)
Indécision:  trend1=+1, trend2=-1, trend3=0 (alignmentScore=1)
```

---

## 🎯 Exemples d'Interprétation

### Exemple 1 : Signal d'Achat Optimal ⭐⭐⭐
```
Critère 1 (qualityScore):     12
Critère 2 (volumeRatio):      2.3
Critère 3 (atrRatio):         1.0
Critère 4 (directionalRun):   4
Critère 5 (alignmentScore):   3
Critère 6 (trend1):           +1
Critère 7 (trend2):           +1
Critère 8 (trend3):           +1
```

**Analyse**:
- Score 12/13 → Excellente qualité
- Volume x2.3 → Forte participation
- ATR normal → Risque maîtrisé
- 4 bougies haussières → Momentum confirmé
- Toutes EMA haussières → Tendance claire sur tous timeframes
- **ACTION**: Achat fort avec SL serré

---

### Exemple 2 : Signal à Éviter ❌
```
Critère 1 (qualityScore):     8
Critère 2 (volumeRatio):      0.7
Critère 3 (atrRatio):         1.8
Critère 4 (directionalRun):   2
Critère 5 (alignmentScore):   1
Critère 6 (trend1):           +1
Critère 7 (trend2):           -1
Critère 8 (trend3):           0
```

**Analyse**:
- Score 8 → Qualité moyenne
- Volume faible (0.7x) → Pas de conviction
- ATR élevé (1.8x) → Forte volatilité, risque
- Seulement 2 bougies → Pas de momentum
- Tendances contradictoires (CT haussier, MT baissier)
- **ACTION**: Éviter, attendre clarification

---

### Exemple 3 : Signal de Vente ⬇️
```
Critère 1 (qualityScore):     11
Critère 2 (volumeRatio):      1.9
Critère 3 (atrRatio):         0.9
Critère 4 (directionalRun):   5
Critère 5 (alignmentScore):   3
Critère 6 (trend1):           -1
Critère 7 (trend2):           -1
Critère 8 (trend3):           -1
```

**Analyse**:
- Score 11/13 → Haute qualité
- Volume élevé → Pression vendeuse confirmée
- 5 bougies baissières → Fort momentum
- Toutes EMA baissières → Tendance baissière claire
- **ACTION**: Vente ou short avec confirmation

---

## ⚙️ Paramètres Configurables

Dans le fichier `.prt`, vous pouvez ajuster (lignes 5-13):

```prorealtime
lookbackPeriod = 100    // Période historique pour moyennes
atrPeriod = 14          // Période ATR (standard)
minBodyRatio = 0.5      // Ratio corps/mèche minimum (50%)
minVolRatio = 1.0       // Volume minimum pour bonus
enableMTF = 1           // Active/désactive multi-tendance (1/0)
emaPeriod1 = 20         // EMA court terme
emaPeriod2 = 50         // EMA moyen terme
emaPeriod3 = 100        // EMA long terme
```

**Ligne 284** pour ajuster le seuil de filtrage:
```prorealtime
condition = (qualityScore >= 7)  // Modifier le 7 pour filtrer +/- strict
```

---

## 📈 Stratégies d'Utilisation

### 1. **Trading de Momentum** (Scalping/Day Trading)
- Filtrer: `qualityScore ≥ 9`
- Chercher: `alignmentScore = 3` + `directionalRun ≥ 3`
- Entrée: Dans la direction des trends (+1 ou -1)
- Stop: Basé sur ATR (atrRatio * prix)

### 2. **Retournements de Tendance**
- Filtrer: `directionalRun ≥ 5` (suracheté/survendu)
- Chercher: Divergence (ex: trend1 ≠ trend3)
- Attendre: Confirmation inverse sur critère 4

### 3. **Trading de Qualité Pure**
- Filtrer: `qualityScore ≥ 11`
- Ignorer direction
- Suivre le signal le plus fort (critères 6-7-8)

### 4. **Gestion de Risque**
- `atrRatio > 1.5` → Réduire taille position de 50%
- `volumeRatio < 1.0` → Éviter (manque liquidité)
- `alignmentScore < 2` → Skip (pas de clarté)

---

## 🔧 Timeframe Recommandé

**Optimal**: 1 minute (comme configuré)

**Pourquoi ?**
- Les EMA 20/50/100 représentent ~20min/50min/100min
- Couvre court, moyen, long terme intraday
- Volume et ATR calculés sur base minute

**Adaptations possibles**:
- 5 minutes → Swing trading (ajuster EMA à 10/25/50)
- 15 minutes → Position trading (ajuster EMA à 5/10/20)

---

## 📝 Notes Importantes

1. **Le screener filtre automatiquement** : Seules les valeurs avec `qualityScore ≥ 7` s'affichent (ligne 284)

2. **VWAP se réinitialise chaque jour** : Le calcul redémarre à chaque nouvelle session (ligne 94)

3. **Les runs directionnels** comptent maximum 10 bougies consécutives (lignes 68-86)

4. **Multi-tendance peut être désactivé** : Mettre `enableMTF = 0` pour analyser sans les EMA

5. **Tous les calculs sont temps réel** : Aucune fonction look-ahead, utilisable en live

---

## 📞 Support

Pour modifier les critères affichés, éditer la ligne 287:
```prorealtime
SCREENER[condition](qualityScore, volumeRatio, atrRatio, directionalRun, alignmentScore, trend1, trend2, trend3)
```

Ajouter/retirer des colonnes selon vos besoins (ex: ajouter `spreadRatio`, `vwapDistance`, etc.)

---

**Version**: 2.0 FINAL
**Date**: 2025-10-26
**Compatibilité**: ProRealTime V12+ / ProScreener
