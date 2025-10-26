# Correction — Exercice « T-P-L-S-F-C-V »

<br/>
<br/>

# PARTIE 1

## Contexte du prompt (texte factuel)

> « Résume l’article ci-dessous en **5 puces** (≤ **120 mots**), et **cite 2 limites** de l’étude.
> Si une information manque, écris *“Incertitude : …”*.
> **Article (extrait autorisé)** : <extrait de 2–3 paragraphes>. »

---

## Tableau complété (modèle)

| Élément                | Valeur attendue (exemple)                                                                                                   | Justification (1 phrase)                                                       |
| ---------------------- | --------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------ |
| **T – Temperature**    | **0.2**                                                                                                                     | Tâche factuelle et contrainte (5 puces ≤120 mots), on minimise la variabilité. |
| **P – top-P / top-K**  | **top_p = 0.85** *(ou top_k = 40)*                                                                                          | Conserve une fluidité correcte sans divaguer ; cohérent avec T basse.          |
| **L – max_tokens**     | **200**                                                                                                                     | Budget suffisant pour 5 puces + 2 limites tout en restant concis.              |
| **S – Stop sequences** | **["### FIN"]** *(optionnel mais recommandé)*                                                                               | Permet une coupure nette si on demande explicitement de finir par “### FIN”.   |
| **F – Format**         | **Markdown** : 5 puces + ligne « Limites : … »                                                                              | Format simple, vérifiable à l’œil et corrigeable automatiquement.              |
| **C – Context**        | **“Répondre uniquement à partir de l’extrait fourni.”**                                                                     | Évite les hallucinations et impose de signaler les manques.                    |
| **V – Validation**     | 1) ≤120 mots ; 2) **exactement** 5 puces + 2 limites ; 3) aucune info hors extrait ; 4) mention *Incertitude* si nécessaire | Contrôles objectifs et mesurables avant validation.                            |

> ✅ Variantes acceptables si **cohérentes et justifiées** :
> – `temperature` entre **0.1 et 0.3** ; `top_p` entre **0.8 et 0.9** ; `max_tokens` entre **160 et 220**.
> – `stop` peut être omis si la consigne de format est strictement respectée, mais l’inclure simplifie l’évaluation.

---

## Bloc « Paramètres recommandés » (modèle)

```yaml
temperature: 0.2
top_p: 0.85        # (ou top_k: 40)
max_tokens: 200
stop: ["### FIN"]  # conseillé si vous imposez de finir sur cette séquence
response_format: "markdown"

context_policy: "Répondre uniquement à partir de l'extrait fourni ; indiquer 'Incertitude : …' si l'information manque."
validation_rules:
  - "Longueur totale ≤ 120 mots"
  - "Exactement 5 puces + 2 limites"
  - "Aucune information hors de l'extrait"
  - "Mention 'Incertitude : …' si nécessaire"
```

---

## Prompt opérationnel (modèle à coller)

```
Rôle : Tu es un rédacteur factuel et concis.
Contexte (extrait autorisé uniquement) :
<EXTRAIT ICI>
Tâche : Résume l’article en 5 puces (≤120 mots) et cite 2 limites de l’étude.
Format : Markdown — 5 puces ; puis une ligne commençant par « Limites : » listant 2 limites.
Contraintes : Aucune information hors extrait. Si une information manque, écris « Incertitude : … ».
Paramètres recommandés : temperature 0.2 ; top_p 0.85 ; max_tokens 200 ; stop ["### FIN"].
Validation avant rendu : longueur ≤120 mots ; exactement 5 puces + 2 limites ; aucune info hors extrait ; incertitudes signalées.
### FIN
```

---

## Notes de correction (barème 10 pts proposé)

* **T (2 pts)** : valeur basse (0.1–0.3) + justification factuelle.
* **P (2 pts)** : `top_p` 0.8–0.9 (ou `top_k` 30–60) + cohérence avec T.
* **L (1 pt)** : `max_tokens` compatible (≈ 180–220).
* **S (1 pt)** : `stop` pertinent **ou** omission justifiée.
* **F (1 pt)** : format vérifiable (Markdown 5 puces + 2 limites).
* **C (2 pts)** : règle “répondre uniquement depuis l’extrait” + mention des incertitudes.
* **V (1 pt)** : ≥3 règles de validation **mesurables** (longueur, compte des puces, hors extrait, incertitude).

---

## Pièges fréquents (et remédiations)

* **T trop haute** (≥0.6) → style inutilement créatif : **baisser T**.
* **top_p = 1.0** + T haute → dérives : **ramener top_p à 0.85–0.9**.
* **max_tokens** trop bas → sortie tronquée : **monter à ~200**.
* **Format flou** (texte brut) → **imposer Markdown** + structure.
* **Hallucinations** → **context_policy** stricte + règle *Incertitude*.
* **Validation vague** → critères **comptables** (mots, n puces, n limites).

---

### Rappel mnémotechnique

**T-P-L-S-F-C-V** → **T**empérature, **P** (top-P/K), **L**ongueur, **S**top, **F**ormat, **C**ontexte, **V**alisation.
*“Tu Peux Lire Sans Faire d’erreurs Constatées & Validées.”*



<br/>
<br/>











# Partie 2 

Rédigez une réponse structurée expliquant **pourquoi choisir la température à 0,2** pour l’exercice « Résumé en **5 puces** (≤ **120 mots**) + **2 limites**, **uniquement** depuis un extrait », et décris **une procédure reproductible** pour fixer et valider la température :

1. **Ancrage par type de tâche** (factuel/contraint, mixte, créatif) ;
2. **Micro-test en 3 minutes** avec trois températures (0,1 / 0,2 / 0,3), mêmes autres paramètres (`top_p=0,85`, `max_tokens=200`, `stop=["### FIN"]`), et **rubrique R1–R5** (format, longueur, hors-contexte, clarté, stabilité) ;
3. **Ajustements** (quand monter à 0,25–0,3, quand descendre à 0,15–0,2, gestion des répétitions avec `frequency_penalty`) ;
4. **Règle d’or** à ne pas cumuler température **élevée** et `top_p` **élevé** en factuel (plage conseillée `temperature 0,1–0,3`, `top_p 0,8–0,9`) ;
5. **Exemple appliqué** avec paramètres initiaux et les **deux raisons** concrètes justifiant 0,2 ;
6. **Validation automatique** (checklist machine notée /5 : nombre de puces, nombre de mots, “Limites : …”×2, détection hors-extrait, mention “Incertitude”).


# Réponse

**Pourquoi 0.2 ?** Parce qu’on ne “devine” pas la température : on la **choisit par protocole** selon la tâche et on **valide par un mini-test**. Voici comment rendre ça clair et reproductible.

# Comment choisir la température (procédure simple)

## 1) Ancrage par type de tâche

* **Factuel/contraint** (résumé ≤ 120 mots, 5 puces, pas d’invention) → **ancre à 0.2**
  (très peu d’aléa → plus de conformité au format et moins d’inventions)
* **Mixte** (explicatif avec un peu de style) → 0.3–0.5
* **Créatif** (idées, storytelling, design) → 0.7–1.0

> Pour ton exercice “5 puces ≤ 120 mots + 2 limites + pas hors extrait”, c’est une **tâche factuelle/contrainte** ⇒ on **part à 0.2**.

## 2) Micro-test en 3 minutes (pour ne pas rester dogmatique)

1. Garde **top_p = 0.85**, **max_tokens = 200**, le même prompt.
2. Lance **3 températures** : **0.1**, **0.2**, **0.3** (mêmes autres paramètres).
3. Évalue chaque sortie avec cette **rubrique rapide** (0 ou 1 point par critère) :

   * R1 : **Format** respecté (exactement 5 puces + 2 limites)
   * R2 : **Longueur** ≤ 120 mots
   * R3 : **Zéro hors-contexte** (uniquement l’extrait)
   * R4 : **Clarté** (phrases simples, pas de fioritures)
   * R5 : **Stabilité** (si tu relances, la structure reste conforme)

> **Choisis la température qui obtient le score total le plus haut.**
> Dans la pratique, pour ce type de consigne, **0.2** bat régulièrement 0.1 (trop sec/elliptique) et 0.3 (un peu plus de dérive/verbosité).

## 3) Ajustements si besoin

* Si la réponse est **trop terne ou elliptique** → essaie **0.25–0.3**.
* Si tu observes des **écarts de format** ou des formulations “libres” → redescends à **0.15–0.2**.
* Si la sortie **bégaye** ou répète → garde la température et ajoute `frequency_penalty: 0.3–0.5`.

# Règle d’or : ne pas cumuler “haut + haut”

* Évite **temperature élevée** **ET** **top_p élevé** ensemble sur du factuel (ça augmente la variance inutilement).
* Pour du factuel : `temperature 0.1–0.3` **et** `top_p 0.8–0.9` marchent bien.

# Exemple appliqué à ton exercice (réalisme pédagogique)

* **Objectif** : 5 puces ≤ 120 mots, 2 limites, **uniquement** l’extrait, ton neutre.
* **Paramètres initiaux** :
  `temperature: 0.2, top_p: 0.85, max_tokens: 200, stop: ["### FIN"]`
* **Pourquoi 0.2 ?**

  * Assez **bas** pour **maximiser la conformité** au format et éviter l’“embellissement”.
  * Pas trop **bas** (0.0–0.1) pour laisser une **petite flexibilité** de phrasé (moins d’ellipses trop sèches).

# Si tu veux un critère plus “quantifié”

Ajoute une **validation automatique** (checklist machine) :

* Compter les puces (== 5) → +1
* Compter les mots (≤ 120) → +1
* Détecter “Limites : …” avec 2 éléments → +1
* Rejeter si le texte contient un mot clé **hors extrait** (liste d’interdits) → +1
* Marquer “Incertitude” si un point manque → +1
  **Score max = 5**. Garde la température qui **maximise** ce score sur **2–3 runs**.
  Sur ce genre de tâche, **0.2** arrive généralement en tête.

---

**En bref**
On **part** à **0.2** parce que la **tâche est factuelle et fortement contrainte**.
On **confirme** par un **micro-test à 3 températures** avec une **rubrique mesurable**.
Si écart → **ajuste par pas de 0.05–0.1**, jamais en même temps que tu montes beaucoup `top_p`.





<br/>
<br/>

# Partie 3



# Question (AC) — Température selon le type de tâche

Rédigez un **guide pratique** qui présente **12 prompts** couvrant des usages variés (résumé factuel, extraction JSON, Q&A cadré par contexte, procédure pas-à-pas, explication pédagogique, reformulation pro, email pro, idéation, slogans marketing, storytelling, traduction pro, génération de code).

Pour **chaque prompt**, fournir obligatoirement :

1. Le **prompt** (clair, une seule consigne principale).
2. La **température de départ** (valeur précise).
3. **Quand baisser** la température (signal concret observé).
4. **Quand monter** la température (signal concret observé).
5. Une **règle rapide d’ajustement** (ex. « si X alors −0,05 / +0,1 »).

Contraintes globales :

* Respecte la **règle flash** :

  * **Factuel/contraint** → 0.1–0.3
  * **Mixte/explicatif** → 0.3–0.6
  * **Créatif/marketing/histoire/idéation** → 0.7–1.0+
* Ne change **aucun autre paramètre** (top_p, max_tokens, stop, etc.) dans tes explications — on ne parle **que** de **température** et de **son ajustement**.
* Termine par une **micro-méthode d’ajustement** (4 étapes : 3 runs à T ancre/−0.1/+0.1, scoring simple, choix de la meilleure T, affinement par pas de 0.05 sans toucher à top_p).

**Livrable attendu** : un document clair, structuré en 12 sous-sections (1 par prompt) + une section finale « Micro-méthode d’ajustement ».




# Réponse

Voici **12 prompts clairs** avec, pour chacun, la **température de départ**, **quand la baisser/monter**, et une **règle rapide** pour ajuster.



# Règle flash

* **Factuel/contraint** → **0.1–0.3**
* **Mixte/explicatif avec un peu de style** → **0.3–0.6**
* **Créatif/marketing/histoire/idéation** → **0.7–1.0+**

---

## 1) Résumé factuel très contraint

**Prompt**

> « Résume l’extrait ci-dessous en **5 puces** (≤ **120 mots**). **Aucune info hors extrait**. Si un point manque, écris *“Incertitude : …”*.
> *Extrait :* ‹…› »

**Température** : **0.2**
**Baisser** si dépasse la longueur ou invente (0.15).
**Monter** si style trop sec/elliptique (0.25–0.3).
**Règle rapide** : si 2 relances dépassent >120 mots → baisse de 0.05.

---

## 2) Extraction structurée → JSON

**Prompt**

> « Rends **UNIQUEMENT** un JSON valide avec `{"titre": "", "resume": "", "points_cles": []}` à partir de l’extrait. Aucune info hors extrait. *Extrait :* ‹…› »

**Température** : **0.1–0.2**
**Baisser** si JSON invalide (0.1).
**Monter** (rarement) si le texte est tronqué (0.25).
**Règle** : si accolades manquantes → 0.1 + stop `["}"]`.

---

## 3) Q&A cadré par contexte

**Prompt**

> « Réponds **uniquement** à partir de l’extrait. Si l’info n’y est pas, écris *“Incertitude : …”*.
> *Question :* ‹…› — *Extrait :* ‹…› »

**Température** : **0.2–0.3**
**Baisser** si ajoute des hypothèses.
**Monter** si la phrase est trop télégraphique.
**Règle** : si la réponse varie trop entre 2 runs → 0.2.

---

## 4) Procédure pas-à-pas (procédé opératoire)

**Prompt**

> « Donne une **procédure en 6 étapes**, impératives, pour ‹tâche›. **Pas d’emphase marketing**, pas d’hypothèses. »

**Température** : **0.2–0.3**
**Baisser** si verbeux ou digressif.
**Monter** si manque de transitions lisibles.
**Règle** : si étapes >6 → baisse 0.05 et impose longueur/étapes.

---

## 5) Explication pédagogique simple

**Prompt**

> « Explique ‹concept› à un public **débutant** en **5 phrases courtes**, avec **1 analogie concrète**. »

**Température** : **0.3–0.4**
**Baisser** si l’analogie part trop loin.
**Monter** si l’explication paraît sèche/peu imagée.
**Règle** : analogie peu parlante → +0.05.

---

## 6) Reformulation polie/professionnelle

**Prompt**

> « Réécris ce message en **registre professionnel**, **clair et concis**, sans adoucir le fond. *Texte :* ‹…› »

**Température** : **0.3**
**Baisser** si ajoute des tournures inutiles.
**Monter** si le ton est trop sec/rigide.
**Règle** : si 2 mots “fluff” par phrase → −0.05.

---

## 7) Email pro avec un peu de chaleur

**Prompt**

> « Rédige un **email bref** pour demander ‹X›, ton **cordial et direct**, 3–5 phrases, avec **CTA clair**. »

**Température** : **0.4–0.5**
**Baisser** si trop fleuri.
**Monter** si sonne robotique.
**Règle** : si 2 adjectifs superflus → −0.05.

---

## 8) Idéation de concepts (divergente)

**Prompt**

> « Propose **10 idées originales** de ‹x›, **une ligne par idée**, sans répétitions. »

**Température** : **0.8–0.9**
**Baisser** si idées redondantes (0.7–0.8).
**Monter** si trop “banal” (0.95–1.0).
**Règle** : ≥3 idées “déjà vues” → +0.1 **ou** ajoute `presence_penalty: 0.4`.

---

## 9) Slogans/accroches marketing

**Prompt**

> « Donne **12 accroches** pour ‹produit›, **≤ 8 mots**, style **percutant**. »

**Température** : **0.9–1.0**
**Baisser** si clichés lourds.
**Monter** si tout se ressemble.
**Règle** : si 4 accroches quasi-identiques → +0.1 et `top_p: 0.95–1.0`.

---

## 10) Paragraphe créatif (storytelling court)

**Prompt**

> « Écris un **paragraphe** (≈120 mots) où ‹personnage› découvre ‹élément›, ton **poétique** mais **lisible**. »

**Température** : **0.9–1.1**
**Baisser** si devient obscur/ampoulé (0.8–0.9).
**Monter** si trop plat.
**Règle** : si 2 métaphores de suite peu claires → −0.1.

---

## 11) Traduction avec choix de ton

**Prompt**

> « Traduis en **français professionnel** (vouvoyement), en **gardant la précision technique**, ce texte : ‹…› »

**Température** : **0.2–0.3**
**Baisser** si glisse vers paraphrase créative.
**Monter** si la fluidité est hachée.
**Règle** : erreurs de registre → −0.05 et rappeler la contrainte.

---

## 12) Génération de code (fonction + tests)

**Prompt**

> « Écris une fonction **Python** `clean_names(df)` (trim, minuscules, suppression d’accents), avec **docstring** et **2 tests pytest**. »

**Température** : **0.2**
**Baisser** si code instable/variations de signature.
**Monter** (rare) si la doc est trop sèche/elliptique (0.3).
**Règle** : si le code change d’API d’un run à l’autre → 0.2 ou seed fixe.

---

## Micro-méthode d’ajustement (appliquer à chaque prompt)

1. **Lance 3 runs** à T = ancre, ancre −0.1, ancre +0.1 (mêmes autres paramètres).
2. **Score 0/1** sur 4 critères simples (format, longueur, hors-contexte, lisibilité).
3. **Garde la T qui maximise** le score.
4. Si besoin, ajuste par **pas de 0.05** (ne change pas `top_p` en même temps).

---

## Mini mémo

* **T bas** = conformité/rigueur.
* **T haut** = variété/style/idéation.
* Pour le **factuel**, garde `top_p` **0.8–0.9** ; pour le **créatif**, `top_p` **0.9–1.0**.
* Évite **T élevée + top_p élevé** sur du factuel.









<br/>
<br/>

# Partie 4



> **Rédigez un mini-explication ultra simple sur le paramètre *température* en IA générative.**
>
> 1. Explique la température comme un **“bouton créativité”** avec trois repères : **0.2** (très sage/précis), **0.5** (normal/un peu de style), **0.9** (créatif/imagé).
> 2. Donne une **règle mémo** : *Fait sérieux → 0.2 · Texte normal → 0.5 · Créatif → 0.9*.
> 3. Propose une **méthode en 3 pas** pour choisir et ajuster : **choisir le but** (sérieux/normal/créatif) → **prendre la valeur de départ** (0.2/0.5/0.9) → **tester une fois** et **ajuster par pas de 0.1** (*trop sec → +0.1 ; ça divague → −0.1*).
> 4. Donne **6 exemples concrets** (A–F) avec pour chacun : le **prompt**, la **température de départ**, et **quand monter/descendre** (valeurs précises demandées : A=0.2, B=0.5, C=0.9, D=0.4, E=0.3, F=1.0) avec des règles d’ajustement **±0.1**.
> 5. Termine par un **mini pense-bête** : *0.2 = réponds juste ; 0.5 = parle normalement ; 0.9 = sois inventif*.
>    **Présente le tout de façon claire et structurée, exactement dans cet ordre.**


# Température = bouton “créativité”

* **0.2** → très sage, précis (peu de surprises).
* **0.5** → normal, un peu de style.
* **0.9** → créatif, images, tournures originales.

**Règle mémo :**
**Fait sérieux → 0.2** · **Texte normal → 0.5** · **Créatif → 0.9**

---

# Comment la choisir (3 pas)

1. **Choisis ton but :** sérieux / normal / créatif.
2. **Prends la valeur de départ :** 0.2 / 0.5 / 0.9.
3. **Teste une fois :**

   * Si c’est **trop sec** → +0.1
   * Si ça **divague** → −0.1

> C’est tout. Tu ajustes par **petits pas de 0.1**.

---

# Exemples tout prêts

## A) Factuel (précis)

**Prompt :** « Résume ce texte en **5 puces** (≤120 mots), **sans inventer**. »
**Température : 0.2**

* Si ça dépasse 120 mots → **0.1**
* Si c’est trop “robot” → **0.3**

## B) Mail pro (ton cordial, bref)

**Prompt :** « Écris un **email court** pour demander un rendez-vous, ton **professionnel**. »
**Température : 0.5**

* Trop froid → **0.6**
* Trop fleuri → **0.4**

## C) Idées (brainstorm)

**Prompt :** « Donne **10 idées originales** pour un atelier IA pour débutants. »
**Température : 0.9**

* Idées banales → **1.0**
* Trop farfelu → **0.8**

## D) Explication simple

**Prompt :** « Explique **la photosynthèse** en **5 phrases faciles** pour un enfant de 10 ans. »
**Température : 0.4**

* Trop scientifique → **0.3**
* Trop sec → **0.5**

## E) Mode d’emploi (étapes)

**Prompt :** « Donne **6 étapes** claires pour faire un gâteau. »
**Température : 0.3**

* Trop de blabla → **0.2**
* Manque de liant → **0.4**

## F) Slogans pub

**Prompt :** « Propose **8 slogans courts** (≤6 mots) pour une appli d’étude. »
**Température : 1.0**

* Trop similaires → **1.1**
* Trop bizarres → **0.9**

---

# Mini pense-bête

* **0.2** = “réponds juste, sans fantaisie”.
* **0.5** = “parle normalement”.
* **0.9** = “sois inventif”.



<br/>
<br/>


# Partie 5


# Question

> **Un seul exemple, on ne change que la température (T)**
>
> En t’appuyant sur l’extrait et le prompt ci-dessous, produis un document structuré où tu varies **uniquement** le paramètre **température (T)**. Tous les autres paramètres restent **identiques**.
>
> **Contexte (extrait fixe)**
> *Les panneaux solaires convertissent la lumière en électricité grâce à l’effet photovoltaïque. Leur coût a fortement baissé depuis 2010, ce qui a accéléré leur adoption. Les limites majeures sont l’intermittence de la production et le besoin de stockage ou d’appoint.*
>
> **Prompt (fixe)**
> **« Résume l’extrait en 5 puces (≤ 120 mots). N’utilise que l’extrait. Si quelque chose manque, écris “Incertitude : …”. Termine par `### FIN`. »**
>
> **Paramètres immuables**
> `top_p = 0.85` · `max_tokens = 200` · `stop = ["### FIN"]`
>
> **Travail demandé**
>
> 1. Pour **T = 0.1**, **0.2**, **0.5**, **0.7**, **0.9** :
>    – Écris une **sortie type** (5 puces + `### FIN`).
>    – Ajoute 2–3 lignes : **à quoi ça sert ?** / **quand l’utiliser ?** / **risques**.
>
> 2. Rédige la section **« Comment décider de la température »** pour CE MÊME EXEMPLE :
>    – Règle de départ : commencer à **T = 0.2** pour un devoir factuel à puces.
>    – Ajustement en 1 test : si > 120 mots → descends à **0.1** ; si “trop sec” → monte à **0.3–0.5**.
>    – Limite : ne pas dépasser **0.5** pour un devoir factuel.
>
> 3. Conclus par une **mini-fiche** récapitulative :
>    – **T=0.1** : conformité maximale, style très sobre.
>    – **T=0.2** : factuel recommandé (examens, résumés contraints).
>    – **T=0.5** : plus fluide, toujours correct.
>    – **T=0.7+** : plus de style/variété, à éviter pour l’évaluation factuelle.
>
> **Contraintes**
> – **Ne change que T**.
> – Garde exactement **5 puces** et **≤ 120 mots** à chaque essai.
> – Termine chaque sortie par **`### FIN`**.






# Réponse

# Exemple unique (on ne change que T)

## Contexte (extrait fixe)

> *Les panneaux solaires convertissent la lumière en électricité grâce à l’effet photovoltaïque. Leur coût a fortement baissé depuis 2010, ce qui a accéléré leur adoption. Les limites majeures sont l’intermittence de la production et le besoin de stockage ou d’appoint.*

## Prompt (fixe)

> **“Résume l’extrait en 5 puces (≤ 120 mots). N’utilise que l’extrait. Si quelque chose manque, écris « Incertitude : … ». Termine par `### FIN`.”**
> *(Paramètres immuables : top_p=0.85, max_tokens=200, stop=["### FIN"])*

---

## 1) T = **0.1** (très sage, très stable)

**Sortie type**

* Conversion de la lumière en électricité par effet photovoltaïque.
* Forte baisse des coûts depuis 2010.
* Adoption accélérée grâce à la baisse des coûts.
* Production **intermittente**.
* Besoin de **stockage** ou d’appoint.

### FIN

**À quoi ça sert ?** format **nickel**, aucune “envolée”.
**Quand l’utiliser ?** examens, extraction, réponses ultra factuelles.
**Symptôme pour baisser à 0.1 :** quand T=0.2 invente ou dépasse 120 mots.

---

## 2) T = **0.2** (factuel recommandé)

**Sortie type**

* Les panneaux solaires produisent de l’électricité via l’effet photovoltaïque.
* Le **coût** a nettement baissé depuis **2010**.
* Cette baisse a **accéléré** l’adoption.
* La production est **intermittente**.
* Un **stockage** ou un **appoint** est nécessaire.

### FIN

**Pourquoi c’est le “par défaut” pour du factuel ?**
Toujours propre, un tout petit peu plus fluide que 0.1, sans dériver.

---

## 3) T = **0.5** (neutre/équilibré)

**Sortie type**

* L’effet photovoltaïque transforme la lumière en électricité.
* Les coûts chutent depuis 2010, rendant la technologie plus abordable.
* Résultat : diffusion plus rapide dans de nombreux contextes.
* Production irrégulière selon l’ensoleillement.
* Nécessité de stockage ou d’un système d’appoint.

### FIN

**Constat** : encore conforme, un style un peu plus “rédigé”.
**Quand monter à 0.5 ?** si 0.2 paraît trop “sec”.

---

## 4) T = **0.7** (plus de style, risque léger)

**Sortie type**

* L’effet photovoltaïque capte la lumière pour en faire du courant.
* La chute des prix depuis 2010 a ouvert le marché.
* L’adoption s’accélère, portée par l’accessibilité.
* Limite : une production qui suit les caprices du soleil.
* Solution : stockage ou appoint pour lisser l’alimentation.

### FIN

**Attention** : le ton devient plus “image” (“caprices du soleil”).
**Quand éviter 0.7 ?** si l’exercice exige sobriété stricte.

---

## 5) T = **0.9** (créatif, le plus variable)

**Sortie type**

* La lumière devient électricité via le photovoltaïque.
* En une décennie, les coûts plongent et changent l’échelle.
* L’adoption accélère, portée par cette bascule économique.
* Talon d’Achille : l’intermittence de la production.
* D’où le besoin de stocker ou d’adosser un appoint.

### FIN

**Risque** : formulations imagées, parfois borderline sur un devoir factuel.
**À réserver** : slogans, marketing, storytelling — pas pour ton exercice.

---

# Comment **décider** de la température (avec CE MÊME EXEMPLE)

1. **Commence à T=0.2** (factuel).
2. **Teste une fois** : si

   * ça dépasse 120 mots → **descends à 0.1**
   * c’est trop “sec” → **monte à 0.3–0.5**
3. **Ne monte pas au-delà de 0.5** pour un devoir factuel à puces.

> **Règle ultra simple** :
>
> * **Devoir précis à puces** → 0.2
> * **Un peu plus de naturel** → 0.3–0.5
> * **Créatif/marketing** → 0.7–1.0

---

## Mini-fiche (prête à coller dans ton cours)

* **Même prompt, même extrait, on ne change QUE T.**
* **T=0.1** : maximum de conformité, style très sobre.
* **T=0.2** : factuel recommandé (exams, résumés contraints).
* **T=0.5** : plus fluide, toujours correct.
* **T=0.7+** : style/variété, attention pour l’évaluation.











