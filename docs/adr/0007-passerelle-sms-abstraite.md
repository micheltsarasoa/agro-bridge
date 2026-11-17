# Passerelle SMS derrière une interface, OTP rare

L'authentification et les notifications aux producteurs passent par SMS. Twilio coûte environ 0,59 USD par SMS vers Madagascar, hors de portée ; l'API Orange SMS MG coûte 30 à 50 Ar, exige une SIM Orange, ne garantit pas la réception et ne permet pas de SMS entrants. On branche Orange SMS MG par le « Send SMS Hook » de Supabase derrière une interface de passerelle, pour pouvoir changer de fournisseur, et on limite l'OTP à l'inscription et aux nouveaux appareils, avec une session de 30 jours.

## Consequences

- Aucun flux de réponse par SMS.
- Notifications aux acheteurs par application, e-mail, WhatsApp et Messenger ; le SMS est réservé à un abonnement spécial.
