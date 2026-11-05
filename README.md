# Iris Ghost — le site

Le site public d'**Iris Ghost** (*Iris Spectre* en français), un outil de rangement de coffre pour
Destiny 2. Ce dépôt ne contient **que le site** : le code de l'application est ailleurs.

| Fichier | À quoi il sert |
|---|---|
| `index.html` | la page d'accueil (plus tard : téléchargement, notes de version, crédits) |
| `callback.html` | la page de **redirection OAuth**. Bungie y renvoie le code d'autorisation, elle le passe aussitôt à l'application installée sur l'ordinateur du joueur |
| `latest.json` | la version publiée : numéro, date, lien de l'installateur, empreinte SHA-256, notes FR / EN |

## La page de redirection, en deux mots

Bungie n'accepte **qu'une seule URL de redirection** par application, et elle doit être en `https` sans
avertissement de certificat. Un `https://localhost` avec un certificat auto-signé en affiche un : pas
question de l'imposer à un joueur.

`callback.html` reçoit donc le retour de Bungie et le renvoie vers l'application locale. Le port de
l'application voyage dans `state` (`<port>.<aléa>`), et la page **ne construit que des adresses vers
`127.0.0.1`** : ce n'est pas un redirecteur ouvert. Elle ne stocke rien, n'appelle rien, ne journalise
rien. Si l'application ne répond pas, elle affiche le code à coller à la main.

Iris Ghost n'est pas affilié à Bungie, Inc.
