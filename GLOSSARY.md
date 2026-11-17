# agro-bridge

Plateforme qui met en relation des groupements d'agriculteurs et des acheteurs professionnels à Madagascar, pour que les producteurs captent davantage de valeur.

## Language

### Acteurs

**Groupement**:
Organisation de producteurs (coopérative, association) qui publie des lots et reçoit les paiements. C'est l'unité de vente de la plateforme.
_Avoid_: Coopérative (trop restrictif), fournisseur, vendeur

**Producteur**:
Agriculteur membre d'un groupement. N'a pas de compte ; il est informé par SMS de sa part.
_Avoid_: Paysan, fermier

**Agent**:
Personne du groupement qui utilise l'application pour publier les lots et confirmer les étapes.
_Avoid_: Responsable, animateur

**Acheteur**:
Professionnel revendeur (distributeur, grossiste, restaurant, épicerie) qui réserve des lots.
_Avoid_: Client, consommateur, distributeur

**Transporteur**:
Prestataire qui achemine un lot du point de collecte à la destination. N'a pas de compte en v1.
_Avoid_: Livreur, chauffeur

**Back-office**:
Équipe interne qui valide les comptes, arbitre et réserve le transport.
_Avoid_: Admin, opérateur

**Partenaire terrain**:
Organisation (par exemple Ceffel, Fifata) qui présente et accompagne les groupements.
_Avoid_: ONG

**Agrégateur**:
Collecteur traditionnel inscrit comme groupement et noté comme tel.
_Avoid_: Collecteur, intermédiaire

### Produits et offre

**Lot**:
Stock récolté d'un produit et d'un grade, avec sa quantité, sa date de récolte et ses producteurs.
_Avoid_: Batch, stock, cargaison

**Offre**:
Lot publié avec une fourchette de prix, un point de collecte et des villes de livraison.
_Avoid_: Annonce, listing

**Apport**:
Quantité qu'un producteur donne à un lot, enregistrée au chargement.
_Avoid_: Contribution, livraison du producteur

**Grade**:
Niveau de qualité d'un produit, standard ou premium, défini par des photos de référence.
_Avoid_: Qualité, catégorie

**Sac standard**:
Sac de poids fixe par produit servant d'unité de vente et de transport.
_Avoid_: Colis, kapoaka

**Durée de conservation**:
Nombre de jours pendant lesquels un produit reste consommable après la récolte.
_Avoid_: DLC, péremption

**Fraîcheur restante**:
Part de la durée de conservation qui reste à l'arrivée du lot chez l'acheteur.
_Avoid_: Fraîcheur, vie restante

**Calendrier de récolte**:
Liste des plantations déclarées par un groupement, avec leur date de récolte prévue, sans aucun engagement.
_Avoid_: Planning, précommande

### Prix

**Fourchette de prix**:
Plancher et plafond au kilo fixés par le groupement pour une offre.
_Avoid_: Prix, tarif

**Prix de référence**:
Prix de marché au kilo d'un produit dans une ville, issu des relevés des agents et des sources publiques.
_Avoid_: Cours, mercuriale

**Coût rendu**:
Prix producteur plus transport ramené au kilo, tel que l'acheteur le paierait à destination.
_Avoid_: Prix final, prix livré

**Tarif de transport**:
Prix fixe demandé par un transporteur pour un sac standard sur une route donnée.
_Avoid_: Frais de port

### Commande

**Commande**:
Réservation d'une quantité d'un lot par un acheteur ; elle est servie par un seul groupement.
_Avoid_: Panier, achat

**Référence de paiement**:
Identifiant de la transaction mobile money, saisi par l'acheteur et confirmé par l'agent.
_Avoid_: Reçu, preuve

**Point de collecte**:
Lieu où le groupement rassemble et charge un lot.
_Avoid_: Entrepôt, dépôt

**Mission de transport**:
Trajet confié à un transporteur pour une commande.
_Avoid_: Course, livraison

**Code de livraison**:
Code envoyé par SMS au transporteur et remis à l'acheteur pour prouver la livraison.
_Avoid_: OTP, PIN

**Revue**:
État d'un lot hors des règles de prix, de transport ou de fraîcheur, en attente d'une décision du back-office.
_Avoid_: Modération

### Confiance

**Score de fiabilité**:
Part des commandes honorées par un groupement ou un acheteur.
_Avoid_: Note, réputation

**Défaut**:
Annulation d'un acheteur après le chargement, ou non-livraison d'un groupement. Deux défauts suspendent le compte.
_Avoid_: Incident, échec

**Litige**:
Désaccord sur la quantité, le grade ou le paiement d'une commande, tranché par un médiateur humain.
_Avoid_: Plainte, réclamation

**Précommande**:
Commande d'une récolte à venir, avec acompte et engagement. Absente de la v1.
_Avoid_: Réservation (réservé au stock disponible)
