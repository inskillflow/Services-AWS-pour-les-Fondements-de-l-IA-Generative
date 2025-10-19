# Modèles de fondation — Panorama, choix et usage (exemples détaillés)

*Fichier : `03-foundation-models.md`*

## Plan de matière

1. [But du module](#1-but-du-module)
2. [Notions essentielles et vocabulaire](#2-notions-essentielles-et-vocabulaire)
3. [Panorama rapide des modèles (GPT, Claude, Gemini, Llama/Mistral, Titan, SDXL…)](#3-panorama-rapide-des-modèles-gpt-claude-gemini-llamamistral-titan-sdxl)
4. [Entraînement, adaptation et gouvernance](#4-entraînement-adaptation-et-gouvernance)
5. [Choisir un modèle et un service](#5-choisir-un-modèle-et-un-service)
6. [Paramètres d’inférence — texte, code, image](#6-paramètres-dinférence--texte-code-image)
7. [Qualité, évaluations et sécurité](#7-qualité-évaluations-et-sécurité)
8. [Patterns modernes : RAG, outils, agents](#8-patterns-modernes--rag-outils-agents)
9. [Exemples détaillés (multi-fournisseurs, prêts à copier)](#9-exemples-détaillés-multi-fournisseurs-prêts-à-copier)
10. [Résumé & check-list](#10-résumé--check-list)

<br/>

## 1) But du module

* Comprendre ce qu’est un **modèle de fondation (FM)** et distinguer **LLM**, **VLM**, **diffusion**.
* Savoir **sélectionner** un modèle + **service d’accès** selon tâche, langue, coût, latence, sécurité.
* Maîtriser les **réglages d’inférence** et les **patterns** d’usage (RAG, outils, agents).

**Résultat attendu :** être capable de proposer un **panier “modèle + service + paramètres + contrôles”** pour un cas réel.

**Navigation** — ↩︎ [Revenir au plan](#plan-de-matière)

<br/>

## 2) Notions essentielles et vocabulaire

* **Foundation Model (FM)** : grand modèle préentraîné, polyvalent, réutilisable.
* **LLM** : modèle texte/code (raisonnement, Q&A, structuration).
* **VLM** : modèle multimodal texte↔image (analyse image, OCR léger, légendes).
* **Modèle de diffusion** : génération d’images par débruitage (SDXL, SD3).
* **Embeddings** : représentations vectorielles pour recherche/RAG.
* **Fenêtre de contexte** : tokens max visibles à l’inférence (impacte coûts/longueurs).
* **Agentic AI** : système qui **planifie → agit (outils) → vérifie → itère** de façon autonome guidée.
* **Guardrails** : contraintes de sécurité/qualité appliquées à l’entrée/sortie.

**Navigation** — ↩︎ [Revenir au plan](#plan-de-matière)

<br/>

## 3) Panorama rapide des modèles (GPT, Claude, Gemini, Llama/Mistral, Titan, SDXL…)

| Famille | Modèles | Points forts | Points d’attention |
|---|---|---|---|
| **LLM** (propriétaires) | GPT-4/4o, Claude 3.x, Gemini 1.5 | qualité, outils, multimodalité | coûts, dépendance fournisseur |
| **LLM** (ouverts) | Llama 3.x, Mistral/Mixtral, Qwen, Phi | coût/latence maîtrisables, on-prem | tuning/ops à prévoir, qualité variable |
| **VLM** | GPT-4o, Gemini multi, LLaVA | compréhension image + texte | robustesse inégale selon tâches |
| **Diffusion** | SDXL/SD3, Playground, Flux | contrôle créatif, écosystèmes riches | seed/steps/guidance à maîtriser |
| **Entreprise** | Amazon Titan, Cohere Command | gouvernance, SLA, intégrations | couverture langue/domaines |

**Navigation** — ↩︎ [Revenir au plan](#plan-de-matière)

<br/>

## 4) Entraînement, adaptation et gouvernance

**Chaîne d’adaptation**  
1) **Prompting** (ingénierie d’instructions)  
2) **RAG** (contextualisation par récupération)  
3) **Adapters légers** (LoRA/QLoRA)  
4) **Fine-tuning** ciblé (si vraiment nécessaire)

**Gouvernance minimale**  
* Journaliser : prompt, version modèle, paramètres, coûts.  
* Sécurité : PII, contenu sensible, refus normés.  
* Évaluation continue : jeux de tests internes + revue humaine.

**Navigation** — ↩︎ [Revenir au plan](#plan-de-matière)

<br/>

## 5) Choisir un modèle et un service

### 5.1 Critères concrets
* **Tâche** : résumé, extraction, code, analyse image, génération image.  
* **Langue/domaine** : FR requis ? secteur réglementé ?  
* **Contexte** : besoin long-context ? documents volumineux ?  
* **SLA & coût** : budget/tokens, latence cible, quotas.  
* **Implantation** : cloud public, région, on-prem, VPC.  
* **Outils & intégrations** : function/tool calling, bases, stockages.

### 5.2 Services (ne pas se limiter à un seul)
* **OpenAI** (GPT-4/4o, outils, embeddings)  
* **Google** (Gemini, prompt studio, VLM fort)  
* **AWS Bedrock** (Claude, Mistral, Titan, SDXL, guardrails, agents)  
* **Azure OpenAI** (gouvernance entreprise, réseau privé)  
* **Cohere** (Command, classement, RAG)  
* **Hugging Face** (Hub, Inference Endpoints, Spaces)  
* **Stability/Playground/Leonardo** (images)  
* **Lovable / PartyRock / Streamlit** (prototypage app GenAI)

**Navigation** — ↩︎ [Revenir au plan](#plan-de-matière)

<br/>

## 6) Paramètres d’inférence — texte, code, image

### 6.1 Texte/Code (LLM)
* **temperature** : créativité (0.1–0.3 factuel ; 0.7–1.0 créatif)  
* **top_p / top_k** : diversité lexicale (p/k plus bas = réponses plus serrées)  
* **max_tokens** : longueur de sortie max  
* **presence/frequency_penalty** : anti-répétition  
* **stop** : séquences d’arrêt (ex. `"}"` ou `"### FIN"`)

**Réglages rapides**  
| Tâche | temperature | top_p | max_tokens |
|---|---:|---:|---:|
| Fiche factuelle | 0.2 | 0.8 | 200 |
| Résumé article | 0.3 | 0.9 | 500 |
| Idéation | 0.9 | 1.0 | 600 |
| JSON strict | 0.1 | 0.8 | 300 |

### 6.2 Image (diffusion)
* **prompt / negative prompt**  
* **steps** (25–35 souvent suffisent)  
* **guidance** (6–8 équilibré)  
* **seed** (reproductible)  
* **width/height** (format/coût)

**Navigation** — ↩︎ [Revenir au plan](#plan-de-matière)

<br/>

## 7) Qualité, évaluations et sécurité

* **Qualité** : exactitude, complétude, format, style, citations/traçabilité.  
* **Évaluations** : jeux internes + métriques (texte : ROUGE/BLEU ; image : esthétique/CLIP).  
* **Sécurité** : guardrails entrée/sortie, détection PII, politiques de refus.  
* **Observabilité** : traces, coûts, latences, erreurs de parsing.  
* **Robustesse** : injections de prompt, ambiguïté, inputs adversariaux.

**Navigation** — ↩︎ [Revenir au plan](#plan-de-matière)

<br/>

## 8) Patterns modernes : RAG, outils, agents

* **RAG** : embeddings → recherche → contexte contrôlé → génération “ancrée”.  
* **Tool/Function Calling** : le modèle invoque des API (SQL, recherche, calcul).  
* **Agentic AI** : boucle **planifier → agir → vérifier → itérer** avec mémoire courte de tâche.  
* **Orchestration** : tracer chaque étape et verrouiller les sorties (validateurs JSON).

**Navigation** — ↩︎ [Revenir au plan](#plan-de-matière)

<br/>

## 9) Exemples détaillés (multi-fournisseurs, prêts à copier)

> Objectif : montrer **le même besoin** implémenté sur **plusieurs services** avec **réglages documentés**.  
> Note : exemples sans exercices, copiables tels quels, à adapter à votre pile.

### 9.1 Extraction structurée (avis produit → JSON)

**Consigne (gabarit)**
```

Rôle : Extracteur structuré.
Contexte : <coller l’avis texte ici>
Tâche : Extraire en JSON strict selon ce schéma :
{
"produit": "",
"points_forts": ["", ""],
"points_faibles": ["", ""],
"note": 0-5,
"citation_cle": ""
}
Contraintes : JSON valide uniquement, pas de texte hors JSON.
Paramètres : temperature=0.2, top_p=0.8, max_tokens=220, stop=["}\n"]

```

**OpenAI (pseudo-REST)**
```

model: "gpt-4o"
temperature: 0.2
top_p: 0.8
max_tokens: 220

```

**Google (Gemini)**
```

model: "gemini-1.5"
temperature: 0.2
top_p: 0.8
max_output_tokens: 220

```

**AWS Bedrock (Claude/Mistral)**
```

model: "anthropic.claude-3-..."/"mistral..."
temperature: 0.2
top_p: 0.8
max_tokens: 220

````

**Sortie attendue (exemple)**
```json
{
  "produit": "Casque X2",
  "points_forts": ["Confort", "Autonomie"],
  "points_faibles": ["Basses modestes", "Prix"],
  "note": 4,
  "citation_cle": "Très confortable au quotidien."
}
````

<br/>

### 9.2 Résumé fiable avec contraintes et citations

**Consigne**

```
Rôle : Rédacteur technique neutre.
Contexte autorisé :
<<<
<insérer 1–3 extraits>
>>>
Tâche : Résume en 5 puces factuelles et ajoute 2 limites.
Règles : Répondre seulement d’après le contexte. Si non couvert → “non couvert”.
Paramètres : temperature=0.3, top_p=0.9, max_tokens=240
Format :
• [fait 1]
• [fait 2]
• [fait 3]
• [fait 4]
• [fait 5]
Limites : [L1] ; [L2]
```

**Remarque** : pour long-context, choisir une variante du modèle avec fenêtre étendue avant d’augmenter `max_tokens`.

<br/>

### 9.3 Q&A “ancré” (RAG minimal)

**Pipeline**

1. Embeddings (e5/Instructor/Cohere)
2. Recherche top-k=4 (cosine)
3. Prompt avec extraits concaténés + consigne “réponds seulement d’après”

**Consigne**

```
Rôle : Assistant factuel.
Contexte :
<<<
[docA: ...]
[docB: ...]
>>>
Question : <...>
Règles : cite les sections si utilisées ; sinon “non couvert”.
Paramètres : temperature=0.2, max_tokens=230
```

**Sortie attendue**

```
Réponse : ...
Sources : docA §2 ; docB §4
```

<br/>

### 9.4 Multimodal (VLM) — Description d’image

**Consigne**

```
Rôle : Analyste d'image.
Image : <fichier joint>
Tâche : Décrire en 4 phrases : sujet, contexte, objets clés, incertitudes éventuelles.
Paramètres : temperature=0.2, max_tokens=180
```

**Services** : GPT-4o, Gemini multimodal, LLaVA (HF).

<br/>

### 9.5 Génération d’image — JSON → prompt naturel (diffusion)

**JSON canonique**

```json
{
  "subject": "renard roux adulte",
  "style": "photo realiste",
  "pose_action": "plein pied, debout, regard camera",
  "environment": "foret",
  "background": "bokeh naturel",
  "lighting": "lumiere doree de fin d'apres-midi",
  "color_tone": "naturel, saturation moderee",
  "width": 2048,
  "height": 1152,
  "negatives": "text, watermark, oversaturated, artifacts",
  "variants": 3
}
```

**Prompt dérivé**

```
Photo réaliste d’un renard roux adulte en plein pied, debout, regard vers l’objectif.
Forêt en arrière-plan avec bokeh naturel ; lumière dorée de fin d’après-midi ; tonalité naturelle, saturation modérée.
Aucun texte/watermark/artefact. Format 2048×1152. Générer 3 variantes.
```

**Paramètres diffusion (généraux)**
steps=30 ; guidance=7 ; seed fixe ; sampler DPM++ (selon service).

<br/>

### 9.6 Tool/Function Calling — Remplir un gabarit

**Consigne**

```
Rôle : Assistant outillé.
Tâche : Appeler la fonction `create_event({titre, date_iso, lieu})` si toutes les infos sont présentes dans le texte libre.
Texte : "<coller le texte utilisateur>"
Règles : Si info manquante → demander précisément la donnée manquante.
Paramètres : temperature=0.2, max_tokens=180
```

**Idée de test** : varier `temperature` 0.2 → 0.8 et observer la stabilité de l’appel.

<br/>

### 9.7 Agents — boucle courte contrôlée

**Patron**

```
Objectif : <but mesurable en 1-3 phrases>
Étapes cibles : Plan → Action(outil) → Vérif → Rapport
Bornes : 2 itérations max ; sources autorisées : <...> ; refus si hors périmètre
Paramètres : temperature=0.3, top_p=0.9, max_tokens=300
Sortie : plan final + journal condensé (1 ligne/étape)
```

**Astuce** : limiter l’itération et tracer chaque appel d’outil.

**Navigation** — ↩︎ [Revenir au plan](#plan-de-matière)

<br/>

## 10) Résumé & check-list

### À retenir

* **Choix modèle = tâche + langue + contexte + coût/latence + sécurité**.
* **Prompting + RAG + adapters** couvrent 80 % des besoins, avant le fine-tuning.
* **Paramètres** bas pour le factuel, plus hauts pour le créatif. Journaliser tout.

### Check-list express

* [ ] Tâche clarifiée et exemples d’entrées réels
* [ ] Modèle et service justifiés (SLA, coût, région)
* [ ] Paramètres d’inférence documentés
* [ ] Règles de sécurité/guardrails actives
* [ ] Évaluation interne et revue humaine prévues
* [ ] Observabilité/coûts/versionnement en place

**Navigation** — ↩︎ [Revenir au plan](#plan-de-matière)

```

