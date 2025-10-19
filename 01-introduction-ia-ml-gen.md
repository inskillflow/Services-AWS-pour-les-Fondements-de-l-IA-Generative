# Introduction — IA, ML et IA générative

*Fichier : `01-introduction-ia-ml-gen.md`*

## Plan de matière

1. [But du module](#1-but-du-module)
2. [Notions essentielles : IA, ML, IA générative](#2-notions-essentielles--ia-ml-ia-générative)
3. [Cycle de vie d’un système d’IA générative](#3-cycle-de-vie-dun-système-dia-générative)
4. [Entrées et sorties : données, consignes, formats](#4-entrées-et-sorties--données-consignes-formats)
5. [Paramètres de génération : effets clés](#5-paramètres-de-génération--effets-clés)
6. [Qualité et vérifications](#6-qualité-et-vérifications)
7. [Limites, risques et mesures](#7-limites-risques-et-mesures)
8. [Exemples concrets (texte, code, résumé, Q&A)](#8-exemples-concrets-texte-code-résumé-qa)
9. [Exercices et livrables rapides](#9-exercices-et-livrables-rapides)
10. [Résumé & check-list](#10-résumé--check-list)

---

## 1) But du module

* Situer clairement **IA**, **apprentissage automatique (ML)** et **IA générative**.
* Comprendre le **flux général** : *problème → données → modèle → génération → contrôle → amélioration*.
* Savoir configurer les **entrées** (contexte, consignes, contraintes) et analyser les **sorties** (structure, fidélité, utilité).

**Résultat attendu :** décrire et cadrer un usage d’IA générative de bout en bout.

**Navigation** — ↩︎ [Revenir au plan](#plan-de-matière)

---

## 2) Notions essentielles : IA, ML, IA générative

### 2.1 Définitions courtes

* **IA** : techniques permettant à une machine d’accomplir des tâches qui paraissent “intelligentes”.
* **ML** : sous-domaine de l’IA où un modèle **apprend des données** pour **prédire** (classe, valeur, groupe).
* **IA générative (GenAI)** : modèles capables de **produire** du contenu (texte, image, audio, code) à partir d’**instructions** et d’un **contexte**.

### 2.2 Différences clés

* **ML** “classique” : focalisé sur la **prédiction**.
* **GenAI** : focalisée sur la **génération** guidée par des consignes et des paramètres.

### 2.3 Vocabulaire minimal

* **Token** : petite unité de texte traitée par le modèle.
* **Fenêtre de contexte** : quantité maximale d’informations “vues” en une fois.
* **Hallucination** : sortie plausible mais **incorrecte**.

**Navigation** — ↩︎ [Revenir au plan](#plan-de-matière)

---

## 3) Cycle de vie d’un système d’IA générative

1. **Définir le besoin** : objectif, public, contraintes, format attendu.
2. **Sélectionner les données** : sources autorisées, nettoyage, anonymisation si nécessaire.
3. **Orchestrer** :

   * rédiger les **consignes** (rôle, tâche, format),
   * ajouter le **contexte** (extraits, références),
   * régler les **paramètres** (température, top-p, longueur).
4. **Générer** : appeler le modèle et récupérer la sortie.
5. **Contrôler** : vérifications automatiques et humaines (structure, exactitude, sécurité).
6. **Tracer** : conserver exemples, versions de consigne, paramètres.
7. **Améliorer** : itérer sur consignes, contexte, paramètres ou données.

**Navigation** — ↩︎ [Revenir au plan](#plan-de-matière)

<br/>

## 4) Entrées et sorties : données, consignes, formats

### 4.1 Entrées (à soigner)

* **Rôle** : “Tu es…”.
* **Contexte** : faits, définitions, extraits.
* **Tâche** + **critères** : ce qui doit être produit, niveau d’exactitude, concision.
* **Format** : puces, tableau, JSON, gabarit.
* **Contraintes** : longueur, ton, langue, références.

### 4.2 Sorties (à exiger)

* **Structure claire** (titres, sections, listes).
* **Références** ou mention d’**incertitude** si besoin.
* **Format respecté** ; sinon, **réviser l’entrée**.

**Navigation** — ↩︎ [Revenir au plan](#plan-de-matière)

<br/>

## 5) Paramètres de génération : comprendre avec des exemples simples

Quand tu utilises une IA générative (comme ChatGPT, DALL·E ou un autre modèle), tu peux **changer son comportement** grâce à quelques **paramètres essentiels**.
Voici ceux que tu dois connaître — avec **des explications faciles et des exemples concrets.**



### 5.1 Température — “plus froid” ou “plus chaud”

**Ce que ça fait :**
La *température* règle le **niveau de créativité** ou de **variabilité** des réponses.

| Température   | Effet                                     | Exemple                                                                                                                                      |
| ------------- | ----------------------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------- |
| **0.0 → 0.3** | Réponse très précise, presque “robotique” | Demande : “Donne-moi la capitale du Japon.” → Réponse : “Tokyo.”                                                                             |
| **0.7 → 1.0** | Réponse plus libre, imaginative           | Demande : “Décris la capitale du Japon.” → Réponse : “Tokyo, une ville où la tradition et la technologie se croisent sous un ciel de néons.” |

> **Astuce :**
>
> * Pour du **factuel** → garde la température **basse (0.1–0.3)**
> * Pour du **créatif** (idées, design, textes libres) → monte-la à **0.8–1.0**



### 5.2 Top-p et Top-k — “choix dans le vocabulaire”

Ces paramètres servent à **limiter le nombre de mots possibles** que l’IA peut choisir à chaque étape.

* **Top-k** = “Je choisis parmi les *k* mots les plus probables.”
  → Si `k=1`, elle est ultra stricte. Si `k=50`, elle peut improviser un peu plus.

* **Top-p** = “Je prends seulement les mots qui cumulent *p %* de probabilité.”
  → Si `p=0.9`, on garde les mots les plus logiques. Si `p=1.0`, tout est permis.

**Exemple concret :**
Tu veux un poème court sur le café.

| Réglage                      | Résultat                                                |
| ---------------------------- | ------------------------------------------------------- |
| `temperature=0.2, top_p=0.8` | “Le café chaud sur la table du matin.”                  |
| `temperature=0.9, top_p=1.0` | “Dans la vapeur dorée, un rêve se verse dans la tasse.” |



### 5.3 Max tokens — “la taille de la réponse”

**Ce que ça fait :**
Ce paramètre limite **la longueur du texte que l’IA peut écrire.**

| Exemple            | Résultat                                          |
| ------------------ | ------------------------------------------------- |
| `max_tokens = 50`  | Réponse courte : “Le soleil brille sur la ville.” |
| `max_tokens = 500` | Réponse longue : texte complet ou article entier. |

> **Astuce :**
>
> * Pour un résumé ou une définition → **100–300 tokens**
> * Pour un article ou un plan complet → **500–1000 tokens**



### 5.4 Stop sequences — “le frein d’urgence”

**Ce que ça fait :**
Tu peux dire à l’IA : **“arrête d’écrire quand tu vois cette phrase.”**

**Exemple concret :**

```json
"stop_sequences": ["### FIN"]
```

**Prompt :**

```
Donne-moi 3 étapes pour faire un gâteau.
Termine chaque étape sur une nouvelle ligne.
Quand tu as fini, écris “### FIN”.
```

→ L’IA s’arrête **exactement** à “### FIN”, sans continuer.



### 5.5 Résumé express (à retenir)

| Situation        | Réglage conseillé                                                        |
| ---------------- | ------------------------------------------------------------------------ |
| Fiche factuelle  | `temperature=0.2`, `top_p=0.8`, `max_tokens=200`                         |
| Résumé d’article | `temperature=0.3`, `top_p=0.9`, `max_tokens=500`                         |
| Idées créatives  | `temperature=0.9`, `top_p=1.0`, `max_tokens=700`                         |
| JSON structuré   | `temperature=0.1`, `top_p=0.8`, `max_tokens=400`, `stop_sequences=["}"]` |



## 6) Qualité et vérifications — comment savoir si ta sortie est “bonne”

### 6.1 Les 5 questions à se poser

1. **Est-ce que la réponse correspond à la question ?**

   > Tu demandes “Qu’est-ce qu’un volcan ?”
   > ❌ L’IA parle de la Lune → *hors sujet*
   > ✅ Elle parle de lave, cratère, éruption → *pertinent*

2. **Est-ce que c’est vrai ?**

   > Vérifie sur une source fiable (Wikipedia, dictionnaire, article scientifique).

3. **Est-ce que c’est clair ?**

   > Les phrases sont simples, structurées, et pas trop longues.

4. **Est-ce que le format est respecté ?**

   > Si tu as demandé “5 puces”, il doit y avoir **5 puces**.

5. **Est-ce que la réponse est traçable ?**

   > Si l’IA invente, fais-lui préciser :
   > *“Si tu n’es pas sûr, dis-le.”*



### 6.2 Exemples de vérification simple

| Cas             | Mauvais                                | Bon                        |
| --------------- | -------------------------------------- | -------------------------- |
| **Résumé**      | Trop long, 200 mots au lieu de 100     | 5 phrases claires, 90 mots |
| **Format JSON** | Fichiers invalides ou champs manquants | JSON valide et complet     |
| **Tonalité**    | Trop familière ou ironique             | Ton neutre, professionnel  |
| **Sources**     | “Je pense que…” (sans référence)       | “Selon NASA (2023)…”       |


<br/>

## 7) Limites, risques et solutions (avec exemples simples)

### 7.1 Hallucinations — quand l’IA invente

> **Exemple :**
> “Le président du Canada en 2023 était *Justin Bieber*.” ❌
> C’est une **hallucination** (réponse fausse mais dite avec assurance).

**Que faire :**

* Ajouter un **contexte clair** (“Réponds uniquement à partir de ce texte : …”).
* Exiger **des sources**.
* Baisser la **température**.



### 7.2 Biais et stéréotypes

> **Exemple :**
> “Les programmeurs sont toujours des hommes.” ❌
> Réponse biaisée.

**Que faire :**

* Formuler : “Donne une réponse **inclusive et neutre**.”
* Relire et **supprimer** tout mot discriminant.



### 7.3 Confidentialité

> **Exemple :**
> “Voici les coordonnées de M. Dupont : 514-…” ❌
> → Donnée privée.

**Que faire :**

* Masquer ou remplacer par `[Nom]`, `[Téléphone]`.
* Ne **jamais** coller d’information personnelle dans un prompt.



### 7.4 Dépendance au modèle

> **Exemple :**
> “Je ne peux pas répondre sans GPT-5.”
> → Tu deviens dépendant d’un modèle précis.

**Que faire :**

* **Sauvegarde** tes prompts et exemples dans un fichier.
* **Teste** avec plusieurs modèles pour comparer les résultats.



### 7.5 Coût et lenteur

> **Exemple :**
> Tu demandes : “Écris-moi 10 000 idées pour une start-up.”
> → Résultat : très long, très cher, peu utile.

**Que faire :**

* Limiter la taille (`max_tokens`).
* Demander d’abord **5 idées**, puis approfondir **une seule**.



### 7.6 Résumé en 3 phrases

1. Plus tu précises les **paramètres**, plus l’IA est prévisible.
2. Plus tu expliques ce que tu veux, plus la réponse est **fiable et claire**.
3. Vérifie toujours : **pertinence, exactitude, clarté, respect du format**.

**Navigation** — ↩︎ [Revenir au plan](#plan-de-matière)


<br/>

## 8) Exemples concrets (texte, code, résumé, Q&A)

Cette partie montre **comment donner une bonne consigne (entrée)** et **ce que l’IA doit produire (sortie)**.
Chaque exemple peut être **copié et modifié** pour s’entraîner.



### 8.1 Variations d’exercice



* **Entrée** : énoncé, niveau visé, contraintes (sans solution, durée ≤ 10 min).
* **Sortie** : 3 variantes (facile / moyen / difficile) en liste numérotée.


> **Objectif :** voir comment une même consigne peut donner trois niveaux de difficulté.

**Entrée**

```
Explique ce qu’est l’intelligence artificielle en 5 lignes maximum.
```

**Sortie attendue**

1. *(Facile)* L’intelligence artificielle, ou IA, est quand une machine imite l’intelligence humaine.
2. *(Moyen)* L’IA regroupe des programmes capables d’apprendre à partir de données pour accomplir des tâches sans être explicitement programmés.
3. *(Difficile)* L’IA désigne l’ensemble des méthodes permettant à une machine d’acquérir des capacités cognitives (raisonnement, perception, décision) grâce à l’apprentissage automatique et profond.

> **Astuce :** toujours demander plusieurs variantes pour comparer et comprendre le niveau de détail.


### 8.2 Résumé court

* **Entrée** : passage long + consigne “5 puces, ≤ 120 mots, citer 2 limites”.
* **Sortie** : 5 puces + 2 limites, sans opinion gratuite.


> **Objectif :** transformer un texte long en résumé clair et concis.

**Entrée**

```
Voici un article de 200 mots sur l’énergie solaire. Résume-le en 5 puces, maximum 120 mots, et cite 2 limites de cette technologie.
```

**Sortie attendue**

```
• L’énergie solaire provient de la conversion directe du rayonnement du soleil en électricité.  
• Les panneaux photovoltaïques sont la technologie la plus utilisée.  
• Elle réduit les émissions de CO₂ et la dépendance aux combustibles fossiles.  
• La production dépend de l’ensoleillement et du stockage disponible.  
• Les coûts baissent régulièrement grâce à l’innovation.  
Limites : production intermittente ; recyclage des panneaux encore complexe.
```

> **Astuce :** un bon résumé doit tenir sur **une demi-page**, sans phrases d’introduction inutiles.




### 8.3 Q&A cadré

* **Entrée** : question + **extrait** de référence.
* **Sortie** : réponse en 3–5 phrases + mention “*Réponse basée sur l’extrait fourni*”.


> **Objectif :** apprendre à répondre **à partir d’un extrait précis**, sans inventer.

**Entrée**

```
Extrait :
"Les plantes utilisent la photosynthèse pour transformer la lumière du soleil en énergie chimique."

Question :
Comment les plantes produisent-elles leur énergie ?
```

**Sortie attendue**

```
Les plantes produisent leur énergie grâce à la photosynthèse. 
Elles transforment la lumière du soleil en énergie chimique stockée dans leurs cellules.
*Réponse basée sur l’extrait fourni.*
```

> **Astuce :** répéter la phrase *« Réponse basée sur l’extrait fourni »* pour éviter les réponses inventées.


### 8.4 Gabarit d’instruction universel

```
Rôle : Tu es un rédacteur clair et exact.
Contexte : <résumé / extraits autorisés>
Tâche : Produis <type de rendu> couvrant <points indispensables>.
Format : <puces | tableau | JSON (schéma ci-dessous)>
Contraintes : longueur max, ton, langue, références si incertitude.
Exemples : <optionnel : 1–2 mini-démos>
Paramètres recommandés : température 0.2–0.4 pour factuel ; 0.7 pour créatif.
```


> **Ce modèle fonctionne pour TOUT : texte, code, résumé, tableau, image, etc.**

```
Rôle : Tu es un rédacteur clair et exact.  
Contexte : <donne ici les informations de base nécessaires>  
Tâche : Produis <le type de résultat> couvrant <les points indispensables>.  
Format : <texte | liste à puces | tableau | JSON>  
Contraintes : longueur, ton, langue, références si incertitude.  
Exemple : <1 ou 2 mini-démos si tu veux guider le style>  
Paramètres : température 0.2–0.4 pour un ton factuel ; 0.7 pour un ton plus créatif.
```

**Exemple concret d’utilisation**

```
Rôle : Tu es un professeur de sciences.  
Contexte : cours de biologie niveau secondaire.  
Tâche : Rédige 3 questions à choix multiples sur la photosynthèse.  
Format : liste numérotée.  
Contraintes : 1 seule bonne réponse par question, pas de vocabulaire avancé.  
Paramètres : température 0.3.
```

**Sortie**

```
1. Quelle est la principale source d’énergie des plantes ?  
   a) L’eau b) Le soleil c) L’oxygène → **b)**  
2. Quel gaz les plantes absorbent-elles pour faire la photosynthèse ?  
   a) CO₂ b) O₂ c) Azote → **a)**  
3. Que libèrent-elles dans l’air après la photosynthèse ?  
   a) Hydrogène b) Oxygène c) Azote → **b)**
```

> **Astuce finale :** plus ta consigne est claire, plus le résultat de l’IA sera juste.
> Évite les phrases vagues comme “Fais-moi un bon texte sur la nature” — précise **le but, la forme et la longueur.**





**Navigation** — ↩︎ [Revenir au plan](#plan-de-matière)








<br/>

## 9) Exercices et livrables rapides

### 9.1 Exercice 1

* **Cas d’usage (5 lignes)** : objectif, entrées, sorties, contraintes, contrôle.
* **Consigne stricte → sortie JSON** : clés obligatoires + un **exemple valide**.
* **Paramètres** : même demande avec température **0.2** puis **0.9** ; décrire l’écart en 3 lignes.

**Livrable suggéré :** `prompts/01-intro.json` avec :

* l’instruction finale,
* **3 entrées d’essai**,
* les **paramètres** recommandés.

**Navigation** — ↩︎ [Revenir au plan](#plan-de-matière)




<br/>



### 9.1 Exercice 2 — Exemple complet : “mauvais prompt ➜ JSON ➜ ajustements ➜ prompt final”

### 9.1.1. Étape 1 — Prompt **mal formulé** (étudiant)

```
fais un renard joli
```

* Tu obtiens une image (souvent moyenne).
* Tu demandes ensuite à **ChatGPT** de **convertir ce prompt en JSON** pour mieux spécifier ta demande.

** Phrase à copier dans ChatGPT (conversion → JSON)**

```
Convertis ce mauvais prompt en JSON normalisé pour génération d’image.
Mauvais prompt : "fais un renard joli"

Règles :
- Utilise ce schéma minimal et remplis les champs avec des valeurs raisonnables si manquantes :
{
  "subject": "",
  "intent": "",
  "pose_action": "",
  "environment": "",
  "background": "",
  "lighting": "",
  "composition": "",
  "color_tone": "",
  "width": 1920,
  "height": 1280,
  "negatives": "text, watermark, frame, blur, low-res, extra limbs",
  "variants": 3
}
- Ne renvoie que du JSON valide, sans aucun texte autour.
```

> **Astuce** : ne juge pas la première image ; l’objectif est d’améliorer la **spécification** via le JSON.



### 9.1.2. Étape 2 — Conversion en **JSON normalisé**

* Tu **ajoutes des champs** explicites (sujet, pose, lumière, décor…).
* Tu **ajustes des paramètres** (largeur/hauteur, variantes, interdits).

```json
{
  "subject": "renard roux adulte",
  "intent": "photo realiste",
  "pose_action": "portrait cadre poitrine, regard vers la camera",
  "environment": "foret",
  "background": "bokeh naturel, fond flou",
  "lighting": "lumiere doree de fin d'apres-midi",
  "composition": "centre, espace respirant",
  "color_tone": "couleurs naturelles, saturation moderee",
  "width": 1920,
  "height": 1280,
  "negatives": "text, watermark, frame, blur, low-res, extra limbs",
  "variants": 4
}
```

> **Rappel** : ce JSON est **ton interface simple**. Tu y contrôles **taille**, **pose**, **lumière**, **arrière-plan**, **couleurs**, **interdits**, etc.



## Étape 3 — **Ajustements** par l’étudiant (ex. changer format & pose)

* Tu **affines** les champs si besoin.
* Tu **modifies** les paramètres pour coller au rendu souhaité.

**Objectifs d’ajustement :**

* Passer au **format 16:9** → `2048×1152`
* Choisir **plein pied** (au lieu de portrait)
* Réduire à **3 variantes**

```json
{
  "subject": "renard roux adulte",
  "intent": "photo realiste",
  "pose_action": "plein pied, renard debout, regard vers la camera",
  "environment": "foret",
  "background": "bokeh naturel, fond flou",
  "lighting": "lumiere doree de fin d'apres-midi",
  "composition": "regle des tiers, sujet legerement a gauche",
  "color_tone": "couleurs naturelles, saturation moderee",
  "width": 2048,
  "height": 1152,
  "negatives": "text, watermark, frame, blur, low-res, extra limbs",
  "variants": 3
}
```

* Tu demandes à **ChatGPT** de transformer **ce JSON** en **prompt en langage naturel** (propre et complet).

** Phrase à copier dans ChatGPT (JSON → prompt naturel)**

```
Transforme ce JSON en prompt en langage naturel, propre et complet. 
Renvoie uniquement le prompt final (pas de JSON, pas de commentaires) et respecte exactement la taille et les interdits.

<colle ICI le JSON ajusté>
```

> **Mini-check avant finalisation** : sujet OK ? pose claire ? décor cohérent ? lumière adaptée ? taille correcte ? interdits présents ?



## Étape 4 — **Prompt final optimisé** (en langage naturel, à coller tel quel)

```
Photo réaliste d’un renard roux adulte en plein pied, debout, regard dirigé vers l’objectif.
Arrière-plan de forêt en bokeh (fond flou) pour isoler le sujet ; règle des tiers, renard légèrement décentré à gauche.
Lumière dorée de fin d’après-midi ; couleurs naturelles à saturation modérée.
Netteté prioritaire sur les yeux et la texture de la fourrure.
Aucun texte, watermark ni cadre ; éviter flou, basse résolution et artefacts anatomiques.
Format 2048×1152 (16:9). Générer 3 variantes.
```



#### Bonus — “Grille 30 secondes” (à garder sous la main)

* **Sujet** (espèce/âge) ✔︎
* **Pose/Action** ✔︎
* **Décor/Arrière-plan** ✔︎
* **Lumière** ✔︎
* **Composition/Cadrage** ✔︎
* **Couleurs/Tonalité** ✔︎
* **Taille/Format** ✔︎
* **Interdits (negatives)** ✔︎
* **Variantes** ✔︎

> Si un point manque → retourne au JSON, ajuste, régénère le prompt naturel, puis l’image.



<br/>






### 9.2 Exercice 3 — Exemple complet : “mauvais prompt ➜ JSON ➜ ajustements ➜ prompt final (autre scène)”

#### Objectif

Refaire exactement le même processus qu’en 9.1, mais avec une scène différente pour vérifier que la méthode est maîtrisée.

---

### 9.2.1. Étape 1 — Prompt mal formulé (étudiant)

```
un hibou dans la neige joli
```

* L’étudiant génère une première image (souvent moyenne).
* Il demande ensuite à ChatGPT de convertir ce prompt en JSON pour mieux spécifier sa demande.

Phrase à copier dans ChatGPT (conversion → JSON) :

```
Convertis ce mauvais prompt en JSON normalisé pour génération d’image.
Mauvais prompt : "un hibou dans la neige joli"

Règles :
- Utilise ce schéma minimal et remplis avec des valeurs raisonnables si manquantes :
{
  "subject": "",
  "intent": "",
  "pose_action": "",
  "environment": "",
  "background": "",
  "lighting": "",
  "composition": "",
  "color_tone": "",
  "width": 1920,
  "height": 1280,
  "negatives": "text, watermark, frame, oversaturated, blur, low-res, extra limbs",
  "variants": 3
}
- Ne renvoie que du JSON valide, sans aucun texte autour.
```



### 9.2.2. Étape 2 — Conversion en JSON normalisé

Exemple de JSON attendu (réponse de ChatGPT) :

```json
{
  "subject": "hibou des neiges",
  "intent": "photo realiste",
  "pose_action": "en vol, ailes deployees, regard vers l'objectif",
  "environment": "neige fraiche",
  "background": "paysage boreal, flou leger",
  "lighting": "lumiere froide diffuse",
  "composition": "regle des tiers, sujet legerement a droite",
  "color_tone": "neutre a froid",
  "width": 1920,
  "height": 1280,
  "negatives": "text, watermark, frame, oversaturated, blur, low-res, extra limbs",
  "variants": 3
}
```

Rappel utile :

* Le JSON est l’interface simple où l’on précise sujet, pose, décor, lumière, composition, tailles, interdits, variantes.
* Si un champ manque, on le complète avant de continuer.



### 9.2.3. Étape 3 — Ajustements par l’étudiant (exemple guidé)

Objectif des ajustements dans cet exemple :

* Passer en **format carré** (1536×1536) pour une vignette de cours.
* Remplacer la pose par un **gros plan** sur la tête.
* Réduire à **2 variantes** pour aller plus vite.

JSON ajusté par l’étudiant :

```json
{
  "subject": "hibou des neiges",
  "intent": "photo realiste",
  "pose_action": "gros plan de la tete, regard vers l'objectif",
  "environment": "neige fraiche",
  "background": "bokeh froid, flocons discrets",
  "lighting": "lumiere froide diffuse",
  "composition": "centre, espace respirant autour de la tete",
  "color_tone": "neutre a froid",
  "width": 1536,
  "height": 1536,
  "negatives": "text, watermark, frame, oversaturated, blur, low-res, extra limbs",
  "variants": 2
}
```

Phrase à copier dans ChatGPT (validation/ajustement du JSON) :

```
Prends ce JSON et vérifie qu’il est complet et cohérent. 
Si nécessaire, ajuste pour un rendu cohérent avec “photo réaliste” et format 1536×1536. 
Renvoie uniquement le JSON final, valide, sans texte autour.

<colle ICI ton JSON actuel>
```

Puis, pour obtenir le prompt en langage naturel :

Phrase à copier dans ChatGPT (JSON → prompt naturel) :

```
Transforme ce JSON en prompt en langage naturel, propre et complet. 
Renvoie uniquement le prompt final (pas de JSON, pas de commentaires) et respecte exactement la taille et les interdits.

<colle ICI le JSON ajusté>
```



### 9.2.4. Étape 4 — Prompt final optimisé (à coller tel quel)

```
Gros plan photo-réaliste d’un hibou des neiges, regard dirigé vers l’objectif. 
Neige fraîche, arrière-plan froid en bokeh avec flocons discrets pour isoler le sujet. 
Lumière froide diffuse ; netteté prioritaire sur les yeux et la texture du plumage. 
Couleurs neutres à froid, sans sursaturation. 
Aucun texte, watermark ni cadre ; éviter flou, basse résolution et artefacts anatomiques. 
Format 1536×1536. Générer 2 variantes.
```



### 9.2.5. Contrôles qualité et dépannage rapide

Contrôles qualité (à cocher) :

* Sujet correct et lisible (hibou des neiges clairement identifiable).
* Mise au point sur les yeux, texture du plumage visible.
* Arrière-plan cohérent (bokeh froid, pas de distraction).
* Lumière froide diffuse bien rendue, pas de saturation excessive.
* Taille exacte (1536×1536), nombre de variantes respecté.
* Interdits respectés (aucun texte, watermark, cadre, artefacts anatomiques).

Dépannage rapide :

* Image trop fade → autoriser un contraste légèrement plus élevé dans le JSON (ajouter `"contrast": "leger"` en note facultative si votre schéma l’autorise).
* Arrière-plan trop net → préciser dans le JSON `"background": "bokeh froid prononce"`.
* Trop de bruit/artefacts → ajouter dans les interdits `"grain, noise"`.
* Couleurs trop chaudes → réaffirmer `"color_tone": "neutre a froid"` et `"lighting": "lumiere froide diffuse"`.



### 9.2.6. Variantes avancées (facultatif)

Variante A — Action plus marquée :

```json
{
  "subject": "hibou des neiges",
  "intent": "photo realiste",
  "pose_action": "en vol rasant, ailes largement deployees",
  "environment": "neige fraiche",
  "background": "bokeh froid, silhouettes d’arbres floues",
  "lighting": "lumiere froide, leger contre-jour",
  "composition": "regle des tiers, sujet a gauche",
  "color_tone": "froid, sans sursaturation",
  "width": 2048,
  "height": 1152,
  "negatives": "text, watermark, frame, oversaturated, blur, low-res, extra limbs",
  "variants": 3
}
```

Variante B — Portrait posé sur un piquet :

```json
{
  "subject": "hibou des neiges",
  "intent": "photo realiste",
  "pose_action": "perche sur un piquet de bois, regard lateral",
  "environment": "neige tassee",
  "background": "bokeh froid uniforme",
  "lighting": "lumiere froide douce",
  "composition": "règle des tiers, sujet a droite",
  "color_tone": "froid naturel",
  "width": 1920,
  "height": 1280,
  "negatives": "text, watermark, frame, oversaturated, blur, low-res, extra limbs",
  "variants": 2
}
```

Prompts naturels correspondants (exemple de sortie) :

* Variante A :

```
Photo réaliste d’un hibou des neiges en vol rasant, ailes largement déployées. 
Neige fraîche, silhouettes d’arbres floues en arrière-plan (bokeh froid). 
Léger contre-jour avec lumière froide ; sujet placé selon la règle des tiers à gauche. 
Couleurs froides sans sursaturation. 
Aucun texte, watermark ni cadre ; éviter flou, basse résolution et artefacts anatomiques. 
Format 2048×1152. Générer 3 variantes.
```

* Variante B :

```
Portrait photo-réaliste d’un hibou des neiges perché sur un piquet de bois, regard latéral. 
Arrière-plan froid et uniforme en bokeh pour isoler le sujet. 
Lumière froide douce ; détails nets sur les yeux et le plumage. 
Couleurs froides naturelles, sans sursaturation. 
Aucun texte, watermark ni cadre ; éviter flou, basse résolution et artefacts anatomiques. 
Format 1920×1280. Générer 2 variantes.
```



### 9.2.7. Récapitulatif de la méthode (à afficher en haut de l’exercice)

1. Écrire un prompt simple (même mauvais).
2. Demander la conversion en JSON avec le schéma fourni.
3. Ajuster le JSON (pose, décor, lumière, taille, variantes, interdits).
4. Demander la conversion du JSON en prompt naturel propre.
5. Générer l’image.
6. Si le résultat n’est pas bon, revenir au JSON, changer 1–2 paramètres, régénérer le prompt, puis l’image.



















<br/>




## 9.3 Gabarits “copier → adapter” (toutes scènes) — version autonome

### 9.3.1. Point de départ minimal

**Mauvais prompt (tel quel)**

```
<ta phrase vague ici>
```

**Objectif**

* Demander à ChatGPT de convertir cette phrase en **JSON normalisé**, puis d’obtenir un **prompt en langage naturel** propre à partir de ce JSON.



### 9.3.2. Conversion phrase vague → JSON normalisé (à copier-coller)

```
Convertis ce prompt en JSON normalisé pour génération d’image.
Prompt : "<ta phrase vague>"

Règles :
- Utilise ce schéma et remplis avec des valeurs raisonnables si manquantes :
{
  "subject": "",
  "intent": "photo realiste",
  "pose_action": "",
  "environment": "",
  "background": "",
  "lighting": "",
  "composition": "",
  "camera_hint": "",
  "color_tone": "",
  "contrast": "",
  "motion": "",
  "width": 1920,
  "height": 1280,
  "negatives": "text, watermark, frame, oversaturated, blur, low-res, extra limbs, artifacts, noise",
  "variants": 3
}
- Renvoie uniquement du JSON valide, sans texte autour.
```

**Exemple de réponse attendue (illustratif)**

```json
{
  "subject": "renard roux adulte",
  "intent": "photo realiste",
  "pose_action": "portrait cadre poitrine, regard vers la camera",
  "environment": "foret",
  "background": "bokeh naturel, fond flou",
  "lighting": "lumiere doree de fin d'apres-midi",
  "composition": "centre, espace respirant",
  "camera_hint": "85mm, f/2.8",
  "color_tone": "couleurs naturelles, saturation moderee",
  "contrast": "modere",
  "motion": "",
  "width": 1920,
  "height": 1280,
  "negatives": "text, watermark, frame, oversaturated, blur, low-res, extra limbs, artifacts, noise",
  "variants": 3
}
```



### 9.3.3. Ajuster le JSON (format, pose, décor, etc.)

**Commande générique d’ajustement (à copier-coller)**

```
Prends ce JSON et ajuste :
- width/height : <nouvelle_taille>
- pose_action : "<nouvelle_pose>"
- environment : "<nouvel_environnement>"
- background : "<nouvel_arriere_plan>"
- lighting : "<nouvelle_lumiere>"
- composition : "<nouvelle_composition>"
- color_tone : "<nouvelle_tonalite>"
- contrast : "<leger|modere>"
- motion : "<file leger|freeze action>"
- variants : <nombre>

Renvoie uniquement le JSON final, valide, sans texte autour.

<colle ici ton JSON actuel>
```

**Exemples d’ajustements rapides**

* Passer en **16:9** : `width: 2048, height: 1152`
* Passer en **carré** : `width: 1536, height: 1536`
* Changer la **pose** : `pose_action: "plein pied, en marche"`
* Renforcer le **flou d’arrière-plan** : `background: "bokeh prononce"`
* Rester **sobre en couleur** : `color_tone: "neutre a froid"`
* Réduire les artefacts : ajouter dans `negatives`: `"grain, deformed"`

---

### 9.3.4. Transformer le JSON → prompt en langage naturel

**Commande (à copier-coller)**

```
Transforme ce JSON en prompt en langage naturel, propre et complet.
Renvoie uniquement le prompt final (pas de JSON, pas de commentaires) et respecte exactement la taille et les interdits.

<colle ici le JSON ajusté>
```

**Gabarit du prompt attendu (issu du JSON)**

```
Photo réaliste de <subject>, <pose_action>.
Décor : <environment>. Arrière-plan : <background>.
Éclairage : <lighting>. Ton : <color_tone><si contrast non vide : ; contraste <contrast>>.
<si motion non vide : Effet de mouvement : <motion>.>
Indices photo : <camera_hint>.
Netteté sur les zones clés (yeux / textures).
Interdits : aucun texte, watermark ni cadre ; éviter flou, sursaturation, basse résolution et artefacts.
Format <width>×<height>. Générer <variants> variantes.
```

> Si un champ du JSON est vide, il n’apparaîtra pas dans le prompt final.



### 9.3.5. Bibliothèque de valeurs utiles (pour remplir vite)

* **subject** : renard roux adulte | hibou des neiges | tigre du Bengale | manchot empereur | appareil photo vintage | plage rocheuse
* **pose_action** : portrait cadré poitrine, regard caméra | gros plan | plein pied, en marche | en vol, ailes déployées | assis, profil gauche
* **environment** : forêt de conifères | neige fraîche | prairie | dunes | bord de lac
* **background** : bokeh naturel, fond flou | bokeh froid prononcé, silhouettes d’arbres | fond uniforme flou
* **lighting** : lumière dorée de fin d’après-midi | lumière froide diffuse | contre-jour doux | éclairage studio doux
* **composition** : centré, espace respirant | règle des tiers, sujet légèrement à gauche/droite | diagonale dynamique
* **camera_hint** : 85mm, f/2.8 | 35mm, f/4 | 200mm, f/5.6
* **color_tone** : couleurs naturelles, saturation modérée | neutre à froid | pastel doux
* **contrast** : léger | modéré
* **motion** : filé léger | freeze action
* **negatives** (base) : text, watermark, frame, oversaturated, blur, low-res, extra limbs, artifacts, noise, deformed



### 9.3.6. Formats rapides

* Bannière 16:9 : 1920×1080 · 2048×1152
* Carré : 1536×1536
* Diapo 4:3 : 1600×1200
* Miniature web : 1280×720



### 9.3.7. Check-list qualité et dépannage

**Check-list**

* Sujet identifiable et net
* Pose/action claire
* Arrière-plan cohérent et assez flou
* Éclairage conforme
* Composition respectée
* Tonalité/contraste cohérents, pas de sursaturation
* Taille exacte (width×height) et nombre de variantes respecté
* Interdits appliqués (pas de texte, watermark, artefacts)

**Dépannage**

* Image “plate” → `contrast: "modere"`
* Arrière-plan distrayant → `background: "bokeh prononce"`
* Sujet flou → préciser “mise au point sur les yeux / texture”, retirer `motion`
* Couleurs trop chaudes → `color_tone: "neutre a froid"` + `lighting: "lumiere froide diffuse"`
* Artefacts/bruit → ajouter à `negatives`: `noise, artifacts, deformed`



### 9.3.8. Récapitulatif opérationnel

1. Coller **ta phrase vague**.
2. Demander la **conversion en JSON** (commande 9.3.2).
3. **Ajuster le JSON** (commande 9.3.3).
4. Obtenir le **prompt naturel** (commande 9.3.4).
5. Générer l’image.
6. Si besoin, revenir au **JSON**, changer 1–2 paramètres, régénérer le prompt, puis l’image.

<br/>

## 10) Résumé & check-list

### 10.1 À retenir

* **Contexte + Consignes + Format + Paramètres = Qualité**.
* Toujours imposer un **format vérifiable** (JSON / structure).
* **Documenter** consignes, versions et jeux d’essai.

### 10.2 Check-list avant exécution

* [ ] Objectif clair, public, contraintes
* [ ] Contexte fiable et suffisant
* [ ] Consigne structurée (rôle, tâche, format, contraintes)
* [ ] Paramètres adaptés (température / longueur)
* [ ] Vérification prévue (auto + humaine)
* [ ] Journalisation des exemples et résultats

**Navigation** — ↩︎ [Revenir au plan](#plan-de-matière)

