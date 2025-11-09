# Question unique — Tailwind : Flex vs Grid

**Énoncé** : Expliquez **quand privilégier** `flex` / `flex-col` **vs** `grid grid-cols-…` et proposez **un critère simple** de choix.

> **Consigne générale (obligatoire)** : **vous devez produire 6 prompts** (A→F) **sans écrire de réponses de contenu**.
> Après **chaque prompt**, **renseignez** le tableau des **paramètres estimés** (*temperature, max_tokens, top_p, frequency_penalty, presence_penalty*).
> **Interdits** : listes à puces dans les réponses attendues, blocs de code, exemples hors consigne.



### Prompt A — très factuel, court (1 phrase)

> **Une seule phrase de 25–40 mots**, **factuelle** et **vocabulaire simple** : dites **quand** choisir `flex`/`flex-col` plutôt que `grid grid-cols-…` et énoncez **un critère clair** (**1D vs 2D**). **Sans liste. Sans code.**

**Votre prompt A (écrivez ici) :**

---

---

---

#### Estimation des paramètres

| Test | temperature | max_tokens | top_p | frequency_penalty | presence_penalty | But attendu                         |
| ---- | ----------- | ---------- | ----: | ----------------: | ---------------: | ----------------------------------- |
| A    |             |            |       |                   |                  | 1 phrase, factuel, clair (25–40 m.) |



### Prompt B — factuel, développé (120–160 mots)

> **120–160 mots**, **ton académique**, **vocabulaire simple** : définissez `flex` (mise en page **à un axe**) et `grid` (mise en page **à deux dimensions**), exposez **le critère 1D vs 2D**, puis l’**impact** sur **maintenance** et **évolutivité**. **Sans liste. Sans code.**

**Votre prompt B (écrivez ici) :**

---

---

---

---

---

#### Estimation des paramètres

| Test | temperature | max_tokens | top_p | frequency_penalty | presence_penalty | But attendu                                |
| ---- | ----------- | ---------- | ----: | ----------------: | ---------------: | ------------------------------------------ |
| B    |             |            |       |                   |                  | Définition + critère + impact (120–160 m.) |



### Prompt C — bref + nuance (1 phrase, 30–50 mots)

> **30–50 mots**, **une seule phrase** : résumez **Flex pour flux à un axe** et **Grid pour composition 2D**, avec **une nuance** (ex. *Grid* pour gabarits répétitifs, *Flex* pour composants locaux). **Sans liste. Sans code.**

**Votre prompt C (écrivez ici) :**

---

---

#### Estimation des paramètres

| Test | temperature | max_tokens | top_p | frequency_penalty | presence_penalty | But attendu                                |
| ---- | ----------- | ---------- | ----: | ----------------: | ---------------: | ------------------------------------------ |
| C    |             |            |       |                   |                  | 1 phrase, 30–50 mots, + nuance obligatoire |



### Prompt D — créatif mais court (1 phrase)

> **Une phrase de 25–40 mots**, **style créatif mais précis** : utilisez **une métaphore** opposant **Flex** (file/ligne/colonne fluide) et **Grid** (damier/gabarit), et énoncez **un critère simple** (**1D vs 2D**). **Sans liste. Sans code.**

**Votre prompt D (écrivez ici) :**

---

---

#### Estimation des paramètres

| Test | temperature | max_tokens | top_p | frequency_penalty | presence_penalty | But attendu                          |
| ---- | ----------- | ---------- | ----: | ----------------: | ---------------: | ------------------------------------ |
| D    |             |            |       |                   |                  | 1 phrase, créatif, critère explicite |

---

### Prompt E — créatif, développé (150–200 mots)

> **150–200 mots**, **style développé et nuancé** : comparez `flex`/`flex-col` à `grid grid-cols-*`, mentionnez **`flex-wrap`** vs **`grid auto-fit/auto-fill`**, fournissez **un contre-exemple** d’usage inadapté (Flex forcé pour grille 2D), puis donnez **un critère opératoire**. **Sans liste. Sans code.**

**Votre prompt E (écrivez ici) :**

---

---

---

---

---

---

#### Estimation des paramètres

| Test | temperature | max_tokens | top_p | frequency_penalty | presence_penalty | But attendu                                                      |
| ---- | ----------- | ---------- | ----: | ----------------: | ---------------: | ---------------------------------------------------------------- |
| E    |             |            |       |                   |                  | Comparaison + wrap/auto-fit + contre-exemple + critère (150–200) |

---

### Prompt F — créatif + éviter répétitions (150–200 mots)

> **150–200 mots**, **style créatif et varié** : proposez une **stratégie hybride** (**Grid** pour le **layout macro**, **Flex** pour l’**agencement micro**), **évitez les redites**, citez **une mauvaise pratique** et **une règle simple** de décision. **Sans liste. Sans code.**

**Votre prompt F (écrivez ici) :**

---

---

---

---

---

---

#### Estimation des paramètres

| Test | temperature | max_tokens | top_p | frequency_penalty | presence_penalty | But attendu                                                 |
| ---- | ----------- | ---------- | ----: | ----------------: | ---------------: | ----------------------------------------------------------- |
| F    |             |            |       |                   |                  | Stratégie hybride, anti-redite, mauvaise pratique (150–200) |

---

### (Optionnel) Prompt G — modèle avec exigences explicites

> **Rédigez un prompt d’examen “modèle”** (pas la réponse) qui impose : **longueur précise** (25–40 **ou** 120–160 **ou** 150–200 mots), **ton** (factuel académique **ou** créatif précis), **interdits** (**sans liste**, **sans code**), **critère 1D vs 2D obligatoire**, et, pour la version longue, **un contre-exemple**. **N’écrivez aucune réponse.**

**Votre prompt G (écrivez ici) :**

---

---

---

---

#### Estimation des paramètres

| Test | temperature | max_tokens | top_p | frequency_penalty | presence_penalty | But attendu                                         |
| ---- | ----------- | ---------- | ----: | ----------------: | ---------------: | --------------------------------------------------- |
| G    |             |            |       |                   |                  | Prompt méta conforme (exigences claires, sans code) |

