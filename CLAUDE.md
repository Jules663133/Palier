# Palier

Application web personnelle de suivi d'activité (patients vus, argent encaissé,
progression vers des paliers de revenu). Usage : iPhone, en PWA plein écran.

## Structure

Tout tient dans **`index.html`** : HTML, CSS et JavaScript dans un seul fichier.
Il n'y a ni build, ni dépendances, ni framework, ni fichier de test.

- `index.html` — l'application entière
- `render.yaml` — service statique Render (`staticPublishPath: .`, pas de build)
- `icon.png` — icône d'accueil iOS

## Déploiement — à faire à chaque fois

Render sert la branche **`main`** en statique et redéploie automatiquement à
chaque push. **Une modification n'est en ligne que si elle est sur `main`.**

Donc, à la fin de chaque tâche, sans le demander :

1. commiter sur la branche de travail ;
2. fusionner dans `main` (`--ff-only` de préférence, l'historique est linéaire) ;
3. `git push -u origin main`.

Pousser uniquement sur une branche de feature ne déploie rien.

## Conventions

- **Langue** : interface, commentaires et messages de commit en français.
- **JavaScript** : ES5, tout dans une IIFE `(function(){ "use strict"; ... })()`,
  `var` uniquement, pas de bibliothèque externe. Le style est compact
  (une instruction par ligne, peu d'espaces) — s'y conformer.
- **Persistance** : `localStorage`, clés `paliers_v2` (les jours) et
  `paliers_cfg_v2` (objectifs et paramètres de calcul). Changer la forme des
  données stockées efface l'historique de l'utilisateur : à éviter, ou prévoir
  une migration.
- **Typographie** : `Instrument Serif` pour les chiffres et les titres,
  `Inter` pour le reste (chargées depuis Google Fonts).
- **Couleurs** : variables CSS dans `:root` — `--pat` (vert, patients),
  `--money` (doré, argent), `--ink`, `--muted`, `--faint`, `--paper`.
- **Mise en page** : trois pages en `scroll-snap` vertical (accueil, stats,
  historique), largeur max 440 px, marges `env(safe-area-inset-*)` pour l'encoche.

## Vérifier une modification

Pas de suite de tests. Pour contrôler un changement visuel, ouvrir
`file:///.../index.html` dans Chromium (Playwright est disponible,
binaire : `/opt/pw-browsers/chromium-1194/chrome-linux/chrome`) en viewport
390×844, en pré-remplissant `localStorage` avec quelques jours pour peupler
l'historique.
