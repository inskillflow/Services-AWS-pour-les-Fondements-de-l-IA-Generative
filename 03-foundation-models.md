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


* **Foundation Model (FM)**  
  Grand modèle préentraîné, polyvalent, réutilisable sur beaucoup de tâches.  
  **Exemples** : GPT-4/4o (texte+image), Claude 3.x (texte), Gemini 1.5 (multimodal), Llama 3.x (ouvert).  
  **À quoi ça sert ?** Démarrer vite sans réentraîner un modèle de zéro (résumé, Q&A, extraction, chat).

* **LLM (Large Language Model)**  
  Modèle centré **texte/code** : comprend, reformule, écrit, structure.  
  **Exemples d’usages** :  
  – Réécrire un email professionnel court.  
  – Extraire des champs d’une facture en JSON.  
  – Expliquer un bout de code ligne par ligne.  
  **Mini-prompt** : `Explique ce paragraphe en 3 puces simples.`

* **VLM (Vision-Language Model)**  
  Modèle **multimodal** texte↔image : décrit, répond sur une image, OCR simple.  
  **Exemples d’usages** :  
  – Légender une photo de laboratoire.  
  – Lister les panneaux visibles sur une image de rue.  
  – Trouver les différences entre deux captures d’écran.  
  **Mini-prompt** : `Décris en 4 phrases ce graphique (image jointe).`

* **Modèle de diffusion (images)**  
  Génère des images par **débruitage progressif** (guidé par un prompt).  
  **Exemples** : SDXL/SD3, Flux, Playground.  
  **Réglages typiques** : steps (≈30), guidance (≈7), seed (reproductible).  
  **Mini-prompt** : `Portrait réaliste d’un violon sur table en bois, lumière douce, format 1536×1536.`

* **Embeddings**  
  Vecteurs numériques qui représentent le sens d’un texte (ou d’une image).  
  **À quoi ça sert ?** Recherche sémantique, RAG, détection de similarité.  
  **Exemple concret** : retrouver l’article le plus proche d’une question utilisateur.

* **Fenêtre de contexte**  
  Nombre **max de tokens** (morceaux de texte) que le modèle “voit” d’un coup.  
  **Impact** : plus de contexte = prompts plus longs, coûts/latence plus élevés.  
  **Repères** : courts (≈8k), moyens (≈32k), longs (≈200k+).  
  **Astuce** : résumer/segmenter les documents avant d’injecter.

* **Agentic AI (agents)**  
  Système qui **planifie → appelle des outils → vérifie → itère** avec des objectifs simples.  
  **Exemples d’outils** : recherche web interne, base de données, calendrier, API météo.  
  **Cas d’usage** : remplir un rapport hebdo en allant chercher des chiffres, puis se relire.

* **Guardrails (garde-fous)**  
  Règles/filtrages pour **sécurité et qualité** : bloquer PII, refuser contenus sensibles, valider un **format JSON**.  
  **Exemples** :  
  – Filtrer un prompt contenant des numéros de carte.  
  – Vérifier qu’une sortie respecte un schéma JSON avant d’envoyer.  
  – Réécrire en ton neutre et enlever les infos privées.

<br/>

### Exemples éclair express

* **LLM — extraction**  
  Entrée : `Nom: Marie, Tél: 06..., RDV: 12/11, Ville: Lyon`  
  Sortie attendue (JSON) : `{"nom":"Marie","telephone":"06...","date":"2025-11-12","ville":"Lyon"}`

* **VLM — description d’image**  
  Entrée : photo d’un ticket de caisse.  
  Sortie : `3 produits, total 18,30 €, date 05/09, magasin “Bio+”.`

* **Diffusion — bannière 16:9**  
  Prompt : `Paysage côtier au lever du soleil, style photo, brume légère, 2048×1152, sans texte.`

* **Embeddings + RAG**  
  Étapes : (1) convertir les PDF en vecteurs → (2) rechercher les 3 plus proches pour la question → (3) donner ces extraits au LLM pour répondre “ancré”.

<br/>

### Rappels ultra-simples

* **Choix rapide** : texte → LLM ; texte+image → VLM ; image à créer → diffusion.  
* **Contexte** : trop long coûte cher → résume ou découpe.  
* **Sécurité** : applique des **guardrails** sur entrée et sortie (PII, format).  
* **Agent** : commence avec 1–2 outils, limite les itérations, trace chaque action.


**Navigation** — ↩︎ [Revenir au plan](#plan-de-matière)

<br/>




# 3) Panorama rapide des modèles (GPT, Claude, Gemini, Llama/Mistral, Titan, SDXL…)

### Vue d’ensemble simplifiée

Les **modèles de fondation** sont aujourd’hui classés en grandes familles selon leur **type de données** (texte, image, multimodal) et leur **mode d’accès** (propriétaire ou ouvert).  
Le tableau ci-dessous te donne une lecture claire de l’écosystème actuel.

| **Famille** | **Modèles connus** | **Points forts (à retenir)** | **Points d’attention (à surveiller)** |
|--------------|--------------------|-------------------------------|----------------------------------------|
| **LLM (propriétaires)** | GPT-4 / GPT-4o (OpenAI), Claude 3.x (Anthropic), Gemini 1.5 (Google) | Très haute qualité, raisonnement fiable, outils intégrés (code, image, web), multimodalité | Coûts élevés, dépendance au fournisseur, limites d’usage (API fermée) |
| **LLM (ouverts)** | Llama 3.x (Meta), Mistral / Mixtral, Qwen, Phi-3 | Gratuits ou peu coûteux, rapides, exécutables localement ou sur cloud privé | Nécessitent configuration, maintenance, évaluation et sécurité manuelles |
| **VLM (Vision-Language)** | GPT-4o, Gemini multimodal, LLaVA | Comprennent texte + image, bonnes pour analyse visuelle ou OCR | Moins précises pour des images complexes ou du texte manuscrit |
| **Diffusion (image)** | SDXL / SD3 (Stability AI), Playground, Flux, Leonardo | Excellente créativité visuelle, contrôles fins (seed, style, guidance) | Maîtriser le prompt, les paramètres steps/guidance pour éviter dérives ou artefacts |
| **Entreprise (gouvernance)** | Amazon Titan, Cohere Command, Azure OpenAI | Intégration sécurisée, conformité, surveillance, SLA garantis | Plus restreints, souvent centrés sur le marché anglophone |



### Exemples illustratifs (débutants)

**1. LLM propriétaire – GPT-4o (OpenAI)**  
→ Chat intelligent, résumé, correction de texte, génération de code.  
**Prompt exemple :**

```
Explique ce code Python ligne par ligne et résume son but en une phrase.
```

**2. LLM ouvert – Llama 3 (Meta)**  
→ Déployable sur ton propre serveur ou PC local.  
**Cas typique :** assistant conversationnel privé sans fuite de données.

**3. VLM – Gemini ou GPT-4o**  
→ Analyse d’image, identification d’objets, lecture d’un document visuel.  
**Exemple :**  

```
Décris les éléments visibles sur cette photo et donne le nombre de personnes.
```

**4. Modèle de diffusion – SDXL / Playground**  
→ Génération d’images réalistes ou artistiques.  
**Exemple :**  

```
Portrait artistique d’un chercheur en IA devant un tableau de formules, style photo, lumière douce.
```

**5. Titan (AWS Bedrock)**  
→ Modèle textuel et visuel intégré à un environnement AWS sécurisé.  
**Cas d’usage :** résumé automatisé de documents internes, génération de descriptions produits en e-commerce.



### Comparatif express par tâche

| **Tâche** | **Modèle recommandé** | **Pourquoi ?** |
|------------|-----------------------|----------------|
| Résumer un texte | GPT-4 / Claude 3 | Fiabilité, structuration naturelle |
| Générer un texte créatif | Gemini 1.5 / Mistral 7B | Créativité, rapidité |
| Créer une image | SDXL / Flux / Playground | Contrôle artistique |
| Analyser une image | GPT-4o / Gemini multimodal | Vision + langage |
| Déploiement privé | Llama 3 / Mistral | Exécution locale, sécurité |
| Production entreprise | Titan / Cohere Command | SLA, conformité, traçabilité |



### À retenir

* **Propriétaires** = performance + support + coût.  
* **Ouverts** = liberté + ajustement + maintenance.  
* **Multimodaux** = texte + image dans un seul flux.  
* **Diffusion** = génération d’images créatives.  
* **Entreprise** = gouvernance, audit, intégration cloud.

**Conseil** : pour un étudiant débutant, commence par **GPT-4o ou Claude** pour le texte, puis expérimente **SDXL** pour les images avant d’explorer les modèles ouverts (Llama, Mistral).

**Navigation** — ↩︎ [Revenir au plan](#plan-de-matière)








<br/>





## 4) Entraînement, adaptation et gouvernance

### 4.1 Comprendre le cycle d’adaptation

Les modèles d’IA comme GPT-4o, Claude 3, Gemini 1.5 ou Mistral 7B peuvent être **personnalisés progressivement** selon le projet sans devoir les réentraîner complètement.  
On distingue quatre grands **niveaux d’adaptation**, du plus simple (prompting) au plus complexe (fine-tuning complet).

| **Niveau** | **Méthode** | **Principe** | **Quand l’utiliser** | **Exemple concret (Canada/US)** |
|-------------|-------------|---------------|----------------------|--------------------------------|
| 1️⃣ | **Prompting** | Modifier les instructions textuelles et fournir des exemples | Pour créer des assistants rapides (chatbots, générateurs de contenu) | Créer un assistant qui résume des offres d’emploi à Montréal ou Toronto |
| 2️⃣ | **RAG (Retrieval Augmented Generation)** | Ajouter des extraits de vos propres données à chaque requête | Pour relier un modèle à une base locale (PDF, BD, site web) | Assistant qui répond à partir de documents internes d’une entreprise tech canadienne |
| 3️⃣ | **Adapters légers (LoRA / QLoRA)** | Ne réentraîner qu’une petite partie du modèle | Pour spécialiser un LLM open-source à un domaine technique | Adapter Mistral pour comprendre le vocabulaire des startups SaaS nord-américaines |
| 4️⃣ | **Fine-tuning complet** | Réentraîner le modèle sur un corpus spécifique | Pour les grands projets institutionnels ou industriels | Entraîner un modèle sur les lois fiscales canadiennes ou les documents médicaux bilingues |



### 4.2 Étape 1 – Prompting (ingénierie d’instructions)

C’est la méthode la plus simple et la plus courante : tout se joue dans le texte que vous envoyez au modèle.  
Un bon prompt décrit clairement **le rôle**, **la tâche**, **le ton** et **le format** attendus.

#### Exemple 1 : analyse d’opportunités économique


```
Rôle : Analyste d'affaires.
Tâche : Résume les tendances de l'emploi en cybersécurité au Canada.
Format : 5 phrases, ton professionnel, avec une recommandation finale.
```

#### Exemple 2 : rédaction marketing

```
Rôle : Rédacteur IA.
Tâche : Rédige une courte description LinkedIn pour une startup IA basée à Montréal.
Contrainte : 250 caractères, ton optimiste et crédible.
```

#### Exemple 3 : génération de code

```
Rôle : Développeur Python senior.
Tâche : Crée un script Flask minimal pour recevoir et afficher un JSON envoyé par un client.
```

> ✅ **Avantage** : immédiat, accessible à tous, aucun coût d’entraînement.  
> ⚠️ **Limite** : le modèle oublie vos préférences si vous ne les redonnez pas à chaque fois.



### 4.3 Étape 2 – RAG (Retrieval Augmented Generation)

Le **RAG** permet de relier un modèle à **vos données réelles** : CV, rapports, sites, bases techniques.  
Le modèle lit des extraits précis au lieu de deviner.

#### Principe
1. Convertir vos documents en **embeddings** (vecteurs numériques).  
2. Rechercher les passages les plus pertinents selon la requête.  
3. Injecter ces passages dans le prompt avant de générer la réponse.

#### Exemple : assistant carrière canadien

```
Contexte :
<<<
Rapport de Emploi Québec : "Le salaire moyen en IA à Montréal a augmenté de 14 % entre 2021 et 2024."
> > >

Question :
Quelles régions canadiennes affichent la plus forte croissance des emplois IA ?

```
#### Exemple : documentation technique d’entreprise
```

Contexte :
<<<
README du projet API-Analytics :

* Endpoint : /v1/data
* Authentification : Bearer token

> > >

Question :
Comment authentifier un utilisateur dans cette API ?



> ✅ **Avantage** : réponses fiables et basées sur vos sources locales.  
> ⚠️ **Limite** : nécessite une petite base vectorielle (FAISS, Chroma ou Pinecone).



### 4.4 Étape 3 – Adapters légers (LoRA / QLoRA)

On peut affiner un modèle **open-source** (ex. Llama, Mistral) sans tout réentraîner.  
Seules quelques couches internes sont modifiées : c’est rapide et peu coûteux.

#### Exemple : adapter un modèle au vocabulaire technologique canadien
* Objectif : mieux comprendre les termes du secteur numérique (fintech, IA, cloud, DevOps).  
* Données : 800 paragraphes issus d’offres d’emploi IT à Montréal et Toronto.  
* Outils : `transformers` + `peft` (Hugging Face).  

```python
from peft import LoraConfig, get_peft_model
from transformers import AutoModelForCausalLM

model = AutoModelForCausalLM.from_pretrained("mistralai/Mistral-7B")
config = LoraConfig(r=8, lora_alpha=16, target_modules=["q_proj", "v_proj"])
lora_model = get_peft_model(model, config)
````

> ✅ **Avantage** : rapide, local, idéal pour adapter un modèle bilingue FR/EN.
> ⚠️ **Limite** : demande un GPU et un minimum de savoir-faire en IA appliquée.



### 4.5 Étape 4 – Fine-tuning complet (entraînement spécialisé)

Le **fine-tuning complet** est réservé aux grands projets institutionnels ou à la R&D.
Il consiste à réentraîner tout le modèle sur des données spécifiques (souvent des millions de lignes).

#### Exemple : modèle IA pour le marché du travail canadien

| Élément  | Description                                                     |
| -------- | --------------------------------------------------------------- |
| Objectif | Prédire les compétences les plus demandées au Canada d’ici 2030 |
| Données  | 100 000 offres d’emploi (Indeed, JobBank, LinkedIn)             |
| Étapes   | Nettoyage → Tokenisation → Entraînement supervisé               |
| Outils   | `transformers`, `accelerate`, GPU cloud                         |
| Durée    | Plusieurs jours                                                 |
| Coût     | Élevé (≈ 2 000 $ CAD sur GPU A100)                              |



### 4.6 Gouvernance et sécurité (contexte canadien et nord-américain)

#### Journalisation

* Enregistrer : le **prompt**, la **version du modèle**, les **paramètres**, la **date** et le **coût**.
* Exemple : conserver ces métadonnées dans un fichier CSV ou une base SQL.

#### Sécurité et conformité

* Respecter la **Loi 25** (Québec) et le **PIPEDA** (Canada).
* Ne jamais envoyer de données personnelles (nom, NAS, adresse).
* Héberger les données au Canada ou aux États-Unis (AWS Canada Central, Azure US East).
* Mettre en place des **guardrails** : filtrage du ton, contrôle JSON, détection de contenu inapproprié.

#### Évaluation continue

* Tester régulièrement les réponses du modèle sur des cas pratiques :

  * “Résume un article sur les startups en IA à Montréal.”
  * “Explique les avantages de migrer vers AWS Bedrock pour une PME.”
  * “Donne les 3 technologies IA les plus recherchées au Canada.”
* Mesurer la cohérence, la clarté, la factualité, et la neutralité du ton.


### 4.7 Mini-projet guidé (scénario techno-éducatif)

**Objectif** : créer un assistant IA qui aide les étudiants à découvrir les carrières technologiques au Canada.

**Étapes**

1. Créer un dossier `docs/` avec :

   * `emplois_ia_canada.txt`
   * `salaires_devops_2024.txt`
   * `fintech_montreal.txt`
2. Construire des embeddings pour ces fichiers.
3. Créer le prompt suivant :

   ```
   Contexte :
   <<< contenu extrait >>>
   Question : Quelles sont les 3 carrières en IA les plus prometteuses au Canada selon ces données ?
   ```
4. Appeler le modèle (GPT-4o, Claude 3, Gemini 1.5, Mistral).
5. Ajuster la **température** (0.2 → 0.8) et observer les variations de ton et de créativité.



### 4.8 À retenir

* Commencer **simple** : Prompting → RAG → LoRA → Fine-tuning.
* **Documenter** chaque test (prompts, modèles, paramètres, coûts).
* Respecter les **lois canadiennes** sur les données personnelles.
* Préférer des serveurs nord-américains pour les déploiements cloud.
* **Mesurer et auditer** régulièrement les performances et la neutralité du modèle.
* Penser “**carrière et innovation**” : chaque adaptation de modèle peut mener à un projet concret (ex. assistant d’embauche, moteur de recommandation, outil de veille technologique).

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


