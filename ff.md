

# Exemple:

**Question à traiter :**
**1.1 Définitions (6 pts)** — *Balise sémantique (ex. `<header>`) :* …



### Test A — très factuel, court

**Prompt A (à coller) :**

> Réponds **en une seule phrase de 25–40 mots**, **factuelle**, **vocabulaire simple**. Donne **une définition** d’une **balise sémantique** en HTML en citant **`<header>`**. **Aucune liste, aucun code** autre que la balise mentionnée, **aucun exemple supplémentaire**.

| Test | temperature | max_tokens | top_p | frequency_penalty | presence_penalty | But attendu                     |
| ---- | ----------- | ---------- | ----: | ----------------: | ---------------: | ------------------------------- |
| A    | 0.1         | 80         |   1.0 |               0.0 |              0.0 | Très factuel, concis (1 phrase) |



### Test B — factuel, plus développé

**Prompt B (à coller) :**

> Donne **une définition précise** d’une **balise sémantique** en HTML avec **`<header>`**, en **120–160 mots**. **Pas de listes**, **pas de digressions** ; **ton académique**, **vocabulaire simple** ; mentionne **structure du document**, **accessibilité** et **SEO**.

| Test | temperature | max_tokens | top_p | frequency_penalty | presence_penalty | But attendu                       |
| ---- | ----------- | ---------- | ----: | ----------------: | ---------------: | --------------------------------- |
| B    | 0.1         | 220        |   1.0 |               0.0 |              0.0 | Factuel, plus long (120–160 mots) |



### Test C — équilibré avec une nuance

**Prompt C (à coller) :**

> Explique **brièvement** ce qu’est une **balise sémantique** en HTML, en **30–50 mots**, avec **`<header>`** comme exemple **et une nuance** (différence avec `<div>` **ou** mise en garde courante). **Une seule phrase**, **sans liste**.

| Test | temperature | max_tokens | top_p | frequency_penalty | presence_penalty | But attendu                  |
| ---- | ----------- | ---------- | ----: | ----------------: | ---------------: | ---------------------------- |
| C    | 0.5         | 120        |   0.9 |               0.0 |              0.1 | Équilibré, ajoute une nuance |



### Test D — créatif mais court

**Prompt D (à coller) :**

> **Une seule phrase** (25–40 mots), **style plus libre/créatif** : définis une **balise sémantique** en HTML à partir de **`<header>`**, en **mettant l’accent sur le sens** plutôt que le style. **Sans liste**, **sans code** additionnel.


| Test | temperature | max_tokens | top_p | frequency_penalty | presence_penalty | But attendu                                |
| ---- | ----------- | ---------- | ----: | ----------------: | ---------------: | ------------------------------------------ |
| D    | 0.9         | 90         |   1.0 |               0.2 |              0.0 | Créatif mais court, limite les répétitions |


### Test E — créatif, développé

**Prompt E (à coller) :**

> **150–200 mots**, **style développé et nuancé** : explique la **balise sémantique** en HTML avec **`<header>`** comme exemple principal ; **compare** brièvement à `<div>`, mentionne **accessibilité** et **SEO**, donne **un contre-exemple d’usage**. **Sans listes**.


| Test | temperature | max_tokens | top_p | frequency_penalty | presence_penalty | But attendu                       |
| ---- | ----------- | ---------- | ----: | ----------------: | ---------------: | --------------------------------- |
| E    | 0.9         | 230        |   1.0 |               0.0 |              0.1 | Créatif, développé (150–200 mots) |


### Test F — créatif + éviter répétitions

**Prompt F (à coller) :**

> **150–200 mots**, **style créatif et varié** : explique la **balise sémantique** avec **`<header>`**, **évite les répétitions**, propose **idées nouvelles/nuancées**, mentionne **accessibilité** et **SEO**, et **une mauvaise pratique fréquente**. **Sans listes**.


| Test | temperature | max_tokens | top_p | frequency_penalty | presence_penalty | But attendu                           |
| ---- | ----------- | ---------- | ----: | ----------------: | ---------------: | ------------------------------------- |
| F    | 0.95        | 260        |  0.85 |               0.3 |              0.3 | Très créatif, varié, réduit la redite |

#### Rappel express à mettre en haut du chat (optionnel, pour simuler les “paramètres”)

* A/B (style “température basse”) : « **Réponse factuelle, une phrase (ou 120–160 mots), vocabulaire simple.** »
* C : « **Bref + une nuance.** »
* D/E/F (style “température haute”) : « **Développe, compare, nuances, exemples/contre-exemples, évite les répétitions.** »












