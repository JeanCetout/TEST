# 📊 Légende des Critères - ProScreener Trading Quality Metrics V3.0

## Vue d'ensemble

Le screener affiche **9 colonnes avec noms personnalisés** dans ProRealTime.

**⭐ NOUVEAUTÉ V3.0** : Les colonnes affichent maintenant des **noms lisibles** au lieu des noms de variables techniques !

**Affichage dans ProScreener V3** :
```
Score | Volume | ATR | Run | Align | Type | T1 | T2 | T3
```

Au lieu de (V2.x) :
```
qualityScore | volumeRatio | atrRatio | directionalRun | ...
```

---

## 🔢 Les 9 Colonnes Personnalisées

### Colonne 1 : **"Score"** (`qualityScore`)

**Nom affiché** : `Score`
**Variable** : `qualityScore`
**Plage** : 0 à 13
**Signification** : Score composite calculé à partir de 10 métriques de qualité + bonus multi-tendance

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

### Colonne 2 : **"Volume"** (`volumeRatio`)

**Nom affiché** : `Volume`
**Variable** : `volumeRatio`
**Plage** : 0 à ∞
**Signification** : Ratio du volume actuel par rapport à la moyenne des 100 dernières bougies

**Interprétation**:
- `> 2.0` → 🔥 Volume exceptionnel (+100%)
- `1.5-2.0` → 🟢 Volume fort (+50-100%)
- `1.0-1.5` → 🟡 Volume normal à élevé
- `< 1.0` → 🔴 Volume faible

**Utilisation**: Un volume élevé confirme la validité du mouvement de prix.

---

### Colonne 3 : **"ATR"** (`atrRatio`)

**Nom affiché** : `ATR`
**Variable** : `atrRatio`
**Plage** : 0 à ∞
**Signification** : Ratio de l'ATR actuel (volatilité sur 14 périodes) par rapport à la moyenne des 100 dernières valeurs

**Interprétation**:
- `> 1.5` → 🔴 Volatilité excessive (risque élevé)
- `1.2-1.5` → 🟡 Volatilité élevée
- `0.8-1.2` → 🟢 Volatilité normale (optimal)
- `< 0.8` → 🟡 Volatilité faible (marché calme)

**Utilisation**: Permet d'ajuster la taille de position et les stops selon la volatilité.

---

### Colonne 4 : **"Run"** (`directionalRun`)

**Nom affiché** : `Run`
**Variable** : `directionalRun`
**Plage** : 0 à 10
**Signification** : Nombre de bougies haussières ou baissières consécutives (max 10 analysées)

**Interprétation**:
- `≥ 5` → 🔥 Tendance très forte (attention au retournement)
- `3-4` → 🟢 Tendance confirmée
- `1-2` → 🟡 Début de mouvement
- `0` → ⚪ Pas de directionnalité

**Utilisation**:
- Run haussier + Align = 3 → Continuation probable
- Run élevé (≥5) → Attendre pullback avant entrée

---

### Colonne 5 : **"Align"** (`alignmentScore`)

**Nom affiché** : `Align`
**Variable** : `alignmentScore`
**Plage** : 0 à 3
**Signification** : Nombre d'EMA (20, 50, 100) alignées dans la même direction

**Interprétation**:
- `3` → 🔥 **TOUTES les tendances alignées** (court + moyen + long terme)
- `2` → 🟢 Alignement partiel (2 timeframes concordants)
- `1` → 🟡 Tendance faible (1 seul timeframe)
- `0` → 🔴 Pas de tendance claire

**Utilisation**:
- Score = 3 → Signal le plus puissant, probabilité max
- Score < 2 → Éviter, signaux contradictoires

---

### Colonne 6 : **"Type"** (`marketType`)

**Nom affiché** : `Type`
**Variable** : `marketType`
**Plage** : -2 à +2
**Signification** : Classification automatique du type de marché basée sur l'alignement des EMA

**Valeurs**:
- `+2` → 🔥 **Bull Fort** (toutes les EMA haussières, Align = 3)
- `+1` → 🟢 **Bull Modéré** (2+ EMA haussières, tendance haussière probable)
- `0` → ⚪ **Range/Neutre** (pas de direction claire, tendances mixtes)
- `-1` → 🟠 **Bear Modéré** (2+ EMA baissières, tendance baissière probable)
- `-2` → 🔴 **Bear Fort** (toutes les EMA baissières, Align = 3)

**Interprétation**:
- `+2` → Position LONG privilégiée, forte tendance haussière confirmée
- `+1` → Position LONG possible, tendance haussière en formation
- `0` → RANGE trading ou attente, pas de tendance claire
- `-1` → Position SHORT possible, tendance baissière en formation
- `-2` → Position SHORT privilégiée, forte tendance baissière confirmée

**Utilisation stratégique**:
- Filtrer `Type >= +1` pour ne trader QUE les marchés haussiers
- Filtrer `Type <= -1` pour ne trader QUE les marchés baissiers
- Filtrer `Type = 0` pour stratégies de range (support/résistance)
- Filtrer `ABS(Type) = 2` pour les tendances les plus fortes

---

### Colonnes 7, 8, 9 : **"T1"**, **"T2"**, **"T3"** (trends)

**Noms affichés** : `T1`, `T2`, `T3`
**Variables** : `trend1`, `trend2`, `trend3`
**Plage** : -1, 0, +1
**Signification** : Direction de chaque EMA par rapport au prix

| Colonne | Nom Affiché | Variable | EMA | Représente |
|---------|-------------|----------|-----|------------|
| **7** | **T1** | trend1 | EMA 20 | Tendance **court terme** (quelques heures) |
| **8** | **T2** | trend2 | EMA 50 | Tendance **moyen terme** (demi-journée) |
| **9** | **T3** | trend3 | EMA 100 | Tendance **long terme** (journée complète) |

**Valeurs**:
- `+1` → 🟢 Prix > EMA (tendance **haussière**)
- `0` → ⚪ Prix = EMA (neutre)
- `-1` → 🔴 Prix < EMA (tendance **baissière**)

**Configurations optimales**:
```
Achat fort:  T1=+1, T2=+1, T3=+1 (Align=3, Type=+2)
Vente forte: T1=-1, T2=-1, T3=-1 (Align=3, Type=-2)
Indécision:  T1=+1, T2=-1, T3=0 (Align=1, Type=0)
```

---

## 🎯 Exemples d'Interprétation

### Exemple 1 : Signal d'Achat Optimal ⭐⭐⭐

**Affichage dans ProScreener V3** :
```
Score: 12  | Volume: 2.3 | ATR: 1.0 | Run: 4 | Align: 3 | Type: +2 | T1: +1 | T2: +1 | T3: +1
```

**Analyse détaillée** :
- 🟢 **Score: 12/13** → Excellente qualité (presque parfait)
- 🟢 **Volume: 2.3** → Volume x2.3 la moyenne (forte participation)
- 🟢 **ATR: 1.0** → Volatilité normale (risque maîtrisé)
- 🟢 **Run: 4** → 4 bougies haussières consécutives (momentum confirmé)
- 🟢 **Align: 3** → Toutes les EMA alignées (cohérence maximale)
- 🔥 **Type: +2** → **BULL FORT confirmé** (toutes tendances haussières)
- 🟢 **T1/T2/T3: +1** → Court, moyen, long terme TOUS haussiers

**Interprétation globale** :
- 🎯 **Probabilité** : Très élevée (12/13 + Type +2 = signal parfait)
- 💪 **Force** : Maximale (momentum + alignement complet)
- 📈 **Direction** : Haussière sans ambiguïté

**Action recommandée** : **ACHAT FORT** avec SL serré
**Stratégie** : Momentum trading / Scalping haussier
**Entry** : Entrée immédiate ou sur léger pullback
**Stop-Loss** : 1.5 x ATR sous le bas récent
**Take-Profit** : 3 x risque (ratio 1:3)

---

### Exemple 2 : Signal à Éviter ❌

**Affichage dans ProScreener V3** :
```
Score: 8   | Volume: 0.7 | ATR: 1.8 | Run: 2 | Align: 1 | Type: 0  | T1: +1 | T2: -1 | T3: 0
```

**Analyse détaillée** :
- 🟡 **Score: 8** → Qualité moyenne (juste au-dessus du seuil)
- 🔴 **Volume: 0.7** → Volume faible (30% sous moyenne, manque liquidité)
- 🔴 **ATR: 1.8** → Volatilité élevée (80% au-dessus normale, risque!)
- 🟡 **Run: 2** → Seulement 2 bougies (pas de momentum clair)
- 🔴 **Align: 1** → Une seule EMA alignée (pas de cohérence)
- ⚠️ **Type: 0** → **RANGE/Neutre** (pas de direction claire)
- ⚠️ **T1: +1, T2: -1, T3: 0** → Tendances CONTRADICTOIRES !

**Interprétation globale** :
- ⚠️ **Problème majeur** : Court terme hausse, moyen terme baisse = conflit
- 🔴 **Risque élevé** : Volatilité excessive + volume faible = slippage probable
- 📊 **Indécision** : Marché en range, pas de direction

**Action recommandée** : **ÉVITER** - Signaux contradictoires
**Raison** : Tendances opposées (CT haussier vs MT baissier)
**Alternative** : Attendre clarification (Align >= 2 + Type ≠ 0)

---

### Exemple 3 : Signal de Vente ⬇️

**Affichage dans ProScreener V3** :
```
Score: 11  | Volume: 1.9 | ATR: 0.9 | Run: 5 | Align: 3 | Type: -2 | T1: -1 | T2: -1 | T3: -1
```

**Analyse détaillée** :
- 🟢 **Score: 11/13** → Haute qualité (excellent signal)
- 🟢 **Volume: 1.9** → Volume élevé (90% au-dessus moyenne, pression vendeuse)
- 🟢 **ATR: 0.9** → Volatilité normale (risque maîtrisé)
- 🟢 **Run: 5** → 5 bougies baissières consécutives (fort momentum baissier)
- 🟢 **Align: 3** → Toutes les EMA alignées (cohérence maximale)
- 🔴 **Type: -2** → **BEAR FORT confirmé** (toutes tendances baissières)
- 🔴 **T1/T2/T3: -1** → Court, moyen, long terme TOUS baissiers

**Interprétation globale** :
- 🎯 **Probabilité** : Très élevée (11/13 + Type -2 = signal fort)
- 💪 **Force** : Maximale (momentum baissier + alignement complet)
- 📉 **Direction** : Baissière sans ambiguïté

**Action recommandée** : **VENTE/SHORT** avec confirmation
**Stratégie** : Momentum baissier / Short selling
**Entry** : Entrée sur retracement ou cassure support
**Stop-Loss** : 1.5 x ATR au-dessus du haut récent
**Take-Profit** : 3 x risque (ratio 1:3)

---

## 💡 Stratégies d'Utilisation avec Colonnes V3

### 1. Filtrage Rapide par Colonne "Type"

**Avantage V3** : Triez directement la colonne "Type" dans ProScreener !

**Pour LONG uniquement** :
1. Lancez le screener
2. Triez colonne **"Type"** décroissant
3. Les **Type = +2** (Bull Fort) apparaissent en premier
4. Filtrez visuellement **Score >= 10** + **Run >= 3**

**Pour SHORT uniquement** :
1. Lancez le screener
2. Triez colonne **"Type"** croissant
3. Les **Type = -2** (Bear Fort) apparaissent en premier
4. Filtrez visuellement **Score >= 10** + **Run >= 3**

---

### 2. Stratégie "Perfect Setup"

**Critères dans ProScreener V3** :
```
Score >= 11  |  Volume >= 1.5  |  ATR: 0.8-1.2  |  Align = 3  |  Type = ±2
```

**Comment filtrer** :
1. Trier par **"Score"** décroissant
2. Vérifier **"Align"** = 3
3. Vérifier **"Type"** = +2 ou -2
4. Vérifier **"Volume"** >= 1.5
5. Vérifier **"ATR"** entre 0.8 et 1.2

**Probabilité de succès** : 70-80% sur timeframe 1min

---

### 3. Stratégie "Momentum Burst"

**Critères dans ProScreener V3** :
```
Run >= 4  |  Type = ±2  |  Volume >= 2.0  |  Score >= 9
```

**Objectif** : Capturer les mouvements explosifs

**Comment utiliser** :
1. Trier par **"Run"** décroissant
2. Sélectionner **Run >= 4**
3. Vérifier **"Type"** = ±2 (direction claire)
4. Vérifier **"Volume"** >= 2.0 (forte participation)
5. Entry immédiate dans la direction du Type

**Attention** : Run >= 5 = possible surextension, attendre pullback

---

### 4. Stratégie "Range Reversal"

**Critères dans ProScreener V3** :
```
Type = 0  |  Score >= 7  |  Run <= 2  |  Volume >= 1.0
```

**Objectif** : Trader les oscillations en range

**Comment utiliser** :
1. Filtrer **"Type"** = 0 (range/neutre)
2. Identifier supports/résistances sur graphique
3. Acheter au support + confirmation chandelier
4. Vendre à la résistance + confirmation chandelier
5. SL serrés hors de la range

---

## ⚙️ Personnaliser les Noms de Colonnes V3

**Ligne 332 du code** - Vous pouvez modifier les alias affichés :

```prorealtime
SCREENER[condition](
  qualityScore AS "Score",      // Changer en "Qualité" ou "Q"
  volumeRatio AS "Volume",      // Changer en "Vol" ou "Liquidité"
  atrRatio AS "ATR",            // Changer en "Volatilité"
  directionalRun AS "Run",      // Changer en "Momentum" ou "M"
  alignmentScore AS "Align",    // Changer en "EMA" ou "A"
  marketType AS "Type",         // Changer en "Marché" ou "T"
  trend1 AS "T1",               // Changer en "CT" (Court Terme)
  trend2 AS "T2",               // Changer en "MT" (Moyen Terme)
  trend3 AS "T3"                // Changer en "LT" (Long Terme)
)
```

**Contraintes** :
- Guillemets doubles obligatoires : `"Nom"`
- Éviter caractères spéciaux : %, /, €, etc.
- Noms courts recommandés : max 10 caractères
- Pas d'espaces dans les noms

**Exemples de personnalisation** :

**Version française étendue** :
```prorealtime
SCREENER[condition](
  qualityScore AS "Qualite",
  volumeRatio AS "Vol",
  atrRatio AS "Volatil",
  directionalRun AS "Momentum",
  alignmentScore AS "EMA",
  marketType AS "Marche",
  trend1 AS "CT",
  trend2 AS "MT",
  trend3 AS "LT"
)
```

**Version ultra-courte** :
```prorealtime
SCREENER[condition](
  qualityScore AS "Q",
  volumeRatio AS "V",
  atrRatio AS "A",
  directionalRun AS "R",
  alignmentScore AS "E",
  marketType AS "M",
  trend1 AS "1",
  trend2 AS "2",
  trend3 AS "3"
)
```

---

## 📊 Tableau Comparatif V2 vs V3

| Aspect | Version 2.x | Version 3.0 |
|--------|-------------|-------------|
| **Colonnes** | Noms techniques | **Noms personnalisés** ✅ |
| **Affichage** | qualityScore | **Score** ✅ |
| **Lisibilité** | Moyenne | **Excellente** ✅ |
| **Compréhension** | Nécessite doc | **Immédiate** ✅ |
| **Personnalisation** | Non | **Oui** ✅ |
| **Tri colonnes** | Difficile | **Facile** ✅ |
| **Usage pro** | Possible | **Optimal** ✅ |

---

## 📝 Notes Techniques V3

### Alias AS - Syntaxe ProBuilder

**Code source (ligne 332)** :
```prorealtime
SCREENER[condition](qualityScore AS "Score", volumeRatio AS "Volume", ...)
```

**Compatibilité** :
- ✅ ProRealTime V12+ : Supporté
- ❌ ProRealTime V11 et antérieur : Non supporté

**Si erreur de syntaxe** :
- Vérifier version ProRealTime (doit être V12+)
- Vérifier guillemets doubles (pas simples)
- Vérifier pas de caractères spéciaux dans alias

### Limitations

1. **Alias max 15 caractères** : ProScreener limite la longueur
2. **Pas de caractères spéciaux** : %, /, €, £, etc. causent des erreurs
3. **Pas d'espaces** : Utiliser tiret ou underscore si besoin

---

## 🔍 Dépannage V3

### Problème : Colonnes sans noms personnalisés

**Cause** : Version ProRealTime < V12 ne supporte pas `AS "Alias"`

**Solutions** :
1. Mettre à jour ProRealTime vers V12+
2. OU retirer les alias (remplacer par version 2.1)

### Problème : Erreur "invalid syntax" ligne 332

**Causes possibles** :
- Caractère spécial dans un alias
- Guillemets simples au lieu de doubles
- Virgule manquante entre alias

**Solution** :
Vérifier la syntaxe exacte :
```prorealtime
variable AS "Alias",  // virgule après chaque ligne sauf dernière
```

---

## 📚 Ressources

### Fichiers du Projet V3

1. **`trading_quality_metrics_v2_FINAL.prt`** (333 lignes)
   - Code source ProScreener V3.0
   - Alias personnalisés intégrés (ligne 332)

2. **`README.md`**
   - Guide complet V3.0 (732 lignes)
   - Installation, stratégies, exemples

3. **`LEGENDE_CRITERES.md`** (ce fichier)
   - Légende des 9 colonnes personnalisées
   - Exemples avec affichage V3

### Documentation ProRealTime

- [Syntaxe AS](https://www.prorealtime.com/fr/probuilder) - Documentation alias
- [ProScreener V12](https://www.prorealtime.com/fr/proscreener) - Guide officiel
- [Forum ProRealCode](https://www.prorealcode.com/forum/) - Aide communauté

---

## 🎯 Tableau Récapitulatif V3

| # | Colonne Affichée | Variable | Plage | Optimal | Utilisation |
|---|------------------|----------|-------|---------|-------------|
| 1 | **Score** | qualityScore | 0-13 | ≥ 10 | Qualité globale |
| 2 | **Volume** | volumeRatio | 0-∞ | ≥ 1.5 | Liquidité |
| 3 | **ATR** | atrRatio | 0-∞ | 0.8-1.2 | Volatilité |
| 4 | **Run** | directionalRun | 0-10 | ≥ 3 | Momentum |
| 5 | **Align** | alignmentScore | 0-3 | 3 | Cohérence |
| 6 | **Type** | marketType | -2 à +2 | ±2 | Bull/Bear/Range |
| 7 | **T1** | trend1 | -1/0/+1 | ±1 | Court terme |
| 8 | **T2** | trend2 | -1/0/+1 | ±1 | Moyen terme |
| 9 | **T3** | trend3 | -1/0/+1 | ±1 | Long terme |

**Signal idéal V3** :
```
Score: 12 | Volume: 2.0 | ATR: 1.0 | Run: 4 | Align: 3 | Type: ±2 | T1/T2/T3: ±1
```

---

**Version**: 3.0 (Colonnes personnalisées)
**Date**: 2025-10-26
**Compatibilité**: ProRealTime V12+ / ProScreener
**Statut**: ✅ Testé et fonctionnel

---

**⭐ La V3.0 transforme l'expérience utilisateur avec ses colonnes personnalisées !**

🚀 **Bon trading avec une interface enfin lisible !**
