# PWA web d'abord dans un monorepo TypeScript, Supabase en backend

Monorepo TypeScript (pnpm, Turborepo) avec packages partagés. La v1 est un **client Next.js en PWA** installable avec file d'attente hors-ligne ; l'application mobile Expo (une seule app, interface par rôle) arrive après la stabilité de la v1. Le backend est Supabase (Postgres, fonctions serverless, stockage) pour qu'un développeur seul n'ait pas de serveur à exploiter.

## Considered Options

- Flutter plus web séparé : peu de code partagé entre mobile et web.
- API maison sur VPS : plus d'exploitation (déploiement, sauvegardes, authentification, SMS).
- Firebase : modèle NoSQL peu adapté aux commandes et paiements relationnels.

## Consequences

- Le hors-ligne repose sur la PWA, moins robuste qu'une base locale native ; à réévaluer avec l'app Expo.
- Dépendance à Supabase.
