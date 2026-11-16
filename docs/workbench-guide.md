# BLUE — Workbench guide

Version documentaire : 0.1.0 — 2026-11-16
Statut : support initial évolutif ; conventions proposées sauf choix déjà exprimés. Aucun déploiement effectué.

## 1. Comment utiliser ce guide

Lis la rubrique utile au moment où tu en as besoin. Tu n’as pas à tout mémoriser ni à terminer une formation avant de développer BLUE.

Chaque terme technique est repris depuis la base. Une connaissance partielle est un acquis à consolider, pas une incapacité. Les corrections doivent expliquer précisément ce qui est juste et ce qui manque, sans jugement ni compliments vagues.

Sommaire :
- 2 : carte des outils
- 3 : fichiers et dossiers
- 4 : conventions et versions
- 5 : Markdown et JSON
- 6 : terminal et Bash
- 7 : Git et GitHub
- 8 : configuration et secrets
- 9 : Perplexity sans Computer
- 10 : travail avec Vibe
- 11 : tests et récupération
- 12 : Cloudflare et suivi partagé
- 13 : installation progressive de notre méthode
- 14 : lexique
- 15 : mini-test
- 16 : ressources

## 2. Carte des outils

Local = fichiers sur ton appareil. Git = historique local. GitHub = hébergement distant du dépôt. Perplexity = recherche, analyse et conception dans cette conversation. Vibe CLI = agent de développement dans ton environnement de terminal. Cloudflare = piste d’hébergement ultérieure.

Chaîne prévue : sources → analyse → présentation CDC/DB → validation → canvas d’affinage → réponses → DB et CDC candidats → validation → règles techniques → autorisation → prototype → tests → version.

Chaque transfert doit être explicite. Perplexity, Vibe, le dossier local et GitHub ne partagent pas automatiquement tout leur contexte.

Git a été créé par Linus Torvalds ; GitHub est un service distinct. Git fonctionne sans Internet. GitHub n’est pas une garantie absolue contre perte ou accès indésirable.

### Minimum utile maintenant

- Git et GitHub.
- Gestionnaire de fichiers et éditeur de texte existants.
- Markdown pour les documents ; bases de JSON pour les données.
- Terminal/Bash dans l’environnement existant pour Vibe, sans en faire une dépendance pour toutes les opérations.
- Navigateur du Redmi pour les essais.
- Perplexity et Vibe selon leurs rôles.

Cloudflare, outils de construction et tests automatisés seront introduits seulement selon la solution retenue. Aucun nouvel abonnement n’est autorisé par ce guide. Réinstallation de systèmes et refonte des comptes restent hors prérequis.

## 3. Fichiers et dossiers

Un fichier contient des données ; son extension indique une convention de format : .md, .html, .js, .json. Un dossier organise les fichiers. Une extension ne chiffre pas le contenu.

Racine du dépôt = dossier principal du projet. Chemin relatif = chemin depuis le dossier courant. Exemple : docs/project-status.md.

Rôles distincts :
- DB_BLUE.md : connaissances personnelles, provenance, situation et historique.
- docs/requirements.md : futur CDC, comportements et critères de vérification ; pas encore généré ici.
- docs/project-status.md : étapes de travail, décisions attendues et blocages.
- docs/workbench-guide.md : ce support pédagogique.
- README.md : point d’entrée du dépôt.
- LICENSE : conditions de licence ; ne pas modifier sans décision.

Ce ne sont pas plusieurs copies de la DB.

Structure future indicative, à valider :

```text
BLUE/
  README.md
  LICENSE
  .gitignore
  docs/
    project-status.md
    workbench-guide.md
    requirements.md     # futur
  src/                  # futur code
  tests/                # futurs tests
  public/               # uniquement contenu publiable si ce dossier est retenu
```

Données personnelles et sources originales : emplacement privé à décider avant migration. Ne pas copier automatiquement toute la DB dans le dépôt ou le dossier déployé. Un dossier public n’a rien de privé parce que le dépôt d’origine serait privé.

Originaux : conserver sans réécriture. Extractions : fichiers séparés. Copie importée dans Perplexity : instantané identifié par version/date, pas une seconde DB modifiable indépendamment.

### Organisation locale simple

- Un dossier de travail clairement identifié, pas plusieurs dossiers final/final2 concurrents.
- Éviter de travailler directement dans Téléchargements.
- Conserver une sauvegarde indépendante, en particulier pour les données ignorées par Git.
- Ne pas déplacer ou supprimer .git à la main.
- Avant de remplacer un document : vérifier son statut et préserver l’original si nécessaire.
- Si tu travailles sur deux appareils : synchroniser et vérifier les changements avant d’éditer les mêmes fichiers.

## 4. Nommage et versions

Choix de direction : noms techniques anglais ; explications et contenu personnel en français. Nommage détaillé à valider avec la chaîne de production.

- Fichiers ordinaires : minuscules et tirets, exemple project-status.md. C’est du kebab-case.
- README.md est une convention reconnue ; SUIVI.md n’était pas une obligation. Les majuscules ne donnent aucun pouvoir spécial au fichier.
- camelCase : identifiants possibles en JavaScript, exemple currentTask.
- PascalCase : convention possible pour composants/classes, exemple TaskCard.
- BEM : convention CSS block__element--modifier, pas structure HTML ou système de dossiers.
- Éviter espaces et accents dans les chemins techniques pour simplifier les commandes.
- Garder DB_BLUE.md tant qu’un renommage n’est pas validé.

Garder des noms stables pendant le travail : requirements.md, pas final-final2.md. Git conserve les révisions.

Une livraison peut être nommée blue-prototype-v0.1.0.html. C’est une proposition, pas la convention finale. x.y.z peut représenter changement majeur / ajout compatible / correction selon la politique approuvée. Avant 1.0, préciser notre politique plutôt que supposer une stabilité.

Ne pas confondre :
- version documentaire ;
- version de l’application ;
- identifiant de commit ;
- date d’export ;
- statut candidat ou approuvé.

Date non ambiguë : YYYY-MM-DD. Une date de modification seule ne prouve pas qu’un fichier est la référence.

## 5. Markdown et JSON

Markdown est du texte lisible avec une mise en forme légère. GitHub peut l’afficher.

```markdown
# Titre
## Rubrique
- élément
- [ ] à faire
- [x] terminé
[libellé](adresse)
```

Pour modifier une case du suivi : remplacer [ ] par [x], puis enregistrer la modification dans un commit. Ne cocher qu’une action réellement effectuée.

GitHub : ouvrir le fichier, utiliser l’édition si disponible avec ton rôle, relire l’aperçu/diff puis enregistrer. Selon l’interface mobile, utiliser l’affichage navigateur complet. Conserver un message de commit compréhensible.

JSON structure des données avec objets, listes, chaînes et nombres. Exemple fictif :

```json
{"id":"task-demo","title":"Lire une page","status":"todo"}
```

Les guillemets, virgules et types comptent. Le JSON standard n’accepte pas les commentaires. Les données réelles devront suivre un schéma ; modifier un champ ne suffit pas à mettre à jour tous les liens automatiquement.

## 6. Terminal et Bash

Terminal = application d’interaction textuelle. Shell = interpréteur des commandes. Bash = un shell et un langage de script, pas le noyau Linux.

```bash
pwd             # afficher le dossier courant, pas un mot de passe
ls              # fichiers et dossiers non masqués
ls -la          # liste détaillée avec fichiers masqués
ls -R           # parcourir les sous-dossiers
ls -r           # inverser l’ordre du tri
cd chemin       # changer de dossier
cd ..           # remonter au dossier parent
```

~ = dossier personnel ; . = dossier courant ; .. = parent. Un chemin absolu commence à la racine / sous Linux ; un chemin relatif dépend du dossier courant.

Une commande comporte un programme, des options et des arguments. Exemple : git diff -- docs/project-status.md. Les chemins avec espaces demandent une protection correcte, souvent des guillemets.

Avant exécution : comprendre le dossier cible, les fichiers concernés, l’effet et la possibilité de retour arrière. Ne pas coller un long bloc inconnu. Pas de sudo, rm, reset --hard, clean ou force-push par réflexe.

## 7. Git et GitHub

Working tree = fichiers de travail. Index/staging area = contenu préparé pour le prochain commit. Commit = instantané local enregistré. Branch = branche de développement. Remote = dépôt distant configuré ; origin est un nom courant, pas obligatoire.

Cycle de consultation et enregistrement, une fois le dépôt configuré :

```bash
git status
git diff
git add docs/project-status.md
git diff --staged
git commit -m "docs: update project checklist"
git push
```

- status : situation des fichiers suivis/non suivis et changements.
- diff : changements non préparés ; ce n’est pas toujours la comparaison au dernier commit pour tout le contenu.
- add : prépare le contenu actuel du fichier ; ne crée pas de branche.
- diff --staged : contenu réellement prévu pour le commit.
- commit : enregistrement local ; aucune publication automatique.
- push : envoi au distant configuré ; suppose accès et branche amont adaptés.

Autres commandes :

```bash
git log --oneline -5   # derniers commits
git ls-files          # chemins suivis
git diff --check      # certaines erreurs d’espaces, pas un test fonctionnel
```

clone copie le dépôt et son historique. fetch récupère les références distantes sans intégrer aux fichiers courants. pull récupère puis intègre selon la configuration ; en cas de divergence, s’arrêter et examiner plutôt que forcer.

Un commit cohérent peut contenir plusieurs fichiers. Un commit réussi ne prouve pas que les tests passent.

### Sauvegarde et retour arrière

Git peut fonctionner hors ligne, y compris pour consulter l’historique. GitHub n’est pas indispensable au retour arrière local. Perdre le disque contenant l’unique dépôt peut toutefois détruire travail et historique.

Consulter un ancien état ne signifie pas forcément remplacer toute la version courante. Sur un historique partagé, un revert peut produire une annulation traçable ; choisir la commande seulement après avoir examiné l’état réel et protégé le travail non commité.

Une copie indépendante reste nécessaire pour les données non suivies, les secrets protégés et la récupération après incident. Synchroniser n’est pas toujours sauvegarder : une erreur peut aussi se propager.

## 8. .env, .gitignore et secrets

Les noms commençant par un point sont généralement masqués par défaut sous Linux. Ils ne sont pas chiffrés.

### .env

Fichier texte de configuration selon les outils. Exemple fictif :

```dotenv
MISTRAL_API_KEY=replace_locally
APP_MODE=development
# commentaire
```

Forme habituelle NOM=valeur. Règles exactes de guillemets et chargement : selon le programme. Créer .env ne le charge pas automatiquement. La configuration exacte de ta version de Vibe reste à vérifier ; cet exemple n’est pas une instruction d’installation de Vibe.

Une variable d’environnement est transmise à un processus. .env n’est qu’une méthode possible pour fournir des valeurs.

### .gitignore

Fichier texte de motifs excluant les fichiers non suivis. Il ne dépend pas d’un langage unique ; les modèles GitHub sont des aides facultatives.

Exemple de base adopté pour ce dépôt après approbation :

```gitignore
.env
.env.*
!.env.example
*.log
```

# = commentaire ; * = motif ; ! = exception. Un / final désigne un dossier.

.gitignore est lui-même versionnable. Il ne chiffre rien, ne supprime pas un fichier déjà suivi et n’efface pas les anciens commits.

.env.example : modèle avec noms des variables mais aucune vraie clé. Une clé publiée doit être révoquée/remplacée ; supprimer la ligne ne suffit pas.

Une clé API ne doit jamais se retrouver dans le HTML, le JavaScript public, une URL, un export ou une capture. Une variable injectée dans le code du navigateur n’est pas un secret. L’intégration IA finale devra utiliser une architecture appropriée, pas une clé cachée visuellement.

## 9. Perplexity Project sans Computer

Ce workflow vise les conversations, sources et outils disponibles ici, sans dépendance au produit Computer. Les possibilités réelles et limites de ton compte prévalent.

### Instructions du projet

Règles durables : langue, méthode, sources de référence, validations, pas d’action externe sans accord. Pas l’endroit où recopier toute la DB.

### Fichiers et sources

Documents persistants utilisés comme contexte. Présence ne signifie pas lecture intégrale. Demander chemins examinés, couverture et limites.

Les imports depuis un connecteur sont des copies ponctuelles : pas de synchronisation vivante garantie. Pour travailler sur la référence GitHub actuelle, demander sa lecture via le connecteur.

### Conversations parallèles

Séparer conception et exploration est possible. Ne pas supposer accès intégral à tous les échanges. Rapporter les conclusions dans un bilan ou document validé.

### Connecteurs, plugins et MCP

Connecteur = liaison autorisée à un service. Plugin = ensemble d’outils/instructions rendu disponible selon l’interface. MCP = protocole de connexion d’outils, pas un stockage ou agent autonome en lui-même.

GitHub est connecté au moment de la préparation de ce guide ; lecture de la racine et branche main vérifiées. Une écriture n’est attestée qu’après résultat de l’action et vérification.

Authentification au compte, autorisation du dépôt et choix de notre référence sont trois choses distinctes. Ne jamais donner des permissions plus larges que nécessaire pour résoudre une erreur sans examen.

Les outils disponibles ici peuvent lire fichiers et historique et préparer des modifications. Toute écriture externe doit être approuvée avec son contenu exact. Connexion ne signifie pas surveillance permanente ou modifications en arrière-plan.

### Brain / mémoire, Skills et automatisations

La documentation actuelle décrit une mémoire Brain avec mise à jour manuelle ou périodique et des réglages de projet ; vérifier leur présence dans ton interface. Cette mémoire ne remplace ni la DB ni le registre des décisions.

Des rubriques Skills/Plugins peuvent exister selon l’offre et l’interface. Leur disponibilité ne sera pas présumée et notre chaîne ne doit pas en dépendre.

Les agents continus Teammates décrits dans la documentation reposent sur Computer ; hors solution retenue. Ne pas promettre de synchronisation autonome du suivi.

### Réglages proposés pour BLUE

- Projet privé ; dépôt et chemins de référence explicitement indiqués.
- Sources candidates/approuvées identifiées ; anciennes versions non ambiguës.
- Manifeste indiquant référence, version, emplacement et copie importée.
- Web : recherches ciblées et sources officielles pour les faits importants.
- Pas d’import de clés, logs sensibles ou totalité des données par défaut.
- Connecteurs supplémentaires seulement si utiles ; aucun MCP personnalisé nécessaire actuellement.

Les modifications de paramètres Perplexity restent manuelles sauf outil explicitement disponible. La connexion du dépôt ne transfère pas automatiquement les sources du projet dans GitHub.

## 10. Travailler avec Vibe CLI

Environnement déclaré : terminal sous Pop!_OS, usage de Bash. Version de Vibe et configuration à vérifier avant instructions spécifiques.

Avant la session : vérifier dossier, git status et fichiers de référence. Donner objectif, fichiers modifiables, limites et critères de réussite.

Exemple : « Lis le CDC et le suivi de référence. Propose les changements avant modification. Ne modifie pas les originaux ou données privées hors périmètre. Donne les fichiers touchés, les commandes de test, leurs résultats et limites. Ne publie rien sans accord. »

Après : examiner diff, sorties des tests et essai concret sur Redmi. Un message “corrigé” n’est pas une preuve suffisante. Distinguer test proposé, exécuté, réussi et non effectué.

Transmettre à Vibe les fichiers et décisions exacts : il ne connaît pas automatiquement cette conversation. Le code généré n’est pas nécessairement exécuté ou testé.

Développement CLI et API utilisée par BLUE sont deux origines de consommation à suivre séparément. Abonnements, crédits et facturation exacte restent à vérifier, sans supposer qu’un abonnement couvre l’API.

## 11. Tests et incidents

Pour chaque test : contexte, action, résultat attendu, résultat observé, version/appareil, statut et limite.

Exemple : modifier une note → fermer/réouvrir → vérifier sa conservation. Ce test ne valide pas à lui seul restauration ou synchronisation.

Avant intégration : navigation, saisie, annulation d’erreur, persistance, export/import et absence de secrets. Les tests doivent correspondre au périmètre réellement implémenté.

En cas d’erreur : s’arrêter, préserver le travail, noter les étapes et le message exact, comparer au dernier état connu. Ne pas empiler des corrections non vérifiées.

## 12. Cloudflare et suivi partagé

Cloudflare Pages peut publier un site et redéployer après push GitHub. Rien n’est configuré ici. Un dépôt privé ne rend pas automatiquement privé le site déployé.

HTML local avec localStorage : état dans ce navigateur, pas partagé.
HTML hébergé : même adresse de consultation, pas nécessairement état partagé.
Application avec état central : stockage, authentification, écritures et conflits à concevoir.

Pour le moment, docs/project-status.md dans GitHub est proposé comme référence. Une vue HTML peut en être dérivée ultérieurement ; ne pas éditer deux listes indépendantes.

Je dois relire le fichier via un outil pour connaître son état actuel ; pas de surveillance continue. Pour écrire, une approbation et un outil autorisé restent nécessaires. Aucun token GitHub dans un HTML.

Avant déploiement : choisir branche et seul dossier destiné au public, vérifier données et secrets, comprendre accès et conditions tarifaires. Build command et output directory dépendent de la pile retenue.

Workers, bases de données, contrôle d’accès et CI automatisée : pistes ultérieures, pas prérequis. Aucun achat ou publication autorisé par le présent document.

## 13. Mise en place progressive

1. Vérifier dépôt, branche et contenu existant.
2. Ajouter guide, suivi et exclusions approuvés.
3. Relire ces références avant mise à jour.
4. Continuer analyse des sources et CDC, sans attendre une formation complète.
5. Valider plus tard les conventions et l’architecture définitives.

État initial du dépôt inspecté : README.md et LICENSE à la racine, branche main. Leur contenu et leurs conditions n’ont pas été audités dans ce travail ; aucun remplacement proposé.

## 14. Lexique anglais–français

| Anglais | Français / sens |
|---|---|
| repository / repo | dépôt |
| working tree | fichiers de travail |
| source of truth | référence faisant autorité |
| staging area / index | sélection du prochain commit |
| stage | préparer pour le commit |
| commit | instantané enregistré localement |
| branch | branche |
| remote | dépôt distant configuré |
| clone | copier un dépôt et son historique |
| fetch | récupérer les références distantes |
| pull | récupérer puis intégrer |
| push | envoyer les commits |
| tracked / untracked | suivi / non suivi |
| ignored | exclu selon les règles Git |
| backup / restore | sauvegarde / restauration |
| release | version livrée |
| deployment | déploiement |
| build | construction du livrable |
| frontend / backend | interface navigateur / service serveur |
| environment variable | variable d’environnement |
| requirements | exigences / cahier des charges |
| acceptance criteria | critères d’acceptation |
| issue | ticket de tâche ou problème |
| changelog | journal des changements |
| mock | simulation |
| rollback | retour à une version précédente |
| cheat sheet | fiche de référence rapide |

## 15. Mini-test sans note

1. Un commit publie-t-il sur GitHub ?
2. .gitignore efface-t-il une clé des anciens commits ?
3. Que fait git add ?
4. Un HTML hébergé partage-t-il automatiquement son localStorage ?
5. Que fait pwd ?
6. Une source Perplexity importée suit-elle toutes les modifications GitHub ?

<details>
<summary>Corrections</summary>

1. Non : commit local ; push pour envoyer.
2. Non : révoquer la clé et examiner l’historique avec une procédure adaptée.
3. Prépare le contenu pour le prochain commit.
4. Non : stockage propre au navigateur et à l’origine.
5. Affiche le dossier courant.
6. Non : copie ponctuelle, relire la référence actuelle.

</details>

## 16. Ressources officielles

- Git : https://git-scm.com/docs
- Git, enregistrer les changements : https://git-scm.com/book/en/v2/Git-Basics-Recording-Changes-to-the-Repository
- Gitignore : https://git-scm.com/docs/gitignore
- GNU ls : https://www.gnu.org/software/coreutils/manual/html_node/ls-invocation.html
- Perplexity Projects : https://www.perplexity.ai/help-center/en/articles/10352961-what-are-projects
- Perplexity GitHub : https://www.perplexity.ai/help-center/en/articles/12275669-github-connector-for-enterprise
- Perplexity MCP : https://www.perplexity.ai/help-center/en/articles/11502712-local-and-remote-mcps-for-perplexity
- Cloudflare Pages : https://developers.cloudflare.com/pages/configuration/git-integration/
- MDN : https://developer.mozilla.org/fr/
- Mistral : https://docs.mistral.ai/ — trouver les instructions correspondant à la version de Vibe utilisée.

Les offres, interfaces et outils évoluent ; revérifier les points opérationnels avant configuration. Ce document n’atteste aucune synchronisation, aucun test du prototype et aucun déploiement.
