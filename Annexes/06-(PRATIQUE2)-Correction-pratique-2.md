# Correction — Pratique 2

## PARTIE 1 — COMPRÉHENSION THÉORIQUE (20 pts)

### 1.1 Définitions (6 pts)

1. **Intelligence artificielle (IA)**
   Sphère de méthodes permettant à une machine d’exécuter des tâches qui requièrent normalement des capacités dites “intelligentes” (perception, raisonnement, décision). L’IA recouvre plusieurs familles d’approches, dont règles symboliques, recherche heuristique et apprentissage.

2. **Apprentissage automatique (ML)**
   Sous-domaine de l’IA où un modèle **apprend** des relations à partir de données pour **prédire** une étiquette, une valeur ou une structure (classification, régression, clustering). Le performance dépend du jeu de données, des features et de la généralisation.

3. **IA générative (GenAI)**
   Classe de modèles capables de **produire** du contenu (texte, code, image, audio) à partir d’instructions et d’un contexte. La sortie n’est pas seulement prédictive mais **créative/constructive**, contrôlée par des paramètres (température, top-p, longueur, stop).

---

### 1.2 Cycle de vie d’un système d’IA générative (4 pts)

**Cas : générateur de résumés d’articles scientifiques**

| Étape                           | Action concrète                                                              | Exemple                                                                                                                |
| ------------------------------- | ---------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------- |
| 1. **Définir le besoin**        | Clarifier objectif, public, format, longueur                                 | “Résumé en 5 puces ≤120 mots pour étudiants de L3”                                                                     |
| 2. **Sélectionner les données** | Choisir sources autorisées, nettoyer, anonymiser                             | PDF de l’article + titre + abstract + sections autorisées                                                              |
| 3. **Orchestrer**               | Rédiger consigne (rôle, tâche, format), injecter extraits, régler paramètres | Prompt : rôle “rédacteur factuel”, 5 puces + 2 limites, `temp=0.2`, `top_p=0.85`, `max_tokens=200`, `stop=["### FIN"]` |
| 4. **Générer**                  | Appeler le modèle, récupérer la sortie                                       | Appel API → résumé Markdown                                                                                            |
| 5. **Contrôler**                | Vérifier exactitude, longueur, format, sources                               | Compter mots, vérifier 5 puces et 2 limites, pas d’info hors extrait                                                   |
| 6. **Tracer**                   | Journaliser consigne, version, paramètres, exemples                          | Logger prompt/params/outputs dans un dossier “runs/”                                                                   |
| 7. **Améliorer**                | Ajuster consigne/params/données selon écarts                                 | Ajouter consigne “signaler incertitudes”, baisser température                                                          |

---

### 1.3 Limites, risques et mesures (10 pts)

| Situation                                    | Type de risque                             | Mesure corrective                                                                             |
| -------------------------------------------- | ------------------------------------------ | --------------------------------------------------------------------------------------------- |
| “Le président du Canada est Justin Bieber.”  | **Hallucination / erreur factuelle**       | Exiger réponse **à partir d’un extrait** + **baisser température** + demander **sources**     |
| “Les programmeurs sont toujours des hommes.” | **Biais/stéréotype**                       | Formuler “réponse **inclusive et neutre**”, relire et supprimer éléments discriminants        |
| “Voici le numéro de Paul Tremblay : 514-…”   | **Confidentialité / données personnelles** | Anonymiser (`[Nom]`, `[Téléphone]`), interdire info privée dans le prompt                     |
| “Je ne peux répondre qu’avec GPT-5.”         | **Dépendance technologique**               | Sauvegarder prompts, **tester plusieurs modèles**, garder une couche d’orchestration portable |
| “Donne 10 000 idées de start-up.”            | **Coût/lenteur/verbosité**                 | **Limiter la taille** (max_tokens), demander d’abord **5 idées**, itérer sur la meilleure     |

---

## PARTIE 2 — PRATIQUE TEXTE (40 pts)

### 2.1 Expérience 1 — Température (15 pts)

**Prompt :** “Décris la ville de Tokyo en deux phrases.”
Params fixes : `top_p=0.9`, `max_tokens=100`

|   Temp. | Réponse modèle                                                                                                                                                                         | Observation                               |
| ------: | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ----------------------------------------- |
| **0.0** | Tokyo est la capitale du Japon. C’est une mégapole dense, centre politique et économique.                                                                                              | Très déterministe, factuel, peu de style. |
| **0.3** | Tokyo est la capitale du Japon, mêlant quartiers d’affaires et zones résidentielles. La ville est reconnue pour son réseau de transport efficace et sa forte densité.                  | Sobre, précis, légère variation possible. |
| **0.7** | Tokyo combine gratte-ciel étincelants et ruelles discrètes où la tradition persiste. Son rythme rapide s’adoucit dans les temples et les parcs qui ponctuent la ville.                 | Plus d’imagerie, créativité notable.      |
| **1.0** | Tokyo, archipel d’enseignes et de néons, pulse comme un cœur électrique au bord du Pacifique. Entre silence des sanctuaires et frénésie des carrefours, la ville réinvente chaque pas. | Très créatif/poétique, moins prévisible.  |

**Conclusion (exemple)**
Plus la **température** est élevée, plus la sortie devient **variée/imagée** mais moins prévisible.
Pour un rendu **factuel et stable**, préférer `0.1–0.3`. Pour un rendu **créatif**, viser `0.7–1.0`.

---

### 2.2 Expérience 2 — Top-p (10 pts)

**Prompt :** “Écris une phrase sur le café du matin.”
Paramètre fixe : `température=0.7`

|   Top-p | Réponse modèle                                                                      | Observation                           |
| ------: | ----------------------------------------------------------------------------------- | ------------------------------------- |
| **0.5** | Le café du matin réveille doucement l’esprit.                                       | Vocabulaire resserré, sobre.          |
| **0.9** | Le café du matin déplie les paupières et met de l’ordre dans les pensées.           | Plus de choix lexicaux, image légère. |
| **1.0** | Le café du matin verse une clarté tiède dans les idées encore froissées de la nuit. | Liberté maximale, plus de style.      |

**Conclusion (exemple)**
Un **top-p** plus bas contraint le **vocabulaire** et stabilise la phrase ; plus haut, il augmente la **richesse** mais aussi l’imprévisibilité.

---

### 2.3 Expérience 3 — Longueur & Stop (15 pts)

**Prompt :**
“Donne trois étapes pour préparer un gâteau.
Termine à ‘### FIN’.”
Params : `temp=0.3`, `top_p=0.8`, `stop=["### FIN"]`

| max_tokens | Résultat modèle                                                                                                                     |  Stop ? | Observation                       |
| ---------: | ----------------------------------------------------------------------------------------------------------------------------------- | :-----: | --------------------------------- |
|     **50** | 1) Mélanger œufs, sucre et beurre. 2) Ajouter farine et levure. 3) Verser dans le moule et cuire. ### FIN                           | **Oui** | Court mais suffisant.             |
|    **150** | 1) Préchauffer le four… 2) Fouetter œufs/sucre/beurre… 3) Incorporer farine/levure, verser, enfourner, vérifier la cuisson. ### FIN | **Oui** | Plus détaillé, toujours propre.   |
|    **400** | Liste détaillée avec variantes d’ingrédients, temps et conseils, puis “### FIN”.                                                    | **Oui** | Verbeux mais contrôlé par `stop`. |

**Conclusion (exemple)**
`max_tokens` plafonne la **longueur**, tandis que `stop` garantit une **coupure nette** au bon endroit. Même avec un budget long, `stop` évite les débordements.

---

## PARTIE 3 — PRATIQUE IMAGE (30 pts)

### 3.1 Prompt de départ (5 pts)

**Prompt :** “fais un renard joli”

**Observation**
Prompt vague → résultats aléatoires (style/pose/lumière non contrôlés). Manque de format, d’interdits et de composition.

---

### 3.2 Conversion en JSON normalisé (10 pts)

**JSON modèle attendu**

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
  "negatives": "text, watermark, frame, blur, low-res, extra limbs, artifacts",
  "variants": 3
}
```

---

### 3.3 Ajustement guidé 16:9 / plein pied / tiers / 3 variantes (10 pts)

**JSON ajusté (modèle)**

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
  "negatives": "text, watermark, frame, oversaturated, blur, low-res, artifacts",
  "variants": 3
}
```

**Prompt naturel final (modèle)**
“Photo réaliste d’un renard roux adulte en **plein pied**, debout, **regard dirigé vers l’objectif**.
Arrière-plan de **forêt** en **bokeh** (fond flou) pour isoler le sujet ; **règle des tiers**, renard légèrement décentré à gauche.
**Lumière dorée** de fin d’après-midi ; **couleurs naturelles** à saturation modérée.
Aucun texte, watermark ni cadre ; éviter flou, basse résolution et artefacts.
**Format 2048×1152 (16:9)**. **Générer 3 variantes**.”

---

### 3.4 Vérification (5 pts)

| Critère                     | Oui/Non attendu   |
| --------------------------- | ----------------- |
| Sujet clair et lisible      | Oui               |
| Arrière-plan cohérent       | Oui (bokeh forêt) |
| Éclairage conforme          | Oui (doré)        |
| Taille correcte (2048×1152) | Oui               |
| Absence de texte/watermark  | Oui               |

**Analyse type**
Le cahier des charges est respecté (pose, décor, lumière, ratio), et les **interdits** réduisent les artefacts. Si l’arrière-plan distrait, renforcer “bokeh prononcé”. Si couleurs trop chaudes, préciser “saturation modérée”.

---

## PARTIE 4 — CONCLUSION FINALE (10 pts)

1. La **température** contrôle le **degré de créativité/variabilité** des sorties.
2. Le **top-p** agit sur le **vocabulaire retenu** (nucleus sampling) ; le **top-k** sur le **nombre** de choix possibles.
3. Le **max_tokens** détermine la **longueur maximale** de la réponse.
4. La **stop sequence** permet une **coupure nette** lorsque la séquence apparaît.
5. Le **format JSON** garantit une **structure vérifiable** et exploitable automatiquement.
6. Un **prompt clair** améliore la **fidélité au cahier des charges** (exactitude, format, longueur, traçabilité).

---

### Remarques de notation rapides

* Des formulations différentes sont acceptées si **cohérentes et justificatives**.
* Pour la partie 2, le libellé exact des phrases peut varier ; on évalue **l’effet des paramètres** (et l’analyse).
* Pour la partie image, toute variante équivalente en JSON/prompt naturel est recevable si elle respecte **sujet/pose/décor/lumière/composition/format/negatives/variants**.
