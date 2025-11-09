# Pratique 2 — Rédaction de prompts (HTML & Tailwind)

## 0) Rappel des paramètres (à connaître)

* **temperature** : contrôle la créativité/variabilité. Faible (0.0–0.2) = réponses stables et factuelles ; élevée (≥0.8) = réponses plus libres/variées.
* **max_tokens** : plafond de longueur générée. Trop bas = réponses coupées ; assez haut = permet d’atteindre la longueur demandée.
* **top_p** : nucleus sampling (0–1). Proche de 1 = éventail large ; plus bas = choix plus restreint.
* **frequency_penalty** : pénalise les répétitions exactes. Plus haut = moins de répétitions.
* **presence_penalty** : encourage l’introduction d’idées/mots nouveaux. Plus haut = contenu plus varié.

> Règle d’or : **A/B** → temperature basse, style sobre et précis. **C** → bref + une nuance. **D/E/F** → temperature plus haute, style développé/créatif, comparaisons/contre-exemples, éviter la redite.



## 1) EXEMPLE (format attendu d’un prompt)


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





<br/>

# 2) Consignes globales (obligatoires)

* Pour **chaque question**, fournissez **6 prompts** : **A**, **B**, **C**, **D**, **E**, **F**.
* Respectez strictement ces formats :

  * **A** : 1 phrase, **25–40 mots**, factuel, vocabulaire simple.
  * **B** : **120–160 mots**, ton académique, vocabulaire simple, **sans listes**.
  * **C** : **30–50 mots**, **1 phrase**, **+ une nuance** (mise en garde ou comparaison).
  * **D** : 1 phrase, **25–40 mots**, **style créatif** mais précis.
  * **E** : **150–200 mots**, **développé**, **compare** brièvement, **contre-exemple**, **sans listes**.
  * **F** : **150–200 mots**, **créatif et varié**, **éviter les répétitions**, **idées nouvelles**.
* Interdits récurrents à rappeler dans vos prompts : **pas de listes**, **pas de code** (sauf mention stricte d’une balise), **pas d’exemples hors consigne**.


<br/>

# 3) Énoncés à traiter (écrivez vos prompts A→F pour chacun)

### Q1 — Balises sémantiques

Explique la différence entre **`<header>`**, **`<nav>`**, **`<section>`**, **`<footer>`** et indique **quand éviter `<div>`** à la place.
*(Écris ici tes 6 prompts A→F, en respectant les formats ci-dessus.)*


> Pour chacun des prompts, estimez les paramètres qui ont été utilisés (vous n'êtes pas obligés d'être très précis)

Prompt A : 

| Test | temperature | max_tokens | top_p | frequency_penalty | presence_penalty | But attendu                     |
| ---- | ----------- | ---------- | ----: | ----------------: | ---------------: | ------------------------------- |
| A    | ...         | ...         |   ... |               ... |              ... | Très factuel, concis (1 phrase) |


Prompt B : 

| Test | temperature | max_tokens | top_p | frequency_penalty | presence_penalty | But attendu                     |
| ---- | ----------- | ---------- | ----: | ----------------: | ---------------: | ------------------------------- |
| A    | ...         | ...         |   ... |               ... |              ... | Très factuel, concis (1 phrase) |

etc...




### Q2 — Tailwind : spacing

Différence entre **`m-4`**, **`mx-4`**, **`my-4`**, **`mt-4`** ; donner **un cas concret d’utilisation**.
*(Écris ici tes 6 prompts A→F.)*

### Q3 — Tailwind : responsive (mobile-first)

Que font les préfixes **`sm:`**, **`md:`**, **`lg:`**, **`xl:`** et **comment sont-ils évalués** (mobile-first, min-width, styles progressifs) ?
*(Écris ici tes 6 prompts A→F.)*

### Q4 — Tailwind : Flex vs Grid

Quand privilégier **`flex`/`flex-col`** vs **`grid grid-cols-…`** ? Donne **un critère simple**.
*(Écris ici tes 6 prompts A→F.)*

### Q5 — Couleurs & thème

Explique l’intérêt de **`text-slate-700`** vs **`text-gray-700`** et l’usage de **`dark:`** pour le mode sombre.
*(Écris ici tes 6 prompts A→F.)*

### Q6 — Typographie

Rôle de **`text-base`**, **`text-2xl`**, **`font-semibold`**, **`leading-relaxed`**, **`tracking-wide`** dans la hiérarchie et la lisibilité.
*(Écris ici tes 6 prompts A→F.)*

### Q7 — Utilitaires conditionnels

Que permettent **`hover:`**, **`focus:`**, **`active:`**, **`disabled:`** et quel est **l’ordre de priorité** / chevauchement attendu ?
*(Écris ici tes 6 prompts A→F.)*

