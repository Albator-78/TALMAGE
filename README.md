Documentation complète — TALMAGE SDE : Session Persistence Demo

1. Présentation générale

Le prototype TALMAGE SDE est une démonstration de persistance d’état côté client, centrée sur l’expérience utilisateur d’un « desktop » web simulé. Il illustre comment conserver et restaurer automatiquement des préférences d’interface, des fenêtres ouvertes et des paramètres de session via localStorage.

Ce prototype n’a pas vocation à être un système d’authentification réel, mais un environnement de test pour la gestion d’état persistant.

2. Fonctionnalités principales

2.1 Persistance de l’état utilisateur

Le système enregistre automatiquement dans localStorage :

le nom d’utilisateur

le type de session

la langue

l’état restoreHomeSession

la liste des fenêtres ouvertes

les préférences visuelles : scanlines, glow

la dernière route visitée : lastRoute

Ces données sont restaurées automatiquement au rechargement de la page.

2.2 Redirection automatique

Si authenticated est présent et vrai dans l’état persistant, l’utilisateur est redirigé vers :

/desktop

2.3 Simulation d’authentification

Le champ mot de passe est strictement visuel.

Aucun jeton réel n’est stocké.

L’objectif est uniquement de démontrer la restauration d’état.

3. Limitations connues

Aucun vrai système d’authentification n’est implémenté.

localStorage n’est pas sécurisé et ne doit pas contenir de données sensibles.

Le prototype ne gère pas les rôles, permissions ou sessions serveur.

4. Architecture technique

4.1 Structure générale

Le prototype repose sur trois composants clés :

lib/storage.js

Fournit les fonctions de lecture/écriture dans localStorage.

Centralise la logique de persistance.

components/LoginClient.js

Gère la connexion simulée.

Recharge les valeurs persistées pour pré-remplir les champs.

Met à jour l’état persistant lors de la connexion.

components/DesktopClient.js

Interface principale du « desktop ».

Mémorise les fenêtres ouvertes et les préférences UI.

Applique automatiquement les paramètres restaurés.

5. Installation et lancement

5.1 Installation

npm install

5.2 Lancement du serveur de développement

npm run dev

5.3 Accès à l’application

Ouvrir :

http://localhost:3000

6. Fonctionnement détaillé de la persistance

6.1 Cycle de vie de l’état

L’utilisateur interagit avec l’interface.

Les modifications sont enregistrées dans localStorage.

Au rechargement :

l’état est lu

les préférences sont appliquées

les fenêtres sont restaurées

la route précédente est rechargée

6.2 Exemple de structure stockée

{
  "username": "demo",
  "sessionType": "standard",
  "language": "fr",
  "windows": ["terminal", "notes"],
  "scanlines": true,
  "glow": false,
  "lastRoute": "/desktop",
  "authenticated": true
}

7. Bonnes pratiques et recommandations

Ne jamais stocker de données sensibles dans localStorage.

Prévoir une couche serveur pour toute authentification réelle.

Ajouter une expiration de session si le prototype évolue.

Utiliser un schéma de validation pour éviter les états corrompus.

8. Améliorations possibles

Implémentation d’un vrai système d’authentification (JWT, sessions serveur).

Migration vers IndexedDB pour des données plus volumineuses.

Ajout d’un système de fenêtres plus avancé (z-index, minimisation, etc.).

Support multi-profils.

Mode sombre / clair.

9. Conclusion

Ce prototype démontre efficacement comment persister et restaurer un environnement utilisateur complet dans un contexte client-side. Il constitue une base solide pour explorer des concepts de bureau virtuel, de personnalisation d’interface et de gestion d’état persistante.
