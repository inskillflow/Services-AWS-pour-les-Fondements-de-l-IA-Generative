# 1) Paramètres essentiels (texte / code)

> Idée clé : la qualité d’une génération = *(Contexte + Consignes + Format + Paramètres + Contrôles)*

## 1.1 Paramètres de **contrôle du style / hasard**

| Paramètre                           | Ce que ça contrôle                                 | Quand l’augmenter                                                              | Quand le baisser                                    | Notes & pièges                                                  |
| ----------------------------------- | -------------------------------------------------- | ------------------------------------------------------------------------------ | --------------------------------------------------- | --------------------------------------------------------------- |
| **temperature** (0–1.5)             | Aléa global (créativité).                          | Idéation, style littéraire, variations.                                        | Faits, exactitude, code sensible, tableaux stricts. | Ne la pousse pas **et** top-p haut en même temps (instabilité). |
| **top_p** (0–1)                     | Nucleus sampling : réduit le “vocabulaire” retenu. | Fluidité créative, éviter répétitions quand *temperature* est basse à moyenne. | Sortie stable sans surprises.                       | Si tu montes **top_p**, évite une **temperature** trop haute.   |
| **top_k** (entier)                  | Coupe au *k* tokens les plus probables.            | Prose concise, “resserrer” le choix.                                           | Sortie plus riche.                                  | Top-k=1 ≈ très déterministe. Pas toujours dispo.                |
| **frequency_penalty** (−2…2)        | Pénalise la répétition de *tokens* fréquents.      | Réduire verbosité/répétitions.                                                 | Maintenir refrain/mot-clé.                          | Pour éviter “bégaiements”.                                      |
| **presence_penalty** (−2…2)         | Pousse à introduire de nouveaux mots/idées.        | Explorer des angles nouveaux.                                                  | Rester très cadré.                                  | Utile en brainstorming.                                         |
| **logit_bias** / **bias par token** | Favoriser/défavoriser certains mots.               | Forcer un style ou bannir un terme.                                            | —                                                   | Avancé; ne pas abuser (risque d’artefacts).                     |

**Rappels rapides**

* **Factuel/rigoureux** : `temperature 0.1–0.3`, `top_p 0.7–0.9`, `frequency_penalty 0–0.5`.
* **Créatif** : `temperature 0.8–1.0`, `top_p 0.9–1.0`, `presence_penalty 0.2–0.6`.

---

## 1.2 Paramètres de **longueur et structure**

| Paramètre                             | Ce que ça contrôle                          | Bonnes pratiques                                                                 |
| ------------------------------------- | ------------------------------------------- | -------------------------------------------------------------------------------- |
| **max_tokens**                        | Longueur maximale de la sortie.             | Fixe une **budgetisation** (ex. 300 pour un résumé, 1200 pour un plan détaillé). |
| **stop_sequences**                    | Séquences d’arrêt (coupe nette).            | Exemple : `["### FIN","</json>"]` pour stopper proprement.                       |
| **response_format** / **json_schema** | Forcer un JSON valide conforme à un schéma. | Idéal pour **extraction structurée** & **évaluations automatiques**.             |
| **n** (nb de complétions)             | Variantes parallèles.                       | Prends 2–3 variantes pour comparer, puis garde la meilleure.                     |
| **seed**                              | Reproductibilité.                           | Utile en cours/examens pour mêmes résultats d’un run à l’autre.                  |

---

## 1.3 Paramètres de **orchestration / garde-fous**

| Paramètre                        | Ce que ça contrôle            | Bonnes pratiques                                                         |
| -------------------------------- | ----------------------------- | ------------------------------------------------------------------------ |
| **system / rôle**                | Persona & règles du modèle.   | “Tu es un correcteur exigeant…”, “Tu es un assistant de conformité…”.    |
| **instructions** (consignes)     | Ce qu’il faut produire.       | Objectif, critères, format, contraintes, langue, ton.                    |
| **context** (données autorisées) | Ce à partir de quoi répondre. | Extraits, références, tableaux. *Interdire d’inventer* si hors contexte. |
| **tools/functions**              | Appels d’outils (optionnel).  | Quand il faut calculer/chercher/structurer via fonctions.                |
| **safety/guardrails**            | Style & limites.              | “Évite les affirmations non sourcées ; indique *incertitude* si besoin.” |

---

# 2) Présélections “prêtes à l’emploi”

## 2.1 Presets (texte/code)

**A. Fiche factuelle (sûre & concise)**

```yaml
temperature: 0.2
top_p: 0.8
max_tokens: 250
frequency_penalty: 0.2
presence_penalty: 0.0
stop: ["### FIN"]
```

**B. Idéation créative (divergente)**

```yaml
temperature: 0.9
top_p: 1.0
max_tokens: 700
presence_penalty: 0.4
frequency_penalty: 0.2
n: 3
```

**C. Extraction → JSON (strict)**

```yaml
temperature: 0.1
top_p: 0.8
max_tokens: 400
response_format: json_schema  # ou équivalent
stop: ["}"]
```

**D. Code sensible (rigueur)**

```yaml
temperature: 0.2
top_p: 0.7
max_tokens: 800
frequency_penalty: 0.1
presence_penalty: 0.0
```

---

# 3) Gabarit d’instruction complet (texte)

> **Utilise tel quel, remplace les chevrons.**

```
[ROLE] Tu es <rôle précis : ex. rédacteur technique exact et concis>.

[CONTEXTE] Réponds UNIQUEMENT à partir de ce contexte :
<coller ici extraits, tableaux, références autorisées>
Si une information manque, écris : “Information non disponible dans le contexte fourni.”

[TÂCHE] Produis <type de rendu> couvrant <points indispensables>.
- Public : <débutant / intermédiaire / expert>
- Ton : <neutre / pédagogique / professionnel>
- Langue : <français>
- Longueur : <ex. 200–250 mots>

[FORMAT] 
- Structure : <titres H2 + puces> 
- Sortie finale : <JSON valide selon schéma ci-dessous OU Markdown strict>
- Interdits : <aucun contenu spéculatif, pas de sources inventées>

[PARAMÈTRES RECOMMANDÉS]
- temperature: <0.2–0.4 factuel ; 0.7–1.0 créatif>
- top_p: <0.8–0.95>
- max_tokens: <valeur>
- stop: ["### FIN"] (si utile)

[VALIDATION] 
- Vérifie exactitude, format, longueur. Si incertitude : “Incertitude : …” et propose une étape de vérification.

### FIN
```

---

# 4) Forcer un **JSON valide** (extraction/évaluation)

## 4.1 Schéma **universel** minimal

```json
{
  "type": "object",
  "properties": {
    "titre": { "type": "string" },
    "resume": { "type": "string" },
    "points_cles": { "type": "array", "items": { "type": "string" } },
    "limites": { "type": "array", "items": { "type": "string" } },
    "incertitudes": { "type": "array", "items": { "type": "string" } }
  },
  "required": ["titre", "resume", "points_cles"],
  "additionalProperties": false
}
```

## 4.2 Prompt “strict JSON”

```
Rends UNIQUEMENT un JSON **valide** conforme au schéma. 
N’insère aucun commentaire, ni texte avant/après.
Si une valeur est inconnue, mets "" ou [].

<schéma ici>
```

> Astuce : ajoute `stop: ["}"]` pour couper juste après la fin de l’objet (selon l’API).

---

# 5) Table **effets croisés** (très pratique)

| Tu veux…                   | Fais ceci                                               | Évite                                       |
| -------------------------- | ------------------------------------------------------- | ------------------------------------------- |
| Sortie **très précise**    | `temperature≤0.3`, `top_p 0.7–0.9`, `max_tokens` adapté | `temperature>0.5`                           |
| **Moins de répétitions**   | `frequency_penalty 0.2–0.6`                             | `frequency_penalty=0` si le modèle “bégaie” |
| **Plus d’idées nouvelles** | `presence_penalty 0.2–0.6`, `temperature ≥0.7`          | `temperature bas + top_p bas`               |
| **Plus court**             | baisse `max_tokens`, donne longueur exacte              | —                                           |
| **Strict JSON**            | `temperature 0.1–0.2`, `stop=["}"]`, schéma             | `temperature>0.4`                           |
| **3 variantes rapides**    | `n=3`, température moyenne (0.6–0.8)                    | n=1 (perd la comparaison)                   |

---

# 6) Images — paramètres clés (génération)

> S’applique à la plupart des générateurs (les noms peuvent varier).

## 6.1 Paramètres **de rendu**

| Paramètre                   | Rôle                                             | Conseils                                            |
| --------------------------- | ------------------------------------------------ | --------------------------------------------------- |
| **width / height / aspect** | Taille & ratio (ex. 2048×1152 → 16:9).           | Choisis dès le départ (bannière, carré, slide 4:3). |
| **subject**                 | Sujet principal (espèce/objet/personne).         | Nom précis + attributs (âge, style, matière).       |
| **pose_action**             | Posture/angle (gros plan, plein pied, en vol).   | Spécifie « regard caméra » si tu veux l’accroche.   |
| **environment**             | Décor (forêt, studio, urbain).                   | 1 décor clair, pas 3.                               |
| **background**              | Traitement de fond (bokeh, uniforme).            | “bokeh prononcé” pour isoler le sujet.              |
| **lighting**                | Lumière (dorée, froide diffuse, studio softbox). | Adapte au ton (chaud/froid).                        |
| **composition**             | Cadrage (règle des tiers, centré, diagonale).    | Évite les consignes contradictoires.                |
| **color_tone**              | Palette (neutre à froid, saturation modérée).    | “sans sursaturation” évite l’effet cartoon.         |
| **negatives**               | Interdits (texte, watermark, blur, artifacts).   | Toujours en mettre une liste courte et solide.      |
| **variants**                | Nombre de versions (2–4).                        | Compare et choisis.                                 |
| **seed**                    | Reproductibilité.                                | Utile pour retouches pédagogiques.                  |

## 6.2 Gabarit **universel** (image → JSON)

```json
{
  "subject": "<ex. renard roux adulte>",
  "intent": "photo realiste",
  "pose_action": "<gros plan | plein pied | en vol>",
  "environment": "<foret | studio>",
  "background": "<bokeh naturel, fond flou>",
  "lighting": "<lumiere doree de fin d'apres-midi>",
  "composition": "<regle des tiers | centre>",
  "color_tone": "<couleurs naturelles, saturation moderee>",
  "width": 2048,
  "height": 1152,
  "negatives": "text, watermark, frame, oversaturated, blur, low-res, artifacts, extra limbs",
  "variants": 3
}
```

## 6.3 Prompt naturel (depuis le JSON)

```
Photo réaliste de <subject>, <pose_action>. 
Décor : <environment>. Arrière-plan : <background>. 
Éclairage : <lighting>. Ton : <color_tone>. 
Composition : <composition>. 
Interdits : aucun texte, watermark ni cadre ; éviter flou, basse résolution et artefacts. 
Format <width>×<height>. Générer <variants> variantes.
```

---

# 7) Exemples complets (copier → modifier)

## 7.1 Factual QA **avec contexte strict** (texte)

```
[ROLE] Tu es un assistant académique exact.
[CONTEXTE] Réponds UNIQUEMENT à partir de l’extrait ci-dessous. Si la réponse n’y figure pas, écris “Information non disponible dans l’extrait.”
<EXTRAIT ICI>

[TÂCHE] Réponds en 3–5 phrases, ton neutre, français.
[FORMAT] Markdown simple (pas de listes). Termine par “*Réponse basée sur l’extrait fourni.*”
[PARAMÈTRES] temperature=0.2, top_p=0.85, max_tokens=180
[VALIDATION] Vérifie exactitude et longueur.

### FIN
```

## 7.2 **Extraction → JSON** (strict)

```
[ROLE] Tu es un extracteur strict.
[TÂCHE] Extrait les champs {titre, resume, points_cles[], limites[]} à partir du texte fourni.
[FORMAT] Rends UNIQUEMENT un JSON valide conforme au schéma (pas de texte autour).
[PARAMÈTRES] temperature=0.1, top_p=0.8, max_tokens=350, stop=["}"]
[SCHÉMA]
{ "type":"object", "properties":{
 "titre":{"type":"string"},
 "resume":{"type":"string"},
 "points_cles":{"type":"array","items":{"type":"string"}},
 "limites":{"type":"array","items":{"type":"string"}}
}, "required":["titre","resume","points_cles"], "additionalProperties":false}
```

## 7.3 **Idéation** (3 variantes)

```
[ROLE] Tu es un consultant créatif.
[TÂCHE] Propose 3 concepts d’ateliers IA pour débutants (objectif, public, plan en 4 étapes).
[FORMAT] Liste numérotée (1–3), chaque item ≤ 120 mots.
[PARAMÈTRES] temperature=0.9, top_p=1.0, max_tokens=600, n=1
```

## 7.4 **Image** (renard → bannière 16:9)

```json
{
  "subject": "renard roux adulte",
  "intent": "photo realiste",
  "pose_action": "plein pied, debout, regard vers la camera",
  "environment": "foret",
  "background": "bokeh naturel, fond flou",
  "lighting": "lumiere doree de fin d'apres-midi",
  "composition": "regle des tiers, sujet legerement a gauche",
  "color_tone": "couleurs naturelles, saturation moderee",
  "width": 2048,
  "height": 1152,
  "negatives": "text, watermark, frame, oversaturated, blur, low-res, artifacts",
  "variants": 3
}
```

---

# 8) Check-lists rapides

## 8.1 **Avant d’exécuter**

* [ ] Objectif clair (quoi / pour qui / format).
* [ ] Contexte propre (sources autorisées, pas de données privées).
* [ ] Consignes structurées (rôle, tâche, format, contraintes).
* [ ] Paramètres adaptés (température, top_p, longueur, stop).
* [ ] Méthode de **contrôle** (auto + humain) définie.

## 8.2 **Dépannage**

* Sortie **verbeuse** → baisse `max_tokens`, ajoute longueur exacte.
* **Répétitions** → `frequency_penalty 0.3–0.6`.
* **Hallucinations** → contexte plus strict + phrase “Ne réponds que depuis l’extrait”.
* JSON **cassé** → `temperature 0.1–0.2` + `stop=["}"]` + schéma.
* **Trop sage** (créativité faible) → `temperature 0.8–1.0`, `presence_penalty 0.3–0.6`.

---

# 9) Mini **matrice de décision**

1. **Factuel/structuré ?**
   → `temperature 0.1–0.3`, `top_p 0.7–0.9`, JSON/format strict.

2. **Créatif/découverte ?**
   → `temperature 0.8–1.0`, `top_p 0.9–1.0`, 2–3 variantes.

3. **Évaluation automatique ?**
   → Schéma JSON + stop + validation.

4. **Image ?**
   → JSON “sujet/pose/décor/lumière/composition/taille/negatives/variants” ; ratio dès le départ.

---

# 10) Résumé express (mémotechnique)

* **T** (Temperature) : créativité
* **P** (top-P/K) : vocabulaire retenu
* **L** (Length) : max_tokens
* **S** (Stop) : coupe nette
* **F** (Format) : JSON/Markdown/…
* **C** (Context) : sources autorisées
* **V** (Validation) : règles de vérif (exactitude, format, longueur, incertitudes)

> T-P-L-S-F-C-V — pense “**Tu Peux Lire Sans Faire d’erreurs Constatées & Validées**”.



<br/>

# Annexe - Mémo ultra-court

* **top-k** = on ne garde que **k** mots les plus probables.
* **top-p** = on garde les mots jusqu’à atteindre une **probabilité cumulée p**.

### Exemples concrets (les probabilités d’un prochain mot)

| Situation                  | Distribution (triée)                                                         | **top-k (k=3)** → mots gardés | **top-p (p=0.8)** → mots gardés                                          | Pourquoi c’est différent                                                         |
| -------------------------- | ---------------------------------------------------------------------------- | ----------------------------- | ------------------------------------------------------------------------ | -------------------------------------------------------------------------------- |
| **1. Classique**           | le 0.40, la 0.20, un 0.15, des 0.10, ce 0.08, pour 0.04, dans 0.03 (somme=1) | **le, la, un**                | **le, la, un, des** (0.40+0.20+0.15=0.75 < 0.8 ⇒ on ajoute *des* → 0.85) | top-p s’adapte et prend 4 mots pour dépasser 0.8, top-k reste fixé à 3.          |
| **2. Pic très fort**       | X 0.70, Y 0.10, Z 0.08, W 0.05, …                                            | **X, Y, Z**                   | **X, Y** (0.70+0.10=0.80 pile)                                           | Avec un mot ultra-probable, **top-p** peut garder **moins** d’options que top-k. |
| **3. Répartition “plate”** | a 0.18, b 0.17, c 0.16, d 0.15, e 0.14, f 0.10, g 0.10                       | **a, b, c**                   | **a, b, c, d, e** (cumul = 0.80)                                         | Quand tout est assez probable, **top-p** garde **plus** de mots que top-k.       |

### Règles pratiques

* **T (température)** contrôle l’aléa global ; **top-k/top-p** contrôlent **l’éventail** de choix.
* Pour réponses **stables** : T basse (≈0.2) + **top-p 0.8–0.9** *ou* **top-k 40**.
* Si c’est **trop sec** : augmente légèrement **p** (0.9) ou **k** (50).
* Si ça **divague** : baisse **p** (0.7–0.8) ou **k** (20).



# Annexe 2

- **“top-k = 40”** est juste un **repère pratique** (pas magique) : on limite le choix aux **40 tokens les plus probables** à chaque pas. 

### Que signifie k=40 ?

* À chaque mot, le modèle **regarde seulement les 40 meilleurs candidats** puis échantillonne dedans.
* Si la distribution est “raide” (très concentrée), **il n’y a parfois même pas 40 candidats plausibles** → l’effet est quasi nul.
* Si elle est “plate”, k=40 **évite d’aller trop loin** dans les queues (moins de divagations que k=200).

### Quand utiliser quels k ?

| Objectif                  | Réglage conseillé        | Effet                              |
| ------------------------- | ------------------------ | ---------------------------------- |
| Réponse factuelle, stable | **T=0.2, top-k=20–50**   | Peu de créativité, cohérence forte |
| Chat naturel contrôlé     | **T=0.5, top-k=40–80**   | Fluide, peu d’erreurs              |
| Créatif (story, idées)    | **T=0.7, top-k=100–200** | Plus de variété, plus de risque    |

### Par rapport à top-p

* Utilise **l’un ou l’autre** (ou l’intersection si ta lib le permet).
* **Équivalence grosso modo** : *top-p=0.9* ≈ *top-k autour de 40–80* (dépend de la distribution).
* Si tu veux un **seul bouton** : prends **top-p=0.85–0.9** et laisse **k désactivé**.

### Raccourci pratique

* “Je veux du **sobre**” → **T=0.2 + top-k=40** (ou **top-p=0.85**).
* “Trop sec ?” → monte **k** (→60–80) ou **p** (→0.9).
* “Ça divague ?” → baisse **k** (→20–30) ou **p** (→0.8).
* 



<br/>

# Annexe 3



* **top-p** s’exprime en **probabilité** → une **valeur entre 0 et 1** (ex. 0.85 = 85 % de masse de proba cumulée).
* **top-k** n’est **pas un pourcentage** : c’est un **nombre entier** de candidats gardés (ex. k=40 = 40 tokens les plus probables).

### Mémo visuel

| Paramètre        | Unité  | Ce que ça garde                                           | Intuition                                 |
| ---------------- | ------ | --------------------------------------------------------- | ----------------------------------------- |
| **top-p = 0.80** | 0–1    | Tous les mots jusqu’à atteindre **80 %** de proba cumulée | Taille **variable** selon la distribution |
| **top-p = 0.90** | 0–1    | ~90 % de la masse                                         | Plus large que 0.80                       |
| **top-k = 20**   | entier | **20** mots les plus probables                            | Taille **fixe** (toujours 20)             |
| **top-k = 40**   | entier | **40** mots les plus probables                            | Plus de variété que k=20                  |

### Équivalences (approximatives, pour se repérer)

* Si la distribution est **concentrée** (un mot domine), **top-p=0.9** ≈ **top-k très petit** (souvent 2–5).
* Si elle est **étalée**, **top-p=0.9** peut correspondre à **top-k** beaucoup plus grand (souvent 30–80).
  ➡️ Donc on ne convertit pas **p → %** pour **k** : **p** vise une **part de probabilité**, **k** un **compteur** de mots.

### Raccourci pratique

* Réponses stables : **T=0.2 + top-p=0.85** *(ou)* **top-k=40**.
* Un seul bouton ? Choisis **top-p (0.85–0.9)** et laisse **k** désactivé.

