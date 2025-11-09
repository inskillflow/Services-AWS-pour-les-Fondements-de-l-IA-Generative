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



<br/>

# Annexe 1



### Test A — très factuel, court (1 phrase, 25–40 mots)

`<header>` introduit l’en-tête, `<nav>` regroupe la navigation, `<section>` organise un bloc thématique avec titre pertinent, `<footer>` clôt la zone ; on évite `<div>` lorsqu’une balise sémantique décrit déjà précisément le rôle attendu.

**Paramètres suggérés**

| Test | temperature | max_tokens | top_p | frequency_penalty | presence_penalty | But attendu          |
| ---- | ----------: | ---------: | ----: | ----------------: | ---------------: | -------------------- |
| A    |         0.1 |         90 |   1.0 |               0.0 |              0.0 | Très factuel, concis |

### Test B — factuel, développé (120–160 mots, sans listes)

Les balises sémantiques décrivent le **rôle** d’une portion de page. `<header>` porte l’en-tête d’une page ou d’une section, avec éléments introductifs tels que titre ou identité. `<nav>` regroupe des liens formant un système de **navigation** cohérent. `<section>` segmente le contenu en **parties thématiques** identifiables par un en-tête significatif. `<footer>` ferme la page ou la section par des informations de **pied** (auteur, mentions, liens connexes). Les employer améliore la **structure du document**, facilite l’**accessibilité** (repères reconnus par les lecteurs d’écran, navigation par régions) et fournit des **signaux** utiles aux moteurs de recherche, bénéfiques pour l’**SEO**. On évite `<div>` quand une balise nommée exprime déjà l’intention, car `<div>` est neutre sémantiquement : multiplier les `<div>` dilue le sens, complique la maintenance et nuit à la compréhension automatique et humaine de la page.

**Paramètres suggérés**

| Test | temperature | max_tokens | top_p | frequency_penalty | presence_penalty |
| ---- | ----------: | ---------: | ----: | ----------------: | ---------------: |
| B    |         0.1 |        230 |   1.0 |               0.0 |              0.0 |


### Test C — bref + nuance (1 phrase, 30–50 mots)

`<header>`, `<nav>`, `<section>` et `<footer>` indiquent respectivement en-tête, navigation, bloc thématique et pied ; **nuance** : `<div>` est purement structurel et ne doit servir que lorsqu’aucune balise sémantique ne correspond exactement à l’intention de contenu.

**Paramètres suggérés**

| Test | temperature | max_tokens | top_p | frequency_penalty | presence_penalty |
| ---- | ----------: | ---------: | ----: | ----------------: | ---------------: |
| C    |         0.5 |        120 |   0.9 |               0.0 |              0.1 |



### Test D — créatif mais court (1 phrase, 25–40 mots)

Comme un journal : `<header>` installe la manchette, `<nav>` trace les chemins, `<section>` raconte le sujet, `<footer>` signe la fin ; remplace le `<div>` générique dès qu’une balise peut **nommer** clairement le rôle.

**Paramètres suggérés**

| Test | temperature | max_tokens | top_p | frequency_penalty | presence_penalty |
| ---- | ----------: | ---------: | ----: | ----------------: | ---------------: |
| D    |         0.9 |        100 |   1.0 |               0.2 |              0.0 |



### Test E — créatif, développé (150–200 mots, sans listes, avec contre-exemple)

Une page robuste repose sur des **repères** clairs. `<header>` introduit l’identité et le contexte d’une page ou d’une partie ; `<nav>` rassemble les voies d’accès utiles ; `<section>` isole un **sujet** cohérent, accompagné d’un en-tête ; `<footer>` referme la zone avec des informations de contexte. Ces balises n’imposent pas un style : elles **déclarent** un rôle que les technologies d’**accessibilité** reconnaissent, ce qui rend la navigation par régions plus rapide et prévisible. Elles fournissent aussi des **indices** aux moteurs de recherche, qui interprètent mieux l’ossature éditoriale, un atout pour l’**SEO**. **Contre-exemple** : envelopper le menu principal dans un simple `<div>` prive les utilisateurs d’un repère de navigation et empêche certains outils d’annoncer correctement la région ; un `<nav>` aurait rendu le rôle explicite. Principe : choisir la balise qui **nomme** le rôle réel et réserver `<div>` aux cas sans équivalent sémantique.

**Paramètres suggérés**

| Test | temperature | max_tokens | top_p | frequency_penalty | presence_penalty |
| ---- | ----------: | ---------: | ----: | ----------------: | ---------------: |
| E    |         0.9 |        240 |   1.0 |               0.0 |              0.1 |




### Test F — créatif + éviter répétitions (150–200 mots, inclut mauvaise pratique fréquente)

Sur un projet vivant, le CSS peut changer sans altérer le **sens** si la charpente est sémantique : `<header>` cadre, `<nav>` oriente, `<section>` articule les sujets, `<footer>` boucle l’ensemble ; ces repères stabilisent la lecture, la **narration** et la collaboration. Les lecteurs d’écran y gagnent des points d’entrée fiables, et les moteurs de recherche comprennent mieux l’**organisation** éditoriale, ce qui soutient l’**SEO**. Mauvaise pratique fréquente : empiler des `<div>` pour « faire joli » ou utiliser `<section>` sans **titre** pertinent ; on préfère un `<div>` quand aucun en-tête ne qualifie le contenu, afin d’éviter une sémantique **vide**. Autre piège : remplacer `<nav>` par un `<header>` contenant des liens épars, ce qui brouille les repères. Règle simple et durable : **nommer** exactement le rôle avec la balise adéquate et n’employer `<div>` qu’en dernier recours, pour conserver une architecture claire, accessible et facile à maintenir.

**Paramètres suggérés**

| Test | temperature | max_tokens | top_p | frequency_penalty | presence_penalty |
| ---- | ----------: | ---------: | ----: | ----------------: | ---------------: |
| F    |        0.95 |        260 |  0.85 |               0.3 |              0.3 |




<br/>

# Annexe 2 - exemples de réponses - Corrigé Q1 — Balises sémantiques

## Test A — très factuel, court (1 phrase, 25–40 mots)

**Réponse A (modèle)**
`<header>` annonce l’en-tête, `<nav>` regroupe la navigation, `<section>` organise un bloc thématique, `<footer>` clôt la zone ; on **évite `<div>`** quand une balise sémantique décrit déjà le rôle attendu pour structure, accessibilité et SEO.

**Pourquoi c’est correct (justification)** : une seule phrase, vocabulaire simple, différencie clairement les rôles et énonce la règle d’évitement de `<div>` pour raisons structurelles/a11y/SEO.

**Paramètres suggérés**

| Test | temperature | max_tokens | top_p | frequency_penalty | presence_penalty | But attendu          |
| ---- | ----------: | ---------: | ----: | ----------------: | ---------------: | -------------------- |
| A    |         0.1 |         90 |   1.0 |               0.0 |              0.0 | Très factuel, concis |



## Test B — factuel, développé (120–160 mots, sans listes)

**Réponse B (modèle)**
En HTML, les balises sémantiques décrivent le **rôle** d’une zone. `<header>` présente l’en-tête d’une page ou d’une section, souvent avec titre, logo et éléments d’introduction. `<nav>` regroupe des liens de **navigation** cohérents menant vers des pages, ancres ou catégories. `<section>` segmente le contenu en parties **thématiques** ayant un en-tête pertinent, indépendamment de la disposition visuelle. `<footer>` termine une page ou un bloc avec des informations de **pied** : mentions, auteur, liens de contexte. Employer ces balises améliore la **structure du document**, facilite la compréhension par les technologies d’**accessibilité** (repères ARIA implicites, navigation par régions) et fournit des **signaux** clairs aux moteurs de recherche, bénéfiques pour l’indexation et l’**SEO**. On évite `<div>` lorsque l’une de ces balises exprime précisément l’intention, car `<div>` n’apporte pas de **sens** et dilue l’architecture sémantique, ce qui nuit à la robustesse et à la réutilisabilité.

**Justification** : 140–150 mots environ, ton académique, couvre structure/a11y/SEO, pas de listes, pas de digressions.

**Paramètres suggérés**

| Test | temperature | max_tokens | top_p | frequency_penalty | presence_penalty |
| ---- | ----------: | ---------: | ----: | ----------------: | ---------------: |
| B    |         0.1 |        230 |   1.0 |               0.0 |              0.0 |



## Test C — bref + nuance (1 phrase, 30–50 mots)

**Réponse C (modèle)**
`<header>`, `<nav>`, `<section>` et `<footer>` indiquent respectivement en-tête, navigation, bloc thématique et pied ; **nuance** : `<div>` ne porte **aucun sens** et doit être réservé aux cas où **aucune** balise sémantique ne correspond précisément.

**Justification** : une phrase, 35–45 mots, ajoute explicitement la nuance demandée sur `<div>`.

**Paramètres suggérés**

| Test | temperature | max_tokens | top_p | frequency_penalty | presence_penalty |
| ---- | ----------: | ---------: | ----: | ----------------: | ---------------: |
| C    |         0.5 |        120 |   0.9 |               0.0 |              0.1 |



## Test D — créatif mais court (1 phrase, 25–40 mots)

**Réponse D (modèle)**
Pense la page comme un journal : `<header>` ouvre, `<nav>` oriente, `<section>` raconte, `<footer>` conclut ; **remplace** le `<div>` générique dès qu’une balise **porte le sens** attendu, sinon l’histoire perd ses repères.

**Justification** : métaphore brève, reste précis sur le sens, aucune liste, une seule phrase.

**Paramètres suggérés**

| Test | temperature | max_tokens | top_p | frequency_penalty | presence_penalty |
| ---- | ----------: | ---------: | ----: | ----------------: | ---------------: |
| D    |         0.9 |        100 |   1.0 |               0.2 |              0.0 |



## Test E — créatif, développé (150–200 mots, sans listes, avec contre-exemple)

**Réponse E (modèle)**
Une page lisible commence par des **repères** solides : `<header>` installe l’identité et le cadre d’une page ou d’une partie, `<nav>` rassemble les trajets utiles, `<section>` isole un **sujet** cohérent assorti d’un titre, `<footer>` referme le périmètre avec les informations de contexte. Ces balises n’imposent pas un style ; elles **déclarent** une intention que les lecteurs d’écran reconnaissent immédiatement, ce qui fluidifie la navigation par régions et améliore l’**accessibilité**. Elles constituent aussi des **signaux** clairs pour les moteurs de recherche, qui interprètent mieux l’organisation du contenu, donc un bénéfice indirect pour l’**SEO**. **Contre-exemple** : envelopper un menu principal dans un simple `<div>` prive l’utilisateur de repères de navigation, alors qu’un `<nav>` aurait exposé son rôle. Le principe est simple : employer les balises sémantiques lorsqu’elles décrivent **exactement** le rôle prévu et réserver `<div>` aux cas où **aucune** balise nommée ne convient, afin de préserver une architecture de document stable et durable.

**Justification** : 170–190 mots, compare à `<div>`, mentionne accessibilité/SEO, inclut un contre-exemple concret, pas de listes.

**Paramètres suggérés**

| Test | temperature | max_tokens | top_p | frequency_penalty | presence_penalty |
| ---- | ----------: | ---------: | ----: | ----------------: | ---------------: |
| E    |         0.9 |        240 |   1.0 |               0.0 |              0.1 |



## Test F — créatif + éviter répétitions (150–200 mots)

**Réponse F (modèle)**
Dans une maquette, on peut **changer** les couleurs sans toucher au **sens** ; c’est exactement ce que permettent `<header>`, `<nav>`, `<section>` et `<footer>` : fixer des **repères** stables que le CSS habille ensuite. Un document gagne alors en **navigabilité** : le lecteur d’écran saute d’un repère à l’autre, l’outil d’analyse comprend l’ossature, et l’équipe conserve un langage commun. À l’inverse, empiler des `<div>` pour « faire pareil » brouille le rôle des zones, complique les tests et fragilise les refactorings. Mauvaise pratique fréquente : utiliser `<section>` sans **en-tête** pertinent ; on y préfère un simple `<div>` si aucun titre ne **qualifie** le contenu, afin d’éviter une sémantique **vide**. Règle opératoire : choisir la balise qui **nomme** le rôle réel de la zone et ne recourir à `<div>` qu’en absence d’équivalent sémantique, ce qui pérennise l’accessibilité, la qualité éditoriale et la maintenance.

**Justification** : style varié, idées nouvelles (titre requis pour `<section>`), mention d’une mauvaise pratique, évite la redite, 160–190 mots.

**Paramètres suggérés**

| Test | temperature | max_tokens | top_p | frequency_penalty | presence_penalty |
| ---- | ----------: | ---------: | ----: | ----------------: | ---------------: |
| F    |        0.95 |        260 |  0.85 |               0.3 |              0.3 |




