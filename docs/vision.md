# agro-bridge — vision et périmètre du MVP

Document issu d'un brainstorming (grilling) mené avant tout code. Il fixe ce qui est décidé, ce qui est repoussé et ce qui reste ouvert. Le vocabulaire est défini dans [GLOSSARY.md](../GLOSSARY.md), les décisions structurantes dans [docs/adr/](./adr/), les flux et l'inventaire des écrans dans [flux-et-ecrans.md](./flux-et-ecrans.md).

## Problème

À Madagascar, les agriculteurs captent trop peu de valeur ajoutée. Ils vendent au prix que fixent des collecteurs, qui sont aussi leurs créanciers et leurs transporteurs. Exemple relevé : pomme de terre à 150 Ar au départ, 2 350 Ar au détail, l'écart couvrant en partie des coûts réels (transport, pertes).

## Vision

Une plateforme (monorepo web et mobile) qui met en relation des groupements d'agriculteurs avec des acheteurs professionnels, et qui permet à terme d'**anticiper le canal de distribution avant ou dès la récolte** grâce à la précommande.

Le MVP ne fait pas de précommande (voir [ADR 0001](./adr/0001-vente-a-la-recolte-avant-la-precommande.md)). Il met en place la vente de stock récolté, le suivi par producteur et la confiance entre les parties, qui sont les fondations de la précommande.

## Acteurs

| Acteur | Rôle dans la v1 | Accès |
| --- | --- | --- |
| **Agent du groupement** | Publie les lots, confirme paiements et chargements, répartit entre producteurs | PWA mobile, hors-ligne, malgache par défaut |
| **Acheteur** | Revendeur professionnel (distributeur, grossiste, restaurant, épicerie) qui réserve des lots | Web, français |
| **Back-office** | Équipe interne : valide les comptes, arbitre, réserve le transport, paramètre les règles | Web desktop |
| **Producteur** | Reçoit un SMS avec sa part ; n'a pas de compte | SMS en malgache |
| **Transporteur** | Reçoit une mission et un code de livraison ; n'a pas de compte | Téléphone, SMS |
| **Partenaire terrain** | Présente et accompagne les groupements | Hors plateforme |

Les consommateurs finaux (B2C) et les comptes transporteurs en libre-service viennent après le pilote.

## Périmètre du MVP

### Dans la v1

- Vente à la récolte de **stock disponible** : paddy, riz blanc, haricot ; les légumes au cycle suivant.
- Lot tracé par producteur, offre avec fourchette de prix et prix de référence affiché.
- **Coût rendu au kilo** (prix producteur + transport ramené au kilo) avec avertissement si supérieur au prix de référence.
- Contrôle de destination par règle économique ; Antananarivo seule ville ouverte au pilote.
- Frise de fraîcheur côté acheteur, durée de conservation par produit.
- Paiement par mobile money avant le chargement, référence déclarée par l'acheteur et confirmée par l'agent.
- Transport réservé par le back-office, confirmation de livraison par code SMS et par l'acheteur (photos).
- Répartition par producteur avec SMS en malgache.
- Notation, score de fiabilité, annulation gratuite avant chargement, défaut noté ensuite.
- Calendrier de récolte prévisionnel, sans engagement.
- Validation manuelle des comptes des deux côtés.

### Hors v1

- Précommande, acompte, engagement partiel, mécanismes anti-vente parallèle.
- Séquestre, intégration API des opérateurs de mobile money.
- Comptes transporteurs, annonces de fret.
- Application mobile native (Expo) ; la v1 est une PWA.
- Commande servie par plusieurs groupements ; négociation de prix ; B2C.

## Règles métier clés

- **Prix** : le groupement propose une fourchette ; l'acheteur choisit dans la fourchette, sans contre-offre.
- **Prix de référence** : relevés hebdomadaires des agents, complétés par les sources publiques (SIEL, ODR).
- **Destination** : un lot est envoyé en revue si le transport dépasse environ 25 à 30 % du coût rendu ou si la fraîcheur restante est inférieure à 50 %. Seuils paramétrables.
- **Fraîcheur** : durée de conservation par produit, fixée par le back-office, alerte sous 50 % de durée restante, sans blocage.
- **Annulation** : gratuite avant le chargement ; ensuite, défaut noté ; deux défauts suspendent le compte.
- **Unités** : kilo ou sac de poids fixe par produit, avec conversion des unités locales (kapoaka, sobika, daba…) ; deux grades illustrés par des photos.
- **Collecteurs traditionnels** : intégrés comme agrégateurs notés plutôt que contournés.

## Technique

Voir [ADR 0004](./adr/0004-pwa-web-d-abord-monorepo-typescript.md) et [ADR 0007](./adr/0007-passerelle-sms-abstraite.md).

- Monorepo TypeScript (pnpm, Turborepo), packages partagés (domaine, schémas, i18n).
- Client unique **Next.js en PWA** installable, file d'attente hors-ligne ; app Expo après la stabilité de la v1.
- Backend **Supabase** (Postgres, fonctions serverless, stockage de photos).
- Authentification par OTP SMS via l'API Orange SMS MG, derrière une interface de passerelle.

## Pilote et calendrier

- Zone : Vakinankaratra vers Antananarivo. Partenaires visés : Ceffel et Fifata (soutenus par Fert), IROOA à contacter.
- Taille : 1 à 2 groupements, 3 à 5 acheteurs, un cycle de récolte, recrutés par le réseau personnel, le partenaire et la prospection à Tana.
- Cible : récolte de riz et de haricot en **mars à mai 2027** (riz de bas-fond : récolte début mars à mi-avril selon le calendrier Météo/MINAE 2025-26), légumes en août à octobre.
- Équipe : développeur seul, à temps partiel ; pilote dans 4 à 6 mois.
- Cadre légal : pilote sous convention avec le partenaire ; création de l'entité avant le premier abonnement.

## Modèle de revenu

Abonnement B2B payé par les acheteurs, gratuit pendant le pilote. Rien n'est prélevé sur les producteurs. Les notifications SMS aux acheteurs sont réservées à un abonnement spécial.

## Mesure du succès à 6 mois

Taux de commandes honorées et prix perçu par le groupement supérieur au prix collecteur habituel.

## Roadmap après le pilote

1. Paiement par API ou séquestre, après création de l'entité.
2. Transporteur en libre-service.
3. B2C (paniers groupés).
4. Précommande avec acompte, à partir des données du calendrier de récolte.

## Risques et points ouverts

- **Concurrence** : IROOA occupe déjà la place de marché B2B de producteurs à entreprises (600 producteurs environ, via des coopératives). Sans précommande, la différence tient au suivi par producteur, au prix rendu et à la fraîcheur. Partenariat à explorer.
- **Calendrier** : mars à mai 2027 est serré pour un développeur à temps partiel.
- **Prix de référence** : pas d'API publique pour les légumes ; le SIEL (porté par le Ceffel) est en PDF et affichage. Partenariat de données ou collecte propre.
- **Mobile money** : les API (MVola, Orange Money, Airtel Money) exigent un statut de marchand et donc une entité légale ; frais et délais non publiés.
- **SMS** : Twilio vers Madagascar coûte environ 0,59 USD par SMS, non viable ; l'API Orange SMS MG coûte 30 à 50 Ar par SMS, exige une SIM Orange et ne garantit pas la réception ; pas de SMS entrant.
- **Durées de conservation et seuils** : à fixer avec le Ceffel.
- **Écrans et design system** : à concevoir dans un processus de design séparé.
- **Statut juridique** pour tout flux d'argent futur : à vérifier.
- **Question non tranchée** : ce que le groupement fait de l'argent reçu pour que la valeur arrive aux producteurs, au-delà du SMS de répartition.

## Sources de la recherche

- IROOA : https://newsmada.com/?p=201507
- Pomme de terre, écart de prix : https://www.lexpress.mg/2026/10/filiere-agricole-pommes-de-terre-du.html
- Calendrier cultural riz 2025-2026 : https://www.meteomadagascar.mg/wp-content/uploads/Calendriers_culturaux-Riz-2025-2026.pdf
- SIEL (Ceffel/Fifata) : https://servinnov.cirad.fr/content/download/4410/34546/version/2/file/FiFata_SIEL_FR_Fond-Perdu.pdf
- SMS Orange Madagascar : https://developer.orange.com/apis/sms-mg/pricing
- Tarif Twilio Madagascar : https://www.twilio.com/en-us/sms/pricing/mg
- Supabase, auth par téléphone : https://supabase.com/docs/guides/auth/phone-login
- Orange Money Web Payment : https://developer.orange.com/apis/om-webpay/faq
- Twiga Foods (leçon : ne pas posséder la logistique) : https://agfundernews.com/twigas-demise-underscores-the-need-for-new-financing-models-in-african-agrifoodtech
- Vente parallèle en agriculture sous contrat : https://www.iied.org/building-transparency-trust-smallholder-commodity-trading-contract-farming
