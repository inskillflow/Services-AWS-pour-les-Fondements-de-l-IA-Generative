# Question de l'examen — Tailwind : margin/padding vs gap

**Énoncé** : Expliquez **quand privilégier** les classes de **marge / padding** (`m-*`, `p-*`) **vs** les classes `gap-*` sur un conteneur flex ou grid, et proposez **un critère simple** de choix (**espacement interne/extérieur** vs **espacement entre éléments**).

> **Consigne générale (obligatoire)** : **vous devez produire 6 prompts** (A→F) **sans écrire de réponses de contenu**.
> Après **chaque prompt**, **renseignez** le tableau des **paramètres estimés** (*temperature, max_tokens, top_p, frequency_penalty, presence_penalty*).
> **Interdits** : listes à puces dans les réponses attendues, blocs de code, exemples hors consigne.

---

### Prompt A — très factuel, court (1 phrase)

> **Une seule phrase de 25–40 mots**, **factuelle** et **vocabulaire simple** : dites **quand** choisir `m-*`/`p-*` plutôt que `gap-*` sur un conteneur, et énoncez **un critère clair** (**espacement autour/dedans** vs **espacement entre éléments**). **Sans liste. Sans code.**

**Votre prompt A (écrivez ici) :**

---

---

---

#### Estimation des paramètres

| Test | temperature | max_tokens | top_p | frequency_penalty | presence_penalty | But attendu                         |
| ---- | ----------- | ---------- | ----: | ----------------: | ---------------: | ----------------------------------- |
| A    |             |            |       |                   |                  | 1 phrase, factuel, clair (25–40 m.) |

<br/>

### Prompt B — factuel, développé (120–160 mots)

> **120–160 mots**, **ton académique**, **vocabulaire simple** : définissez les classes `m-*`/`p-*` comme **espacement externe/interne d’un bloc**, définissez `gap-*` comme **espacement régulier entre enfants** d’un conteneur flex/grid, exposez **le critère interne/extérieur vs entre éléments**, puis l’**impact** sur **maintenance** et **évolutivité**. **Sans liste. Sans code.**

**Votre prompt B (écrivez ici) :**

---

---

---

---

---

#### Estimation des paramètres

| Test | temperature | max_tokens | top_p | frequency_penalty | presence_penalty | But attendu                                |
| ---- | ----------- | ---------- | ----: | ----------------: | ---------------: | Définition + critère + impact (120–160 m.) |

<br/>

### Prompt C — bref + nuance (1 phrase, 30–50 mots)

> **30–50 mots**, **une seule phrase** : résumez `m-*`/`p-*` pour **contrôler l’espace d’un élément isolé** et `gap-*` pour **espacer de façon uniforme une série d’enfants**, avec **une nuance** (par exemple : limites de `gap-*` hors flex/grid). **Sans liste. Sans code.**

**Votre prompt C (écrivez ici) :**

---

---

#### Estimation des paramètres

| Test | temperature | max_tokens | top_p | frequency_penalty | presence_penalty | But attendu                                |
| ---- | ----------- | ---------- | ----: | ----------------: | ---------------: | 1 phrase, 30–50 mots, + nuance obligatoire |

<br/>

### Prompt D — créatif mais court (1 phrase)

> **Une phrase de 25–40 mots**, **style créatif mais précis** : utilisez **une métaphore** opposant **margin/padding** (espace “personnel” d’un bloc) et **gap** (intervalle régulier entre voisins), et énoncez **un critère simple** (**espacement de l’élément** vs **espacement du groupe**). **Sans liste. Sans code.**

**Votre prompt D (écrivez ici) :**

---

---

#### Estimation des paramètres

| Test | temperature | max_tokens | top_p | frequency_penalty | presence_penalty | But attendu                          |
| ---- | ----------- | ---------- | ----: | ----------------: | ---------------: | 1 phrase, créatif, critère explicite |

<br/>

### Prompt E — créatif, développé (150–200 mots)

> **150–200 mots**, **style développé et nuancé** : comparez `m-*`/`p-*` à `gap-*` dans un conteneur flex/grid, mentionnez le **risque de “surcharger” les enfants en marges dispersées**, expliquez en quoi `gap-*` simplifie les grilles ou listes régulières, fournissez **un contre-exemple** (utilisation abusive de marges individuelles pour simuler un espacement global), puis donnez **un critère opératoire** pour choisir l’un ou l’autre. **Sans liste. Sans code.**

**Votre prompt E (écrivez ici) :**

---

---

---

---

---

---

#### Estimation des paramètres

| Test | temperature | max_tokens | top_p | frequency_penalty | presence_penalty | But attendu                                                      |
| ---- | ----------- | ---------- | ----: | ----------------: | ---------------: | Comparaison + contre-exemple + critère opératoire (150–200)     |

<br/>

### Prompt F — créatif + éviter répétitions (150–200 mots)

> **150–200 mots**, **style créatif et varié** : proposez une **stratégie hybride** où `gap-*` structure l’**espacement global** d’un ensemble (liste, grille) tandis que `m-*`/`p-*` affinent quelques éléments particuliers, **évitez les redites**, citez **une mauvaise pratique** (empilement de marges contradictoires), et formulez **une règle simple** de décision pour un projet Tailwind réel. **Sans liste. Sans code.**

**Votre prompt F (écrivez ici) :**

---

---

---

---

---

---

#### Estimation des paramètres

| Test | temperature | max_tokens | top_p | frequency_penalty | presence_penalty | But attendu                                                 |
| ---- | ----------- | ---------- | ----: | ----------------: | ---------------: | Stratégie hybride, anti-redite, mauvaise pratique (150–200) |

<br/>

### (Optionnel) Prompt G — modèle avec exigences explicites (Tailwind : margin/padding vs gap)

> **Rédigez un prompt d’examen “modèle”** (pas la réponse) qui impose :
> – une **longueur précise** (25–40 **ou** 120–160 **ou** 150–200 mots),
> – un **ton** (factuel académique **ou** créatif précis),
> – des **interdits** (**sans liste**, **sans bloc de code**),
> – et qui demande d’expliquer **quand utiliser `m-*`/`p-*` plutôt que `gap-*`**, avec **un critère clair** basé sur le type d’espacement (élément individuel vs groupe).

**Votre prompt G (écrivez ici) :**

---

---

---

---

#### Estimation des paramètres

| Test | temperature | max_tokens | top_p | frequency_penalty | presence_penalty | But attendu                                         |
| ---- | ----------- | ---------- | ----: | ----------------: | ---------------: | Prompt méta conforme (exigences claires, sans code) |

<br/>

# Résumé - Question unique — Tailwind : margin/padding vs gap

**Énoncé** : Expliquez **quand privilégier** les classes de **marge/padding** (`m-*`, `p-*`) **vs** `gap-*` sur un conteneur flex/grid, et proposez **un critère simple** de choix (**espacement de l’élément** vs **espacement du groupe**).

> **Consigne générale :** pour **cette question**, **vous devez produire 6 prompts** (A→F) ci-dessus **sans écrire de réponses**.
> **Après chaque prompt, vous renseignez** le petit tableau des **paramètres estimés** (*temperature, max_tokens, top_p, frequency_penalty, presence_penalty*).

### Prompt A — très factuel, court (1 phrase)

..........

### Prompt B — factuel, développé (120–160 mots)

............

### Prompt C — bref + nuance (1 phrase, 30–50 mots)

..........

### Prompt D — créatif mais court (1 phrase)

..........

### Prompt E — créatif, développé (150–200 mots)

.............

### Prompt F — créatif + éviter répétitions (150–200 mots)

............

### Prompt G — modèle avec exemples super clairs (Tailwind : margin/padding vs gap)

............
