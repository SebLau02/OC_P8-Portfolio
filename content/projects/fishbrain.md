---
slug: fishbrain
title: FishBrain Trivia
tagline: Quiz et mini-jeux pour pêcheurs, avec son back-office et son extension Chrome de sourcing
summary: >-
  Projet personnel de bout en bout : un site de jeux pour pêcheurs (blind test audio, « Devine le leurre »),
  un carnet de pêche privé, un back-office d'administration et une extension Chrome qui automatise
  la création des contenus (clips audio/vidéo, images de leurres détourées).
type: Site web + back-office + outil de sourcing
status: En ligne
period: "Septembre 2026 → aujourd'hui"
role: Conception, design et développement complet
team: Projet personnel (seul)
featured: false
tags: [Projet perso, Next.js, Cloudflare, Extension Chrome, Python, Jeu]
stack:
  frontend: [Next.js 16 (App Router), React 19, TypeScript, Tailwind CSS 4, shadcn/ui, Leaflet]
  backend: [Server Actions, Route handlers, Drizzle ORM, Neon Postgres, Zod]
  mobile: []
  infra: [Cloudflare Workers (OpenNext), Cloudflare R2, Cloudflare Turnstile, GitHub Actions]
  services: [Extension Chrome (Manifest V3), Python, yt-dlp, ffmpeg, rembg]
metrics:
  commits_perso: 50
  commits_total: 50
  premiere_contribution: 2026-09-25
  derniere_contribution: 2026-11-12
modules:
  - name: Site de jeux (front)
    description: "Interface mobile-first en thème sombre, pensée comme une application native."
    features:
      - "Blind test « Qui pèse le son ? » : lecteur audio, modes Carré (2 pts) et Duo (1 pt), vidéo de révélation, crédits des créateurs"
      - "« Devine le leurre » : silhouette à identifier, puis révélation en fondu de la photo détourée"
      - Écran de fin avec score et carte de partage, historique pour ne pas revoir les mêmes questions
  - name: Mon Carnet
    description: "Carnet de pêche privé : sorties, prises, spots sur carte, bredouilles."
    features: [Carte et spots (Leaflet), prévisions et conditions (marées, soleil, météo), photos et lecture des données EXIF]
  - name: Back-office (/admin)
    description: "Interface d'administration protégée pour valider les contenus avant publication."
    features:
      - Pré-écoute, ajout des 3 mauvaises réponses, vérification des crédits, passage de Brouillon à Publié
      - Gestion des leurres, remplacement d'image avec aperçu avant/après
      - Grilles triables et actions par ligne, contrainte SQL empêchant de publier une question incomplète
  - name: Extension Chrome de sourcing
    description: "Outil privé qui transforme une vidéo ou une image trouvée sur le web en contenu prêt à publier."
    features:
      - "Capture des timestamps (audio mystère et vidéo révélation) directement sur YouTube, TikTok ou Instagram"
      - "Clic droit sur une image : « Envoyer à FishBrain Trivia », marque et modèle, aperçu caché/révélé, validation"
      - Suivi des derniers envois, champs sauvegardés par URL, crédit de la chaîne récupéré automatiquement
  - name: Script local (Python)
    description: "Pipeline de traitement lancé sur le poste, appelé par l'extension et par le back-office."
    features:
      - yt-dlp et ffmpeg pour découper mystery.mp3 et reveal.mp4
      - Détourage des leurres (rembg) et génération de la silhouette
      - "Upload sur Cloudflare R2 puis création du brouillon via l'API du site (jeton Bearer)"
contributions:
  - "Conception complète : cahier des charges, design system (thème sombre, vert néon), architecture"
  - Site, jeux, carnet de pêche et back-office en Next.js / TypeScript
  - Extension Chrome Manifest V3 et script Python local pour automatiser le sourcing des contenus
  - Déploiement sur Cloudflare Workers, stockage R2, déploiement manuel via GitHub Actions
  - Protection anti-abus (limitation de débit WAF, Turnstile), pages légales et crédits, aucune donnée personnelle collectée
challenges:
  - "Industrialiser la création de contenu : passer d'un lien vidéo à une question publiable en quelques clics"
  - Tenir dans les limites de l'offre gratuite Cloudflare (taille du Worker, stockage, bande passante)
  - Faire dialoguer le navigateur, un script local et l'API du site de façon sécurisée (jetons, origines autorisées)
links:
  site: https://fishbrain-quiz.com/
  repo: privé
cover: projects/fishbrain/01-accueil.jpg
screenshots_layout: portrait
screenshots:
  - { src: "projects/fishbrain/01-accueil.jpg", alt: "Accueil", caption: "Accueil : les mini-jeux disponibles", kind: capture }
  - { src: "projects/fishbrain/02-blind-test.jpg", alt: "Blind test", caption: "Blind test « Qui pèse le son ? » : lecteur audio et choix du mode Carré ou Duo", kind: capture }
  - { src: "projects/fishbrain/03-devine-le-leurre.jpg", alt: "Devine le leurre", caption: "« Devine le leurre » : silhouette à identifier", kind: capture }
  - { src: "projects/fishbrain/04-recherche-leurre.jpg", alt: "Recherche d'un leurre", caption: "Recherche par marque ou modèle avec suggestions", kind: capture }
  - { src: "projects/fishbrain/05-extension-sourcing.jpg", alt: "Extension Chrome : clips", caption: "Extension Chrome : capture des extraits audio et vidéo, suivi des envois", kind: capture }
  - { src: "projects/fishbrain/06-extension-leurre.jpg", alt: "Extension Chrome : leurre", caption: "Extension Chrome : envoi d'une image de leurre (marque, modèle)", kind: capture }
  - { src: "projects/fishbrain/07-extension-apercu.jpg", alt: "Extension Chrome : aperçu", caption: "Extension Chrome : comparaison silhouette / leurre détouré avant enregistrement", kind: capture }
---

## Présentation
FishBrain Trivia est un projet personnel : un site de quiz et mini-jeux pour pêcheurs, en ligne sur fishbrain-quiz.com. Au-delà du jeu, l'enjeu était de pouvoir alimenter le site en contenu facilement, d'où un back-office et une extension Chrome conçus sur mesure.

## Le front
Une interface mobile-first en thème sombre, avec deux jeux (blind test audio et « Devine le leurre ») et un carnet de pêche privé. Le site est hébergé sur Cloudflare Workers, les médias sont servis depuis R2.

## Le back-office et l'extension Chrome
Le sourcing est la partie coûteuse d'un quiz : trouver, découper, héberger et renseigner chaque contenu. Je l'ai automatisé : l'extension Chrome capture les extraits sur la page, un script local découpe et traite les médias puis les envoie sur R2 et crée un brouillon via l'API. Il ne reste dans le back-office qu'à compléter les mauvaises réponses et publier.

## Mon rôle
Seul sur le projet : conception, design, front, back, outillage et déploiement.
